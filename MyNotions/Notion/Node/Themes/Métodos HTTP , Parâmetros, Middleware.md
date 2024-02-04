---
tags:
  - Node
---
Métodos HTTP

  
GET: Buscar informações do back-end.  
  
GET: Buscar informações do back-end.  
  
POST: Criar uma informação no back-end.  
  
PUT/PATCH: Alterar uma informação no back-end  
PUT: Para atualizar todos dados ao mesmo tempo.  
PATCH: Para atualizar uma informação especifica.  
  
DELETE: Deletar uma informação no back-end.  

  

Parâmetros

  
Query Params: Filtros e paginação.  

Route Params: Identificar recursos para (Atualizar/Deletar).

Request Body: Conteúdo na hora de criar ou editar um recurso (JSON).  
  

Middleware

Ele é um interceptador de requisições, pode interromper totalmente a requisição ou alterar dados da requisição.

function logRequests (request, response, next){

const {method, url } = request;

  

const logLabel = ‘’;

  

return next(); // Próximo middleware

}

É utilizado quando queremos que algum trecho de rota seja disparado de forma automática em uma ou mais rotas.