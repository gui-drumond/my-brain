---
tags:
  - Source-Map
---
# Para que serve o source map?

---

O source map serve para que ele mostre realmente onde está localizado o erro na aplicação e não mostre apenas o bundle convertido onde o código estará modificado e quase impossível de ser entendido. Com o Source Map instalado conseguiremos visualizar o código original para debugs e visualizar os erros.

  

## Instalação do Souce Map

---

Na "==module.exports==" do webpack devemos colocar "devtool:" temos várias e está abaixa é a dependência de desenvolvimento.

```JavaScript
devtool:"eval-source-map",
```

---

## Como deve ficar o código

---

```JavaScript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin")
module.exports = {
  mode:"development",
  devtool:"eval-source-map",
  entry: path.resolve(__dirname, "src", "index.jsx"),
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },
  devServer: {
   contentBase: path.resolve(__dirname, "public")
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