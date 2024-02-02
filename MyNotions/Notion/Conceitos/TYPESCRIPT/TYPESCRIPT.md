---
Created: 2022-01-27T13:38
Last Edited Time: 2022-01-27T13:40
Created By: Guilherme Drumond
---
---

  

- Sempre quando usar bibliotecas que ja tem tipagem e estiver criando interfaces, distribuindo para outros componentes lembrar que todas elas ja tem suas proprias tipagem é só pesquisar.
- Generic
    
      
    
- Partial
    
    Quando queremos que quem esteja recebendo a tipagem não precise ter todos os campos em específico
    
    ```JavaScript
    type User = {
      name:string;
      email:string;
      create_at:number;
    }
    
    Model.extend<Partial<User>>({})
    ```
    

  

- Children
    
    Quando passamos tags comuns, filhas ou textos a tipagem se comporta assim:
    
    ```JavaScript
    interface ComponentProps{
    	children: ReactNode;
    }
    ```
    
    Quando só podemos receber um componente como children:
    
    ```JavaScript
    interface ComponentProps{
    	children: ReactElement;
    }
    ```
    
- Extender propriedades de outras já existentes
    
    ```JavaScript
    
    
    import Link, { LinkProps } from 'next/link';
    
    interface ActiveLinkProps extends LinkProps{
      
    }
    
    export function ActiveLink({..rest}){
      return()
    }
    ```
    
      
    

 