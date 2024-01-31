---
tags:
  - Next
  - React
---
Nome da biblioteca que faz o gerenciamento destes cookies é a Nookies (Next + cookies)

---

  

## Como instalar ?

```JavaScript
yarn add nookies
```

## Dicas

---

Todas as vezes que formos criar/declara/inicializar um cookie sempre que for dentro do browser, ou clientSide sempre será undefined.

```JavaScript
setCookie(undefined, 'nomeDoCookie')
```

## Nome do cookies tem que ser relativos a aplicação como por exemplo:

```JavaScript
setCookie(undefined, 'nextauth.token', ValorToken, options)
```

  

### Opções do cookie customizável

```JavaScript
setCookies(undefined, 'nextauth.token', token, )
```