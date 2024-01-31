---
tags:
  - Webpack-Server
---
# O que o webserver tem de diferente do webpack normal?

---

Basicamente o webpack comum toda a vez que fazemos alguma alteração no código temos que executa-los novamente digitando "yarn webpack" para gerar um index.html para que seja visivel as novas alterações. Com o WebServer além de transformarmos todo o código e mirarmos para o bundle.js e importar no index.html, iremos captar todas alterções de forma automatizada e gerar o bundle.js e o index.html, da mesma maneira que funciona o react normal.

  

# Como instalar via yarn linha de comando

---

```JavaScript
yarn add webpack-dev-server -D
```

  

---

  

## Devemos incluir na "==module.exports==" também o devServer desta maneira:

```JavaScript
devServer: {
   contentBase: path.resolve(__dirname, "public")
  },
```

O "==devServer==" serve para que possamos indicar as propriedades e uma delas é o "==contentBase==" ele definimos seu o caminho da nossa pasta publica que fica nosso conteúdo estático da aplicação

  

  

# Para rodar o webpack server devemos colocar isso no console

---

```JavaScript
yarn webpack server
```

E vualá! pronto servidor react aberto na porta ==localhost:8080==