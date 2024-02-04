---
tags:
  - Ambiente
  - Dev
  - Prod
---
### Devemos criar uma variável global de ambiente chamada env. Usaremos uma biblioteca ( lib ) para que não haja distinção de sistemas operacionais na criação.

---

Para instala-la usaremos o yarn:

```JavaScript
yarn add cross-env -D  
```

### Precisaremos configurar um script dentro da package.json para que configure a variável de ambiente e possamos consulta-la:

---

```JavaScript
"scripts": {
    "dev": "webpack server",
    "build": "cross-env NODE_ENV=production webpack"
  },
```

### Já no código devemos realizar uma condição para que entenda qual ambiente vamos rodar:

```JavaScript
const isDevelopment = process.env.NODE_ENV !== "production";
```

```JavaScript
mode: isDevelopment? "development":"production",
devtool: isDevelopment? "eval-source-map" : "source-map",
```