---
tags:
  - css
  - estilos
  - styles
---
### Para que possamos usar estilos dentro do Webpack necessitamos de um "loader", como já temos o loader do "babel" para rodar arquivos com extensões "jsx" e "js", necessitamos de um para o "css" e fazer uma regra para que o webpack entenda isto.

---

### Antes de tudo vamos instalar o loader:

---

```JavaScript
yarn add style-loader css-loader
```

  

### Agora iremos adicionar a regra a modules do Webpack

---

```JavaScript
module.exports = {
  mode: isDevelopment?"development":"production",
  devtool: isDevelopment?"eval-source-map" : "source-map",
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
      {
        test: /\.css$/,
        exclude: /node_modules/,
        use: ["style-loader","css-loader"],
      },
    ],
  },
};
```