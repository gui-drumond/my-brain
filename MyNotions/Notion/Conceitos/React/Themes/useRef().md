---
tags:
  - React
---
---

Usado para minimizar a quantidade de renderização. Vinda para ajudar a criar "Uncontrolled Components"

Todo componente ao ser criado no react recebe um atributo dentro do componente, este atributo é o "ref", ele pode ser referenciado e declarado assim:

```JavaScript
const searchInputRef = useRef<HTMLInputElement>(null);
 <input
	
	ref={searchInputRef}
  />
```

Ao invés de:

```JavaScript
const [search, setSearch] = useState('');
    <input
		value={search}
    onChange={(event)=> setSearch(event.target.value) }
		/>
```

  

Para acessar o valor resultante do ref usamos :

```JavaScript
console.log(searchInputRef.current.value)
searchInputRef.current.focus() // para dar focus em um button (modo imperativo)
```

---

# Encaminhamento de Ref por dentro dos componentes

---

Para repassar a "ref" para um componente filho, não podemos passar ele em formato de propriedade e ajusta-la na tipagem do react.

Devemos:

- Transformar a função que retorna o componente em uma constante
- Usar um hook que se chama "forwardRef()" para repassar a ref e poder utiliza-la
- Para poder usar a "ref", precisamos ter ciência que primeiro parâmetro vem a =="props"== e a =="ref"== em segundo
- fazer a tipagem da "==ref==", juntamente com da "==props=="

### Antes:

```JavaScript
export function Input({name, label, ...rest }:InputProps){
  return(
    <FormControl>
      { !!label && <FormLabel htmlFor={label}>{label}</FormLabel>}
      <ChakraInput
        name={name}
        id={name}
        bgColor="gray.900"
        focusBorderColor="pink.500"
        variant="filled"
        _hover={{
          bgColor: "gray.900",
        }}
        size="lg"
        {...rest}
      />
  </FormControl>
  );
}
```

### Depois:

```JavaScript
const InputBase = ({name, label, ...rest }:InputProps, ref) => {
  return(
    <FormControl>
      { !!label && <FormLabel htmlFor={label}>{label}</FormLabel>}
      <ChakraInput
        name={name}
        id={name}
        bgColor="gray.900"
        focusBorderColor="pink.500"
        variant="filled"
        _hover={{
          bgColor: "gray.900",
        }}
        size="lg"
        {...rest}
      />
  </FormControl>
  );
}


export const Input = forwardRef(InputBase)
```