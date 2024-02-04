---
tags:
  - React
  - React-Hook-Form
  - Yup
  - lib
  - validação
---
Basicamente devemos fazer a instalação da lib

```JavaScript
yarn add @hookform/resolvers
```

E fazer a importação de todos os "exports" do yup pois ele não tem nenhum "export default" e também fazer a importação

```JavaScript
import * as yup from 'yup'
import { yupResolver } from '@hookform/resolvers/yup';
```

  

Está na documentação do React Hook Forms:

> [!info] Get Started  
> Installing React Hook Form only takes a single command and you're ready to roll.  
> [https://react-hook-form.com/get-started#SchemaValidation](https://react-hook-form.com/get-started#SchemaValidation)