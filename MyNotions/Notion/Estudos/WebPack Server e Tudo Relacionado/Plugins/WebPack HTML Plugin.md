---
tags:
  - Html
  - plugin
---
# Plugin do Webpack para gerar index.html de forma automatizada

---

Temos que executar o código no terminal

```JavaScript
yarn add html-webpack-plugin -D
```

  

### Importar o plugin nas configs do webpack (file: "webpack.config.js")

---

As partes que devem ser inseridas são:

- Para importação da lib adicionada
    
    ```JavaScript
    const HtmlWebpackPlugin = require("html-webpack-plugin")  
    ```
    
- Para implementação do plugin no "==module.exports=="
    
    ```JavaScript
     plugins: [
       new HtmlWebpackPlugin({
          template: path.resolve(__dirname, "public", "index.html"),
    	   })
      ],
    ```
    

  

### O documento deve ficar dessa forma:

---

```JavaScript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin")
module.exports = {
  mode:"development",
  entry: path.resolve(__dirname, "src", "index.jsx"),
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },
  plugins: [
   new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "public", "index.html"),
   })
  ],
  resolve: {
    extensions: [".js", ".jsx"],
  },
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: "babel-loader",
      },
    ],
  },
};
```