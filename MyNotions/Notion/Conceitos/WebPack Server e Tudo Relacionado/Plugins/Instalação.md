---
tags:
  - Instalação
  - configuração
---
# Instalando o webpack no projeto

---

```JavaScript
yarn add webpack webpack-cli -D
```

  

## Criando o arquivo de configuração na raiz do projeto

---

- Deve se chamar webpack.config.js
    
    Dentro dele temos:
    
    - "==mode==" Em qual ambiente está o projeto? aqui definimos como "development" ou "==production=="
    - "==entry==" você deve especificar o local onde o arquivo principal está
    - "==output==" você deve especificar o local onde o será gerado o arquivo
    - "==resolve: extensions==" você deve especificar a extensão dos arquivos que ele irá monitorar e com isto ao fazer um importação ele automaticamente irá reconhecer o arquivo sem que você precise especificar seu formato(extensão, ex: ==js, jsx==).
    - "==module==" configurações que ele se comportará ao importar img, videos, css arquivos e etc
        - "==rules==" arrays de regras criando um objeto para cada tipo de arquivos
            - "==test==" definir o tipo do final do arquivo ex: ==/\.jsx$/==
            - "==exclude==" retirar do monitoramento de arquivos
            - "==use==" para fazer integrações com outras bibliotecas ex: babel
    
      
    
      
    
    ```JavaScript
    module.exports = {
    	mode:"development",
    	entry: "src/index.jsx".
    	output: {
    		path: "dist",
    		filename:"bundle.js"
    	}
    	resolve:{
    		extensions:['.js','.jsx']
    	},
    	module:{
    		rules: [
    			{
    				test: /\.jsx$/,
    				exclude: /node_modules/
    				use: 'babel-loader',
    			},
    		],
    };
    ```
    

### ==Caso tenha problemas de Path ( Diretórios/Caminhos ) devidos aos sistemas operacionais, sabendo disso usamos uma função do node que trata esse caminho para nós...==

```JavaScript
const path = require('path');

module.exports = {
	mode:"development"
	entry: path.resolve(__dirname, "src","index.jsx"),
	output: {
		path: path.resolve(__dirname,"dist"),
		filename:"bundle.js"
	},
	resolve:{
		extensions:['.js','.jsx']
	},
		module:{
			rules: [
				{
					test: /\.jsx$/,
					exclude: /node_modules/,
					use: 'babel-loader',
				},
			],
	}
};
```

---