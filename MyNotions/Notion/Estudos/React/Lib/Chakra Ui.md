---
tags:
  - React
  - lib
  - Estilização
---
---

## Chakra ui com react, especificamente NextJS

  

Documentation

> [!info] Getting Started  
> Inside your React project directory, install Chakra UI by running either of the following: For create-react-app installation instructions, check this CRA templates guide.  
> [https://chakra-ui.com/docs/getting-started](https://chakra-ui.com/docs/getting-started)  

  

  

## Providers

---

Como fazer para criar provider de onClose, onOpen, isOpen e etc.

Só importar useDisclosure que é um hook e desmembrar as funções de dentro dele ou passar o hook inteiro.

```JavaScript
const { onClose } = useDisclosure()
const disclosure  = useDisclosure()
```

  

## Forms

---

Potenciais erros de formulários:

- Colocar:
    
    ```JavaScript
    <Box
    as="form" 
    flex="1"
    borderRadius={8}
    bg="gray.800"
    p={["6","8"]}
    onSubmit={}></Box>
    ```