---
tags:
  - Cache
  - React
  - react-query
---
# Para que serve esta lib de controle de cache?

---

## Neste modelo iremos aprender a usar o react-query para cachear, fazer a comparação e validação com informações novas, contras as obsoletas, determinando o tempo de vida do cache e seu estado.

---

- Como fazer a instalação
    
    ```JavaScript
    yarn add react-query
    ```
    

## Como funciona o cacheamento:

Este trecho de código é um usuário passado para requisição (número id é passado ao clicar no botão). O prefetch faz o pré carregamento para que ao ser consultado futuramente ele apenas mostre os dados.

```JavaScript
async function handlePrefetchUser(userId: number){
    await queryClient.prefetchQuery(['user', userId], async () => {
      const response = await api.get(`users/${userId}`)
      return response.data;
    }, {
      staleTime: 1000 * 60 * 10, //10 minutes
    })
  }
```