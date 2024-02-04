---
tags:
  - React
  - miragejs
  - mock
  - lib
---
Biblioteca para simulação de dados e mockagem, fazendo com que a aplicação possa funcionar sem um backend predefinido.

---

- Configurações
    
    Instação do mirageJS:
    
    ```JavaScript
    yarn add miragejs -D
    ```
    
      
    
    A arquitetura dentro de um projeto é :
    
    ```JavaScript
    src/
    	|
    	->	services/
    					|
    					 ->	mirage/
    								|
    								 ->	 index.ts
    ```
    
    Dentro do index.ts criaremos o server:
    
    ```JavaScript
    import { createServer } from 'miragejs'
    
    export function makeServer(){
      const server = createServer({
        models:{
          // quais os tipos de dados da aplicação
        },
        routes(){
          //quais as rotas a serem criadas
        }
      })
    }
    ```
    
    Precisaremos fazer a tipagem dos dados e assim coloca-las:
    
    ```JavaScript
    import { createServer, Model } from 'miragejs'
    
    type User = {
      name:string;
      email:string;
      create_at:number;
    }
    
    export function makeServer(){
      const server = createServer({
        models:{
          user: Model.extend<Partial<User>>({})
        },
        routes(){
          //quais as rotas a serem criadas
        }
      })
    }
    ```
    
      
    
    Na declaração de rotas, teremos o shorthands é o termo usado na documentação da lib, basicamente é um CRUD completo, listando no get e salvando no post:
    
    ```JavaScript
    export function makeServer(){
      const server = createServer({
        models:{
          user: Model.extend<Partial<User>>({})
        },
        routes(){
          this.get('/users');
          this.post('/users');
        }
      })
      return server;
    } 
    ```
    
      
    
    Após isto chamaremos a função dentro a app.ts com a condição de rodar apenas em ==development==, essa variável é criada pelo próprio nextJS de forma automática.
    
    ```JavaScript
    if(process.env.NODE_ENV === 'development') {
      makeServer();
    }
    ```
    
      
    
    Finalizando a criação:
    
    ```JavaScript
    
    export function makeServer(){
      const server = createServer({
        models:{
          user: Model.extend<Partial<User>>({})
        },
        routes(){
          // rodar o barra do nosso localhost, cuidado para nao colocar o mesmo nome da pasta api (o padrao do nextJS) 
          this.namespace = 'api2';  
          this.timing = 750; // tempo de execucao perfeito para teste de loaders
    
          this.get('/users');
          this.post('/users');
    
          this.passthrough() // fazer com que as chamadas serem passadas pelo mirage, caso nao encontrem repassam para outras rotas
        }
      })
      return server;
    }
    ```
    
      
    
      
    
- Recursos
    - Seeds
        
        As seeds servem para que possamos criar dados para que nossas rotas de api não fiquem vazias
        
          
        
    - factories
        
        As seeds servem para que possamos gerar dados em massa para não criar todos os dados na mão
        
    - Faker ( uma lib para que possamos criar dados fictícios )