# Diagramação do Banco de Dados

## **Armazenamento de datas disponíveis**

### Primeira abordagem

- Salvar `endDate` e `startDate` na entidade viagem.
- Criar tabela `TRIP_RESERVATIONS` e colocar o range de datas reservadas:
    
    ```TypeScript
    interface TripReservation {
        userId: string;
        tripId: string;
        startDate: string;
        endDate: string
    }
    ```
    
- Sempre que reservarmos uma viagem, atualizar o `startDate` e `endDate` da viagem?
    - Sim: deleções manuais de reservas poderiam tirar a legitimidade dos dados
    - Não: teríamos duas fontes de verdade, dados ficariam confusos

**Desvantagens**

- Query para recuperar os dias disponíveis de uma viagem ficaria bem complicada
- Teríamos duas fontes de verdade, o que é ruim (duas tabelas)

  

### Segunda abordagem

- **Não salvar** `startDate` e `endDate` na tabela de viagens.
- Criar tabela `TRIP_AVAILABILITY`, que será responsável por armazenar os dias disponíveis de cada viagem, junto com o seu status de reserva (ocupado ou não ocupado).
- Quando o usuário reservar uma viagem, alteraremos os registros presentes nessa tabela.

# Setup do Projeto e Prisma

## 1. Inicializar Projeto

```Bash
npx create-next-app@latest --use-yarn .
```

## 2. Configurar Prisma Client

Criar arquivo lib/prisma.ts com o seguinte:

```TypeScript
import { PrismaClient } from "@prisma/client";

const globalForPrisma = global as unknown as { prisma: PrismaClient };

export const prisma =
  globalForPrisma.prisma ||
  new PrismaClient({
    log: ["query"],
  });

if (process.env.NODE_ENV !== "production") globalForPrisma.prisma;
```

Esse código garante que apenas uma instância do Prisma vai ser instanciada, e que o Hot Reload do servidor de desenvolvimento não criará várias instâncias.

## 3. Configurar Models

Gerar Model do Prisma seguindo a diagramação feita anteriormente.

```JavaScript
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model Trip {
  id           String            @id @default(uuid())
  name         String
  description  String?
  startDate    DateTime
  endDate      DateTime
  tags         String[]
  location     String
  coverImage   String
  images       String[]
  users        User[]
  reservations TripReservation[]
  pricePerDay  Decimal           @db.Decimal(8, 2)
  highlights   String[]
  recommended  Boolean           @default(false)
}

model TripReservation {
  id        String   @id @default(uuid())
  trip      Trip     @relation(fields: [tripId], references: [id])
  tripId    String
  name      String
  startDate DateTime
  endDate   DateTime
}
```

  

## 4. Conceitos do Next.js

### Sistema de Rotas

- Cada pasta dentro do `app` é tratada como uma rota.
- Cada uma dessas rotas possui um `layout` que é colocado em volta dela.

**Exemplo:**

![[Untitled.png]]

Neste caso, teríamos duas rotas: a home page (/) e a /about. Poderíamos também criar um `layout` para a rota /about.

**Rotas** _**catch-all**_

Essas rotas sempre serão exibidas mesmo se passarmos parâmetros adicionais. Elas são definidas como `[...about]`. Por exemplo:

![[Untitled 1.png]]

Se acessarmos `about/a` ou até mesmo `about123` essa `page.tsx` será renderizada.

### Server Componentes

Dentro de Server Components podemos pegar dados diretamente do nosso banco de dados, já que eles são renderizados totalmente do lado do servidor.

  

O Next.js conta, inclusive, com uma função `fetch` especial para usarmos nesses casos:

```TypeScript
async function getData() {
  const res = await fetch('https://api.example.com/...')
  // The return value is *not* serialized
  // You can return Date, Map, Set, etc.
 
  // Recommendation: handle errors
  if (!res.ok) {
    // This will activate the closest `error.js` Error Boundary
    throw new Error('Failed to fetch data')
  }
 
  return res.json()
}
 
export default async function Page() {
  const data = await getData()
 
  return <main></main>
}
```

Podemos também adicionar um componente de `loading` para essa página, criando um arquivo `loading.tsx` dentro da sua pasta.

  

**Cache**

Por padrão, requisições feitas com o `fetch` do Next.js em Server Components possuem cache “eterno”. Ou seja, elas são feitas uma vez e as requisições subsequentes são pegas do cache.

Para mudar isso, podemos usar o parâmetro `revalidate`, que define o período em que esse cache vai ser invalidado:

```TypeScript
fetch('https://...', { next: { revalidate: 10 } })
```

