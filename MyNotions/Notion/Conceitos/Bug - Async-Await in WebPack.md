---
Created: 2022-01-26T09:12
Last Edited Time: 2022-01-26T09:12
Tag:
  - Bugs
  - React
Created By: Guilherme Drumond
---
### Caso queira fazer um async await no WebPack devemos adiocionar um lib chamada "==polyfill=="

```JavaScript
yarn add -D babel-polyfill
```

  

### Dentro do "==module.export==s" dentro do arquivo "==webpack.config.js=="

```JavaScript
entry: ["babel-polyfill", path.resolve(__dirname, "src", "index.jsx")],
```

  

  

### E assim poderemos utilizar esses códigos abaixo:

```JavaScript
const [repositories, setRepositories] = useState([]);

  useEffect(() => {
    async function getRepositories() {
      try {
        const response = await fetch(API_URL);
        if (!response.ok) {
          const message = `An error has occurred: ${response.status}`;
          throw new Error(message);
        }
        const repositories = await response.json();
        setRepositories(repositories);
      } catch (e) {
        console.error(e.message);
      }
    }

    getRepositories();
  }, []);
```

# ou

  

```JavaScript
const [repositories,setRepositories] = useState([]);

    useEffect(() => {
         async function getRepos(){
           await fetch("https://api.github.com/users/skillado/repos")
            .then(response => response.json())
            .then(repositories => setRepositories(repositories))
         }
         getRepos();
        }
    ,[])
```