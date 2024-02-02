---
Created: 2022-01-26T09:12
Last Edited Time: 2022-01-26T09:12
Tag:
  - Axios
Created By: Guilherme Drumond
---
# Para que serve?

---

Serve para fazer a requisições em apis e fazer a conexão com end points.

# Como instalar?

---

```JavaScript
yarn add axios
```

# Como usar?

---

Precisamos criar um arquivo que irá definir o local da api.

```JavaScript
import axios from "axios";

export const api = axios.create({
    baseURL: 'http://localhost:3000/api',
});
```

  

Já em outro arquivo iremos consumir essas informações usaremos:

```JavaScript
useEffect(() => {
        api.get('transactions')
        .then( response => response.data)
    }, [])
```