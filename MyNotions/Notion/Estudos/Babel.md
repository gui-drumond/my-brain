---
Created: 2022-01-26T09:12
Last Edited Time: 2022-01-26T09:12
Tag:
  - Concluido/Revisado
  - React
Created By: Guilherme Drumond
---
# Para que serve o Babel?

---

Tradução/conversão do JavaScript para o navegador.

  

## Instalação

---

```Elixir
yarn add @babel/core @babel/cli @babel/preset-env @babel/preset-react -D 
```

Essa classificação "-D" significa que é uma dependência de desenvolvimento, que não irá subir no pacote de produção na hora do deploy

  

- Babel Core
    
    É 90% o core em si, a própria biblioteca
    
- Babel CLI
    
    É a execução via linha de comando
    
- Babel Preset ENV
    
    É um identificador de ambiente
    

  

## Pós instalação

---

- Criar um arquivo chamado "babel.config.js"
    
    Relacionar o Babel com o package:
    
    - "==presets==": isso significar que ele irá linkar com as libs instaladas ao babel, umas delas é o react
    - " ==['@babel/preset-react', {runtime: 'automatic' }]== " Isso significa que para o react→ ele receba em tempo de execução definição automática para sem que precisamos importar o react em todos os arquivos, na qual se usa o react

```JavaScript
module.exports = {
    presets: [
        '@babel/preset-env',
        ['@babel/preset-react', {
            runtime: 'automatic'
        }]
    ]
}
```

## Executar o Babel

---

```JavaScript
yarn babel "caminho do arquivo" --out-file "nome do arquivo traduzido que será gerado"

yarn babel src/index.jsx --out-file dist/bundle.js
```

- Geralmente o bundle ele é o nome do arquivo que é convertido pelo Babel.