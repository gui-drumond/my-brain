---
Created: 2022-01-26T09:12
Last Edited Time: 2022-01-26T09:12
Tag:
  - MirageJS
Created By: Guilherme Drumond
Participants: Guilherme Drumond
---
# O que é MirageJS ?

---

MirageJS é um servidor de backend interpretado com várias utilidades, mas seu real objetivo é ser um backend temporário como um JSON SERVER

# Como instalar MirageJS ?

---

```JavaScript
yarn add miragejs
```

  

# Como usar o MirageJS ?

---

Na função abaixo temos:

- "==createServer()==" para iniciar a função do mirage de criar o servidor
- "==routes()==" que usamos para administrar as rotas da aplicação que serão expostas
- "==this.namespace==" é o próprio BARRA do link ex:
    
    "testebackend.com/==api==/testes" Este é o namespace.
    
- "==this.get()==" seria o tipo de requisição que iremos fazer ao bater no BARRA ou melhor "==namespace==" e dentro dele passamos qual o alvo que seria outro barra mas acessando dentro do namespace que é "==/transactions==", logo em seguida passamos uma função de retorno (callback) com um json ou data;

```JavaScript
createServer({
	routes(){
		this.namespace = 'api';
		this.get('/transactions', () => {
			return[{
							id:1,
							title: 'Transaction',
							amount: 400,
							type:'deposit',
							category:'Food',
							createdAt: new Date()
			}]
		})
	}
})
```