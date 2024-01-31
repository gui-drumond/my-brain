---
tags:
  - React
---
---

[[Conceitos/React/Themes/Formulários (Controlled Components vs Uncontrolled Components)/Libs que proporcionam tratativa de formulários, correção e validação (mensagens de erro)|Libs que proporcionam tratativa de formulários, correção e validação (mensagens de erro)]]

No react temos dois tipos de métodos:

- Declarativa
    
    Quando dizemos uma ação e isto ocorre de maneira automática.
    
- Imperativa
    
    Ditando o que iremos fazer de maneira que o código irá fazer para nós (manualmente).
    

  

  

Basicamente obtemos os valores do componente em tempo real e salvamos, isto ocorre com os eventos 'onChange' usando estados dentro do 'React' que é alterado a cara mudança:

```JavaScript

const [search, setSearc h] = useState('');
<input
  placeholder="Buscar na plataforma"
  value={search}
  onChange={(event)=> setSearch(event.target.value) }
/>
```

termos interessantes para serem pesquisados: debounce