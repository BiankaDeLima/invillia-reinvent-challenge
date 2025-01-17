# Invillia Reinvent - Challenge

Agora é a hora de colocarmos em prática tudo o que relembramos em nossas sessões e o que pudemos estudar à mais durante esse tempo.

Para tal propomos aqui um desafio.


## Challenge

Devemos construir um componente dessa e-store que viemos evoluindo durante o programa. 

Este componente é uma aplicação REST que tem por objetivo servir operações sobre um carrinho de compra.

Para esse desafio solicitamos que atendam:
* Criem uma aplicação **funcional**
* As operações implementadas respeitem a convenção **REST** (Methods e Response)
* Seja implementado usando **Java 11+** e **Spring Boot 2.5.3+**
* Seja implementado um código **legível** e **organizado**
* Atendam as **User Stories** abaixo descritas e os **contratos** estabelecidos
* Utilizar uma base de dados para o armazenamento das informações
* README atualizado com instruções de execução


## Epic

Continuamos a desenvolver a nossa e-store. Agora precisamos construir o carrinho de compras (shopping-cart).

### US 1

Eu, como comprador, quero ter um único carrinho de compras onde eu possa adicionar produtos.

### US 2

Eu, como comprador, quero adicionar um ou mais de um item de cada produto.

### US 3

Eu, como comprador, quero listar os itens no meu carrinho de compra.

### US 4

Eu, como comprador, quero incrementar a quantidade de um produto já no carrinho.

### US 5

Eu, como comprador, quero remover todos os items de um mesmo produto do carrinho.

### US 6

Eu, como comprador, quero decrementar a quantidade de um produto já no carrinho.

### US 7

Eu, como comprador, quero calcular o valor total dos itens no meu carrinho.

### US 8

Eu, como comprador, quero esvaziar meu carrinho.


## Contratos de Interface

### Adicionar itens
`POST /shopping-cart/<user-id>/items/<SKU>`

Body
```
{
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1 //optional, default value 1
}
```

Response
`CREATED 201`

```
{
    "sku":"ASDFGHJK",
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1
}
```

### Editar itens
`PUT /shopping-cart/<user-id>/items/<SKU>`

Body
```
{
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1 //optional, default value 1
}
```

Response
`OK 200`

```
{
    "sku":"ASDFGHJK",
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1
}
```

### Editar a quantidade de itens
`PATCH /shopping-cart/<user-id>/items/<SKU>?quantity=<new quantity>`

Body *None*

Response
`OK 200`

```
{
    "sku":"ASDFGHJK",
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1
}
```

### Remover um produto do carrinho
`DELETE /shopping-cart/<user-id>/items/<SKU>`

Body *None*

Response
`OK 200`

```
{
    "sku":"ASDFGHJK",
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1
}
```

### Recuperar um produto do carrinho de compra
`GET /shopping-cart/<user-id>/items/<SKU>`

Body *None*

Response
`OK 200`

```
{
    "sku":"ASDFGHJK",
    "price":"10.00",
    "name":"Bananas",
    "quantity": 1
}
```

### Recuperar o carrinho de compra
`GET /shopping-cart/<user-id>`

Body *None*

Response
`OK 200`

```
{
    "items": [
        {
            "sku":"ASDFGHJK",
            "price":"10.00",
            "name":"Bananas",
            "quantity": 1
        },
        {
            "sku":"ASDFGHJZ",
            "price":"20.00",
            "name":"Maçãs",
            "quantity": 2
        }
    ],
    "total":"50.00"
}
```

### Remover o carrinho de compra
`DELETE /shopping-cart/<user-id>`

Body *None*

Response
`OK 200`

```
{
    "items": [
        {
            "sku":"ASDFGHJK",
            "price":"10.00",
            "name":"Bananas",
            "quantity": 1
        },
        {
            "sku":"ASDFGHJZ",
            "price":"20.00",
            "name":"Maçãs",
            "quantity": 2
        }
    ],
    "total":"50.00"
}
```

### Error message

Response
Any **4XX** or **5XX** errors
```
{
    "resource":"<resource name>",
    "error_key":"<error type key>",
    "message":"<error message>",
    "resource_key":"<resource id>"
}
```

**Ex:**
Response
`RESOURCE NOT FOUND 404`
```
{
    "resource":"product",
    "error_key":"product.not.found",
    "message":"There is no product on shopping cart for the given SKU.",
    "resource_key":"ASDFGHJK"
}
```

## Passos para entrega do challenge

1. Dar fork neste repositório.
2. Implementar desafio.
4. Propor um pull request.


## Extras

Caso consigam completar os requisitos aqui estabelecidos e se sintam confortáveis em ir um pouco além, podem ficar à vontade em acrescentar qualquer melhoria além destes. Como por exemplo:

* Testes de Unidade
* Docker
* Logs
* API Doc (Swagger Open API)
* Autenticação
* Qualquer lib ou framework adicional
* Testes de componente (API)

## Instruções de uso

### Dependencies:

- Spring Web WEB 
- Spring Data JPA SQL
- MySQL Driver SQL
- Spring Data Elastic Search NOSQL 
- Swagger

### Aplication yml:

Url=jdbc:mysql://localhost:3306/sys?useSSL=false&allowPublicKeyRetrieval=true
Username=Bianka
Password=Invillia
driver-class-name: com.mysql.cj.jdbc.Driver
server.port=8080


### Docker - MySQL:
 cmd
docker ps --name mysql-shopping_cart -e MYSQL_DATABASE=shopping-cart -e MYSQL_USER=Bianka -e MYSQL_ROOT_PASSWORD=Invillia -d -p 3306:3306 mysql:latest

### Swagger

Para acessar o Swagger:

http://localhost:8080/swagger-ui.html


### Executar:
   cmd
./gradlew bootRun

- Depois de executado:
  - Docker do MySQL roda na porta `3306`
  - Aplicação roda na porta `8080`