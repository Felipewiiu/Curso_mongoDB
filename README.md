# Curso_mongoDB

## Links de documentações

+ https://www.mongodb.com/docs/manual/tutorial/insert-documents/

## Comando para mostrar tabelas do banco de dados

+ show databases

## Comandos para inserir dados em uma tabela

+ db.series.insertOne() -- serve para inserie apenas

## Filtragem de dados

Podemos filtrar por varios tipos de formas e algumas delas são:

+ Filter -- Retorna os dados que satisfação uma determinada consição

+ Project -- uma projeção retorna alguns campos determinados em uma consulta como:
  `` {"Série": 1, "Classificação": 1}``

+ Sort -- Retornas os documentos de forma ordenada de uma coleção. Ele pode ser retornado de foma crescente ou
  decrescente apenas informando um número, 1 ou -1
  ```{"Série": -1}```

+ Collation -- Podemos especificar regras de idiômas para a copmparação de strings e caracteres especiais.

## Operadores no mongoDb

Exemplo de como podemos implementar as consultas:

``{$and:[{"Ano de lançamento": 2018}, {"Classificação": "18+"}]}``

+ $eq -- Corresponde a valores iguais a um valor especificado.
+ $gt -- Corresponde a valores maiores que um valor especificado.
+ $gte -- Corresponde a valores maiores ou iguais a um valor especificado.
+ $in -- Corresponde a qualquer um dos valores especificados em uma matriz(operador de comparação)[].
+ $lt -- Corresponde a valores menores que um valor especificado.
+ $lte -- Corresponde a valores menores ou iguais a um valor especificado.
+ $ne -- Corresponde a todos os valores que não são iguais a um valor especificado.
+ $nin -- Não corresponde a nenhum dos valores especificados em uma matriz.

## Criando consultas no MongoDb pelo terminal

+ Comando para puxar todos os campos: ```db.series.find()```

+ Comando para puxar apenas um campo: ```db.series.find({"Ano de lançamento": 2018})```

+ Comando para realizar uma projeção: ```db.series.find({}, "Série": 1, "Ano de lançamento": 1, "_id": 0)```

+ Comando para comparar valores: ```db.series.find({"Ano de lançamento": {$in: [2019, 2020]}})```

+ Comando para limitar o resultado de busca: ```db.series.find().limit(5)```

+ Comando para ordenação de elementos: ````db.series.find().sort({"Série": -1})```

+ Comando para retornar valores maiores ou igual a determinada condição:
  ``` db.series.find({"Temporadas disponíveis": {$gte: 4}})```

+ Comando que retorna valores diferentes do que especificao ``````

## Padrão de consulta

```
db.collection.find(query, projection)

```

+ **QUERY**: especificamos a condição que os nossos documentos devem atender para serem retornados na nossa consulta.

+ **PROJECTION**: especificamos quais campos devem ou não ser retornados na nossa consulta.

## Atualizando um campo pela linha de comando

Existem metodos para quue se possa estar atualizando um campo no documento e são eles:

+ **updateMany()** --> Atualiza vários documentos por vez

+ **updateOne()** --> Atualiza um documentos por vez


+ Comando para atualização de documentos:
  ```` db.series.updateOne({"Série": "Grimm"},{$set: {"Temporadas disponíveis": 8}})```
  usando o operador de atualização ($set)


+ comando para se atualizar mais de um objeto de uma vez:
  ```db.series.updateMany({"Série": {$in: ["Four More Shots Please", "Fleabag"]}}, {$set: {"Classificação": "18+"}})```

## Deletando um documento em uma coleção

Ao se deletar um documento é de suma importância que quando se usar o comando de deletar sempre especificar o filtro,
pois caso não seja passado, todos os documentos seram deletados da nossa coleção.

## Adicionando vários documento utilizando variável

Para se adicionar mais de um documento como um array de objetos basta usar o seguinte código:

````ecmascript 6

custArray = [{nome: "Lucas da chagas", idade: 31}, {nome: "Luanna patrocinio", idade: 25}]

db.custumers.insertMany(custArray);

````

## Busca no mongo usando expressões regulares

O mongo aceita regex como parâmetro de busca, como no exemplo:

````ecmascript 6

db.custumers.find({nome: /j/i});

````

## Regras importantes para atualização de documento

1. Se for preciso atualizar um documento apenas, comece usando o ``updateOne()`` ao envés de `replaceOne`, o operador
updateOne() vai te obrigar a usar operadores ao invés de um documento inteiro para a atualização o que é muito mais
seguro

2. Sempre que possível use a chave primária (_id), como filtro da atualização

3. Evite usar ``updateMany`` e outras formas de atualizar vários registros ao mesmo tempo

*Exemplo:*

````ecmascript 6

 db.custumers.updateMany({_id:ObjectId("6668ec8e09b44e848ecdcdf6") }, {$set: {idade: 999}})

````


## Removendo um campo exixtente em um documento

Para se remover um campo de um documento basta utilizar o operador ``$unset``

````ecmascript 6

 db.custumers.updateMany({_id:ObjectId("6668ec8e09b44e848ecdcdf6") }, {$unset: {idade: 999}})

````