Podemos desativá-lo por completo ao definir:

```TypeScript
fetch('https://...', { cache: 'no-store' })
```

Entretanto, eles possuem algumas limitações, como:

- Não podem armazenar state (useState)
- Não possuem ciclo de vida (useEffect)
- Não podem ser interativos (onClick)

Nessas situações, devemos utilizar os **Client Components**.

  

### Client Components

Os Client Components são componentes “normais”, que possuem interatividade, state e ciclo de vida. Entretanto, não podem pegar dados direto do banco de dados, como o seu irmão, por ser renderizado do lado do cliente (navegador).

  

Nesses componentes, devemos fazer o fetch de dados de forma convencional, utilizando um useEffect, por exemplo.

  

**Server Actions**

Outra possibilidade é usarmos Server Actions. Elas são funções que são executadas no lado do servidor e podem ser criadas em Client Components. Entretanto, elas ainda estão em beta. Exemplo:

```JavaScript
async function addItem(data) {
    'use server'
 
    const cartId = cookies().get('cartId')?.value
    await saveToDb({ cartId, data })
  }
```

## 5. Sistema de Autenticação

Para autenticação, vamos usar o Next Router em conjunto com o Prisma. O próprio Next Auth fornece um [Adapter](https://next-auth.js.org/v3/adapters/prisma) para trabalharmos com o Prisma.

  

Vamos também usar o Supabase para hospedarmos um Postgres na Cloud.

  

Algumas configurações necessárias:

### Definir Schemas do Next Auth

```JavaScript
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "sqlite"
  url      = "file:./dev.db"
}

model Account {
  id                 String    @id @default(cuid())
  userId             String
  providerType       String
  providerId         String
  providerAccountId  String
  refreshToken       String?
  accessToken        String?
  accessTokenExpires DateTime?
  createdAt          DateTime  @default(now())
  updatedAt          DateTime  @updatedAt
  user               User      @relation(fields: [userId], references: [id])

  @@unique([providerId, providerAccountId])
}

model Session {
  id           String   @id @default(cuid())
  userId       String
  expires      DateTime
  sessionToken String   @unique
  accessToken  String   @unique
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
  user         User     @relation(fields: [userId], references: [id])
}

model User {
  id            String    @id @default(cuid())
  name          String?
  email         String?   @unique
  emailVerified DateTime?
  image         String?
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt
  accounts      Account[]
  sessions      Session[]
}

model VerificationRequest {
  id         String   @id @default(cuid())
  identifier String
  token      String   @unique
  expires    DateTime
  createdAt  DateTime @default(now())
  updatedAt  DateTime @updatedAt

  @@unique([identifier, token])
}
```

### Definir Rotas do Next Auth

```TypeScript
import NextAuth, { AuthOptions } from "next-auth";
import GoogleProvider from "next-auth/providers/google";
import { PrismaAdapter } from "@auth/prisma-adapter";
import { Adapter } from "next-auth/adapters";

import { prisma } from "@/lib/prisma";

export const authOptions: AuthOptions = {
  adapter: PrismaAdapter(prisma) as Adapter,
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    }),
  ]
};

const handler = NextAuth(authOptions);

export { handler as GET, handler as POST };
```

  

### Gerar API Key do Google

Acessar [Google Developers Console](https://console.cloud.google.com/) e criar um projeto.

  

Ao criar o projeto, selecioná-lo e ir em Menu → Credenciais → ID do Cliente OAuth.

  

Configurar as telas de consentimento e colocar a seguinte URL como URL de Redirecionamento:

> [!important]  
> http://localhost:3000/api/auth/callback/google  

  

Após isso, pegar as chaves e colocar no .env do projeto.

### Criar o NextAuthProvider

O Provider ficará em volta de toda a nossa aplicação, para que a mesma tenha acesso ao usuário logado.

```TypeScript
"use client";

import { SessionProvider } from "next-auth/react";

type Props = {
  children?: React.ReactNode;
};

export const NextAuthProvider = ({ children }: Props) => {
  return <SessionProvider>{children}</SessionProvider>;
};
```

```TypeScript
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={poppins.className}>
        <NextAuthProvider>
          {children}
        </NextAuthProvider>
      </body>
    </html>
  );
}
```

  

  

Após configurarmos com sucesso, conseguimos fazer o login do usuário com a função `signIn` e o logout com a `signOut`. Ambas importadas no Next Auth.

  

Para acessarmos o usuário logado em Client Components, usamos o hook `useSession`. Em Server Components, podemos usar a função `getServerSession`.