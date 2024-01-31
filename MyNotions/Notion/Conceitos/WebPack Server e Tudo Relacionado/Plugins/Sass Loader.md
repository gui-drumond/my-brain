## Integração do Webpack com o SASS via SASS loader

---

## Instalação

```JavaScript
yarn add sass-loader -D //instalação para o loader
yarn add node-sass -D // instalação do Sass
```

  

## Integração

---

Dentro da module.exports do webpack.config.js devemos incluir o loader do SASS dentro de "rules" que fica em "module" .

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
        test: /\.scss$/,
        exclude: /node_modules/,
        use: ["style-loader","sass-loader","css-loader"],
      },
    ],
  },
};
```