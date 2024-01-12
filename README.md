# Curso_mongoDB

## Comandos para inserir dados em uma tabela

+ db.series.insertOne() -- serve para inserie apenas 

## Filtragem de dados

Podemos filtrar por varios tipos de formas e algumas delas são:

+ Filter -- Retorna os dados que satisfação uma determinada consição

+ Project -- uma projeção retorna alguns campos determinados em uma consulta como: 
`` {"Série": 1, "Classificação": 1}``

+ Sort -- Retornas os documentos de forma ordenada de uma coleção. Ele pode ser retornado de foma       crescente ou decrescente apenas informando um número, 1 ou -1
```{"Série": -1}```

+ Collation -- Podemos especificar regras de idiômas para a copmparação de strings e caracteres especiais. 


## Operadores no mongoDb

Exemplo de como podemos implementar as consultas:

``{$and:[{"Ano de lançamento": 2018}, {"Classificação": "18+"}]}``

+ $eq --  Corresponde a valores iguais a um valor especificado.
+ $gt --  Corresponde a valores maiores que um valor especificado.
+ $gte --  Corresponde a valores maiores ou iguais a um valor especificado.
+ $in --  Corresponde a qualquer um dos valores especificados em uma matriz.
+ $lt --  Corresponde a valores menores que um valor especificado.
+ $lte --  Corresponde a valores menores ou iguais a um valor especificado.
+ $ne --  Corresponde a todos os valores que não são iguais a um valor especificado.
+ $nin --  Não corresponde a nenhum dos valores especificados em uma matriz.

## Criando consultas no MongoDb pelo terminal





