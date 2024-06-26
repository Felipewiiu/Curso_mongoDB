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

db.custumers.updateMany({_id: ObjectId("6668ec8e09b44e848ecdcdf6")}, {$set: {idade: 999}})

````

## Removendo um campo existente em um documento

Para se remover um campo de um documento basta utilizar o operador ``$unset``

````ecmascript 6

db.custumers.updateMany({_id: ObjectId("6668ec8e09b44e848ecdcdf6")}, {$unset: {idade: 999}})

````

## Encontrando valores em um intervalo

Para se encontrar valores em intervalos basta usar o operador ``$in`` como no exemplo abaixo:

````ecmascript 6
E - comerce > db.custumers.find({idade: {$in: [5, 33]}})

````

# MongoDB Aggregation Pipeline

O MongoDB oferece operações de agregação que processam dados de várias formas para retornar resultados computados. A
agregação permite transformar e analisar dados em uma coleção para obter estatísticas, relatórios, resumos ou outras
formas de dados agregados. A principal ferramenta para realizar essas operações no MongoDB é o **pipeline de agregação
**.

## Pipeline de Agregação

Um pipeline de agregação consiste em uma sequência de estágios, onde cada estágio executa uma operação nos documentos de
entrada e passa os resultados para o próximo estágio. Os estágios podem filtrar, projetar, agrupar, ordenar, juntar e
realizar outras transformações nos dados.

### Principais Estágios do Pipeline de Agregação

1. **`$match`**: Filtra documentos com base em critérios especificados, semelhante à cláusula `WHERE` em SQL.
   ```javascript
   db.orders.aggregate([
       { $match: { status: "shipped" } }
   ])

````ecmascript 6
E - comerce > db.custumers.aggregate([{$group: {_id: "$by_user", num_tutorial: {$max: "$likes"}}}])

````

## Adicionando atributos dentro de um array

````ecmascript 6
E - comerce > db.custumers.aggregate([{$group: {_id: "$nome", colecao_idade: {$push: "$idade"}}}])
````

## Fazendo um JOIN no mongosh (lookup)

O operador $lookup no MongoDB é usado para realizar operações de junção (join) entre duas coleções, semelhante a uma
junção em SQL. Ele permite que você combine dados de diferentes coleções em um único conjunto de resultados. No
mongosh (shell interativo do MongoDB), você pode usar o $lookup dentro do aggregate pipeline para realizar essas
operações.

````ecmascript 6
db.coleção1.aggregate([
    {
        $lookup: {
            from: "<coleção2>",
            localField: "<campo1>",
            foreignField: "<campo2>",
            as: "<nome_do_campo_resultante>"
        }
    }
])

````

## Criando uma projeção com $project

O operador $project no MongoDB é usado dentro de um pipeline de agregação para incluir, excluir ou renomear campos em
documentos de saída. Ele permite transformar os documentos de uma coleção, criando uma estrutura personalizada para os
resultados.

**Estrutura Básica do $project**
A estrutura básica do $project é a seguinte:

````ecmascript 6
db.coleção.aggregate([
    {
        $project: {
            "<campo1>": "<expressão>",
            " <campo2>": "<expressão>",
            ...
        }
    }
])

db.orders.aggregate([
    {
        $project: {
            orderId: 1,
            productId: 1,
            quantity: 1
        }
    }
])


````

## Criando uma projeção com $match

O operador $match no MongoDB é usado para filtrar documentos em um pipeline de agregação, semelhante à cláusula WHERE em
SQL. Ele permite selecionar apenas os documentos que atendem a critérios específicos, reduzindo o conjunto de dados
antes de aplicar outras operações no pipeline.

````ecmascript 6
db.orders.aggregate([
    {
        $match: {productId: 101}
    }
])

````



