# Horário de Atendimento do Professor

* Terças e quintas das 8h às 16h, exceto em janelas nas quais reunião extraordinárias acontecem. As janelas são de até 1h.
* Demais dias da semana, estou no Slack, com tempo de respostas no mesmo dia.

# Horário de Atendimento do Monitor

* Segunda: 8h30 às 10h
* Quarta: 8h30 às 10h
* Sexta: 8h30 às 9h30

# Banco de Dados III - Joins


## Definição

**Join** é uma operação que combina linhas de duas ou mais tabelas com base em uma condição relacionada entre elas. 

Essa condição é especificada na cláusula ON ou usando a cláusula WHERE.


## Quando usar?

Quando você tem dados distribuídos em várias tabelas e precisa consultar informações (fazer um **SELECT**) combinadas dessas tabelas.

## No seu projeto

Por exemplo, suponha que você tenha uma tabela de pedidos de produção de notebooks que pode ser enviado à linha de produção. E você tem uma tabela de manuais de notebooks.

* **Vou manter o português para facilitar o entendimento, mas depois a gente traduz os trem.**

### Planilha pedidos

| id_pedido | quant_pedido | linha_producao | modelo |
|----------|----------|----------|----------|
| 1        |  100     | azul     | A        |
| 2        |  200     | laranja  | B        |
| 3        |  300     | verde    | C        |
| 4        |  400     | vermelho | D        |


### Planilha notebooks

Nessa planilha de Pedidos, tem-se os pedidos identificados de 1 a 4, mas apenas os clientes 1, 2 e 4 consumiram algum valor.

| id_notebook | url_manual | fk_id_pedido |
|----------|----------|----------|
| 1        | https://res.cloudinary.com/inteli/image/123.jpg | 1 |
| 2        | https://res.cloudinary.com/inteli/image/321.jpg | 2 |
| 3        | https://res.cloudinary.com/inteli/image/30.jpg  | 3 |
| 4        | https://res.cloudinary.com/inteli/image/10.jpg  | 4 |


Se aplicar **INNER JOIN** (JUNÇÃO INTERNA) para combinar as informações de **pedidos** com os **notebooks**, o resultado será a junção interna de tudo o que está referenciado de forma correta entre as tabelas **pedidos** e **notebooks**. Veja:

| id_pedido | quant_pedido | linha_producao | modelo | id_notebook | url_manual | fk_id_pedido |
|----------|----------|----------|----------|----------|----------|----------|
| 1        |  100     | azul     | A | 1 | https://res.cloudinary.com/inteli/image/123.jpg | 1 |
| 2        |  200     | laranja  | B | 2 | https://res.cloudinary.com/inteli/image/321.jpg | 2 |
| 3        |  300     | verde    | C | 3 | https://res.cloudinary.com/inteli/image/30.jpg  | 3 |
| 4        |  400     | vermelho | D | 4 | https://res.cloudinary.com/inteli/image/10.jpg  | 4 |




## Tipos de Join

Os joins mais usados são:

* INNER JOIN --> retorna linhas que têm valores correspondentes em ambas as tabelas.
* LEFT JOIN --> retorna linhas da tabela da esquerda e as linhas correspondentes da tabela da direita. Se não houver correspondência, os valores NULL são retornados da tabela da direita.
* RIGHT JOIN --> retorna as linhas da tabela da direita e as linhas correspondentes da tabela da esquerda. Se não houver correspondência, os valores NULL são retornados da tabela da esquerda.
* FULL JOIN --> retorna linhas quando há uma correspondência em uma das tabelas. As colunas da outra tabela terão valores NULL quando não houver correspondência.
* CROSS JOIN --> combina cada linha de uma tabela com todas as linhas da outra tabela, resultando em tabela A * tabela B. Cuidado que esse comando pode retornar um grande volume de dados.
* Self JOIN --> une uma tabela a si mesma, permitindo consultas hierárquicas ou aninhadas.
* UNION JOIN --> combina os resultados de duas ou mais consultas em um único conjunto de resultados.
* EXCEPT JOIN --> retorna as linhas de uma tabela que não estão presentes em outra tabela.
* INTERSECT JOIN --> retorna as linhas que estão presentes em ambas as tabelas.


### Planilha Clientes

| id_customer | name | country |
|----------|----------|----------|
| 1   | João   | Brasil   |
| 2   | Pedro   | Chile   |
| 3   | Rafael |   França |
| 4   | Ana   | EUA   |


### Planilha Pedidos

Nessa planilha de Pedidos, tem-se os pedidos identificados de 1 a 4, mas apenas os clientes 1, 2 e 4 consumiram algum valor.

| id_order | id_customer  | value |
|----------|----------|----------|
| 1        | 1        | 100      |
| 2        | 4        | 200      |
| 3        | 2        | 150      |
| 4        | 2        | 300      |


Se aplicar **INNER JOIN** para combinar as informações de **Clientes** com os **Pedidos**, o resultado será:

Em outra palavras, vamos selecionar o **id_customer**, **name** e **country** da tabela "Clientes", bem como o **id_order** e **value** da tabela **Pedidos**, combinando os registros onde o **id_customer** é igual em ambas as tabelas.

| id_customer | name  | country  | id_order | value |
|----------|----------|----------|----------|----------|
| 1        | João     | Brasil   |  1       | 100      |
| 2        | Pedro    | Chile    |  3       | 150      |
| 2        | Pedro    | Chile    |  4       | 300      |
| 4        | Ana      | EUA      |  2       | 200      |


Note que a coluna **id_customer** está em ordem crescente, e o JOIN INNER juntou as duas tabelas **Clientes** e **Pedidos**.

### Tabela Clientes

**Primary key =** id_customer

### Tabela Pedidos

**Primary key =** id_order

**Foreign key** = id_customer

```
SELECT Clientes.id_customer, Clientes.name, Clientes.country, Pedidos.id_order, Pedidos.value
FROM Clientes
INNER JOIN Pedidos ON Clientes.id_customer = Pedidos.id_customer;
```

## Paralelo com o Excel

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03a/blob/main/imgs/desespero.jpg">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03a/blob/main/imgs/desespero.jpg)">
</picture>

