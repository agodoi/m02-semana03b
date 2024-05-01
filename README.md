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

* INNER JOIN --> retorna registros que têm valores correspondentes em ambas as tabelas.
* LEFT JOIN --> retorna todos os registros da tabela da esquerda e os registros correspondentes da tabela da direita. Se não houver correspondência, os valores NULL são retornados da tabela da direita.
* RIGHT JOIN --> retorna todos os registros da tabela da direita e os registros correspondentes da tabela da esquerda. Se não houver correspondência, os valores NULL são retornados da tabela da esquerda.
* FULL JOIN --> retorna todos os registros quando há uma correspondência em uma das tabelas. As colunas da outra tabela terão valores NULL quando não houver correspondência.



<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03a/blob/main/imgs/desespero.jpg">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03a/blob/main/imgs/desespero.jpg)">
</picture>

