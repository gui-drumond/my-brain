---
tags:
  - react-query
  - Cache
---
### 1. Utilizando o react query para fazer um cacheamento comum.


Exemplo abaixo

```js

const { data: profile, isLoading: isLoadingProfile } = useQuery({

    queryKey: ['profile'],

    queryFn: getProfile,

    staleTime: Infinity,

  })

```

