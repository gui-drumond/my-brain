---
tags:
  - Ambiente
  - Dev
  - Instalação
  - plugin
---
## O que o Fast Refresh faz?

---

Ele mantém os estados dos componentes após uma renderização de alteração de código. Ex: você tem um carrinho de compras e está com ele cheio pronto para testar o pagamento, mas altera um texto e quando o webpack renderiza novamente ele limpa seu carrinho e você precisa fazer o processo tudo denovo... Para isso foi criado o Fast Refresh que faz com que os estados e os componentes não se percam! no exemplo acima ele manteria os itens no carrinho e alteraria apenas o texto na renderização.

---

  

## Como faz sua instalação?

---

Link de consulta: [https://github.com/pmmmwh/react-refresh-webpack-plugin](https://github.com/pmmmwh/react-refresh-webpack-plugin)

```JavaScript
yarn add -D @pmmmwh/react-refresh-webpack-plugin react-refresh 
```

### Iremos agora fazer a integração pós instalar essas dependências

---

Dentro do arquivo "==webpack.config.js==" deve ficar desta forma: lembrando que neste arquivo temos integrado também babel, source-map, css e sass loader. Logo estou marcando em amarelo tudo que foi usado do "==FastRefresh==".

```JavaScript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const isDevelopment = process.env.NODE_ENV !== "production";
const ReactRefreshWebpackPlugin = require("@pmmmwh/react-refresh-webpack-plugin");

module.exports = {
  mode: isDevelopment?"development":"production",
  devtool: isDevelopment?"eval-source-map" : "source-map",
  entry: path.resolve(__dirname, "src", "index.jsx"),
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "bundle.js",
  },
  devServer: {
   contentBase: path.resolve(__dirname, "public"),
   hot: true,
  },
  plugins: [
   isDevelopment && new ReactRefreshWebpackPlugin(),
   new HtmlWebpackPlugin({
      template: path.resolve(__dirname, "public", "index.html"),
   })
  ].filter(Boolean),
  resolve: {
    extensions: [".js", ".jsx"],
  },
  module: {
    rules: [
      {
        test: /\.jsx$/,
        exclude: /node_modules/,
        use: {
          loader:"babel-loader",
          options:{
            plugins:[
              isDevelopment && require.resolve('react-refresh/babel')
            ].filter(Boolean)
          }
        },
      },
      {
        test: /\.scss$/,
        exclude: /node_modules/,
        use: ["style-loader","css-loader","sass-loader"],
      },
    ],
  },
};
```