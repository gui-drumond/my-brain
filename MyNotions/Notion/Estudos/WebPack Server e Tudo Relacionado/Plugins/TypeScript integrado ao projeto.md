---
tags:
  - Ambiente
  - Instalação
  - Server
  - TypeScript
---
# Como instalar ?

---

Primeiramente precisamos colocar o typescript dentro do projeto com o yarn

```JavaScript
yarn add typescript -D
yarn tsc --init
```

  

Após isto devemos gerar o arquivo de configuração do typescript chamado "==tsconfig.json==" que dentro dele deve conter as seguintes opções:

```JavaScript
{
  "compilerOptions": {
    "lib": ["dom","dom.iterable","esnext"],
    "allowJs": true,
    "jsx": "react-jsx",
    "noEmit": true,
    "strict": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src"]
}
```

  

Bom detalhando ao certo o que cada uma faz é:

- "==lib==" é o que usaremos de funcionalidades ques estaremos usando a dom do html, esnext e etc.
- "==allowJs==" basicamente é a permissão para que funcione "js" junto com "ts" pois estamos fazendo uma transição
- "==jsx==" é o jsx do react, que usaremos html
- "==noEmit==" Na hora do build da aplicação não gerar o código da aplicação
- "==strict==" modulos de resolver erros
- "==resolveJsonModule==" adiciona a possibilidades de importar arquivos Json
- "==include==" aponta qual pasta estará todos os arquivos do ts

  

## Agora com o arquivo criado mostraremos ao babel que estamos fazendo essa integração com o typescript

---

Para isto iremos instalar um loader do babel que lê o typescript

```JavaScript
yarn add @babel/preset-typescript -D
```

E iremos referenciar ele dentro das configurações do babel no arquivo (==babel.config.js==)

```JavaScript
module.exports = {
    presets: [
        '@babel/preset-env',
        '@babel/preset-typescript',
        ['@babel/preset-react', {
            runtime: 'automatic'
        }]
    ]
}
```

## Já para o Webpack iremos adicionar as novas configurações para o TypeScript

---

```JavaScript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");
const isDevelopment = process.env.NODE_ENV !== "production";
const ReactRefreshWebpackPlugin = require("@pmmmwh/react-refresh-webpack-plugin");

module.exports = {
  mode: isDevelopment?"development":"production",
  devtool: isDevelopment?"eval-source-map" : "source-map",
  entry: ["babel-polyfill", path.resolve(__dirname, "src", "index.tsx")],
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
    extensions: [".js", ".jsx",".ts", ".tsx"],
  },
  module: {
    rules: [
      {
        test: /\.(j|t)sx$/,
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

  

# Pronto! Agora somente instalar as Dependências/Tipagens

---

Se caso você usa qualquer outra tipagem que esteja falto é neste modelo:

```JavaScript
yarn add @types/react-dom -D
```