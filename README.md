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

Quando você tem dados distribuídos em várias tabelas e precisa extrair informações combinadas dessas tabelas.

Por exemplo, suponha que você tenha uma tabela de clientes e outra de pedidos. Para obter informações sobre quais clientes fizeram quais pedidos, você precisa combinar os dados dessas duas tabelas usando JOIN.

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

| id_order | id_customer  | value |
|----------|----------|----------|
| 1        | 1        | 100      |
| 2        | 4        | 200      |
| 3        | 2        | 150      |
| 4        | 2        | 300      |


Se aplicar **INNER JOIN** para combinar as informações de clientes com os pedidos que cada cliente fez, o resultado será:

| id_customer | name  | country  | id_order | value |
|----------|----------|----------|----------|----------|
| 1      | João       | Brasil   |  1       | 100      |
| 2      | Pedro      | Chile    |  3       | 150      |
| 2      | Pedro      | Chile    |  4       | 300      |
| 4      | Ana        | EUA      |  2       | 200      |




<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03a/blob/main/imgs/desespero.jpg">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03a/blob/main/imgs/desespero.jpg)">
</picture>

