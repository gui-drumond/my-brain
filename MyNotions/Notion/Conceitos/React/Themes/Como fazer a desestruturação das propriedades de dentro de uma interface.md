Com uma interface ficaria assim:

```JavaScript
interface ComponenteExemploProps{
	nome: string;
}

export function ComponenteExemplo({ nome }: ComponenteExemploProps ){
  return(<></>)
}
```

Sem uma interface:

```JavaScript

export function ComponenteExemplo({ nome, numero, cpf }){
  return(<></>)
}
```