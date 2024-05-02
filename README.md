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

Nessa planilha **pedidos** tem-se a identificação de cada pedido pelo **id_pedidos**, a quantidade de notebooks a serem produzidos em **quant_pedidos**, qual a cor da linha de produção em **linha_producao** que será produzido e o modelo de notebook que entrará em produção em **modelo_notebook**.

| id_pedido | quant_pedido | linha_producao | modelo_notebook |
|----------|----------|----------|----------|
| 1        |  100     | azul     | A        |
| 2        |  200     | laranja  | B        |
| 3        |  300     | verde    | C        |


### Planilha notebooks

Nessa planilha de notebooks, tem-se as respectivas URL com fotos dos notebooks de 1 a 4.

| id_notebook | url_manual | pedido_id |
|----------|----------|----------|
| 2        | https://res.cloudinary.com/inteli/image/321.jpg | 2 |
| 3        | https://res.cloudinary.com/inteli/image/30.jpg  | 3 |
| 4        | https://res.cloudinary.com/inteli/image/10.jpg  | 4 |


Se aplicar **INNER JOIN** (JUNÇÃO INTERNA) para combinar as informações de **pedidos** com os **notebooks**, o resultado será a junção interna de tudo o que está referenciado de forma correta entre as tabelas **pedidos** e **notebooks**. Veja:

| id_pedido | quant_pedido | linha_producao | modelo | id_notebook | url_manual | fk_id_pedido |
|----------|----------|----------|----------|----------|----------|----------|
| 2        |  200     | laranja  | B | 2 | https://res.cloudinary.com/inteli/image/321.jpg | 2 |
| 3        |  300     | verde    | C | 3 | https://res.cloudinary.com/inteli/image/30.jpg  | 3 |

Nesse caso, os itens 2 e 3 estão corretamente referenciados, logo, aparecerão como resultado do INNER JOIN porque ele retorna linhas que têm valores correspondentes em ambas as tabelas.


## Outros Join

* LEFT JOIN --> retorna linhas da tabela da esquerda e as linhas correspondentes da tabela da direita. Se não houver correspondência, os valores NULL são retornados da tabela da direita.
* RIGHT JOIN --> retorna as linhas da tabela da direita e as linhas correspondentes da tabela da esquerda. Se não houver correspondência, os valores NULL são retornados da tabela da esquerda.
* FULL JOIN --> retorna linhas quando há uma correspondência em uma das tabelas. As colunas da outra tabela terão valores NULL quando não houver correspondência.


<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/joins.jpg">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/joins.jpg)">
</picture>


```
DROP TABLE IF EXISTS pessoasHerois CASCADE;

create table pessoasHerois(
id SERIAL primary key,
cpf VARCHAR(11) not null,
nome VARCHAR(50) not null,
sobrenome VARCHAR(50) not null,
idade VARCHAR(50) null
);

DROP TABLE IF EXISTS caracteristicas CASCADE;

create table caracteristicas(
id SERIAL primary key,
funcao VARCHAR(50) not null,
acessorio VARCHAR(50) not null,
uniforme VARCHAR(50) null,
chaveForeign INT,
foreign key (chaveForeign) references pessoasHerois (id)
);


-- fazendo um CRUD (Create, Read, Update, Delete)

--Fazendo o Create
insert into pessoasHerois (cpf, nome, sobrenome, idade)
values 	('12345678900', 'Capitão', 'América', '32'),
		('00123456789', 'Tony', 'Stark', '39'),
		('98765432100', 'Nick', 'Fury', '55'),
		('54321678900', 'Thor', 'Deus do Trovão', '35'),
		('123456', 'Pantera', 'Negra', '40' );
	
insert into pessoasHerois (cpf, nome, sobrenome, idade)
values 	

insert into caracteristicas (funcao, acessorio, uniforme)
values 	('proteger', 'escudo', 'azul e vermelho'),
		('criar máquinas', 'robôs', 'vermelho'),
		('gerenciar', 'arma', 'preto'),
		('proteger', 'martelo', 'preto e vermelho'),
		('prot', 'mar', 'pre');
--note que não inserimos dado na chaveForeign key nesse insert
	
	
--serve para selecionar o nome Tony na tabela
select * from pessoasHerois where nome = 'Tony'

--serve para selecionar nomes com T na tabela
SELECT * FROM pessoasHerois WHERE nome LIKE 'T%'


--Fazendo o Delete da coluna 1
delete from pessoasHerois where id=1

-- serve para atualizar um item id da tabela
update pessoasHerois 
SET nome = 'Capitão'
WHERE id = 2


--atualizando as chaveForeigns que não foram contempladas no 
--insert original acima
UPDATE caracteristicas
SET chaveForeign = 1
WHERE id = 1;

UPDATE caracteristicas
SET chaveForeign = 2
WHERE id = 2;

UPDATE caracteristicas
SET chaveForeign = 3
WHERE id = 3;

UPDATE caracteristicas
SET chaveForeign = 4
WHERE id = 4;

SELECT pessoasHerois.nome, pessoasHerois.sobrenome, caracteristicas.acessorio, caracteristicas.uniforme
FROM pessoasHerois
INNER JOIN caracteristicas ON pessoasHerois.id = caracteristicas.chaveForeign;

SELECT pessoasHerois.nome, pessoasHerois.sobrenome, caracteristicas.acessorio, caracteristicas.uniforme
FROM pessoasHerois
LEFT JOIN caracteristicas ON pessoasHerois.id = caracteristicas.chaveForeign;

SELECT pessoasHerois.nome, pessoasHerois.sobrenome, caracteristicas.acessorio, caracteristicas.uniforme
FROM pessoasHerois
RIGHT JOIN caracteristicas ON pessoasHerois.id = caracteristicas.chaveForeign;

SELECT pessoasHerois.nome, pessoasHerois.sobrenome, caracteristicas.acessorio, caracteristicas.uniforme
FROM pessoasHerois
FULL JOIN caracteristicas ON pessoasHerois.id = caracteristicas.chaveForeign;
```

## Consulta mais complexa


```
SELECT 
    t.nome AS TutorName,
    t.idade AS TutorAge,
    t.endereco AS TutorAddress,
    d.raca AS DogBreed,
    d.idade AS DogAge
FROM tutor t
INNER JOIN dog d ON t.id = d.tutor_id
WHERE t.idade > 25 AND d.raca = 'Labrador'
ORDER BY t.idade DESC, d.idade ASC;
```

* SELECT: Indica que estamos selecionando colunas específicas da consulta.
	* t.nome AS TutorName: estamos selecionando o nome do tutor da tabela tutor e renomeando-o como TutorName.
 	* t.idade AS TutorAge: estamos selecionando a idade do tutor da tabela tutor e renomeando-a como TutorAge.
  	* t.endereco AS TutorAddress: estamos selecionando o endereço do tutor da tabela tutor e renomeando-o como TutorAddress.
  	* d.raca AS DogBreed: estamos selecionando a raça do cachorro da tabela dog e renomeando-a como DogBreed.
  	* d.idade AS DogAge: estamos selecionando a idade do cachorro da tabela dog e renomeando-a como DogAge.

```
FROM tutor t
INNER JOIN dog d ON t.id = d.tutor_id
```

* FROM: indica as tabelas de onde estamos selecionando os dados.
* tutor t: estamos selecionando dados da tabela tutor e atribuindo um alias t para ela.
* dog d: estamos selecionando dados da tabela dog e atribuindo um alias d para ela.
* INNER JOIN: estamos fazendo uma junção interna entre as tabelas tutor e dog, usando a condição de que o id na tabela tutor deve ser igual ao tutor_id na tabela dog.

```
WHERE t.idade > 25 AND d.raca = 'Labrador'
```

* WHERE: estamos filtrando os resultados com base em algumas condições.
* t.idade > 25: estamos selecionando apenas os registros onde a idade do tutor é maior que 25.
* d.raca = 'Labrador': estamos selecionando apenas os registros onde a raça do cachorro é "Labrador".

```
ORDER BY t.idade DESC, d.idade ASC;
```

* ORDER BY: estamos ordenando os resultados.
* t.idade DESC: estamos ordenando a idade do tutor em ordem decrescente (do maior para o menor).
* d.idade ASC: estamos ordenando a idade do cachorro em ordem crescente (do menor para o maior).


## Conectando seu Render no Sails

Vamos criar uma aplicação Sails do tipo WebApp e conectar o seu banco de dados que está no [https://dashboard.render.com/](https://dashboard.render.com/)

### Etapa 1 - Criando um novo projeto Sails

1.1) Abra um terminal CMD, e digite ```sail new projetoDell``` e escolha **1. Web App** e aguarde alguns minutinhos para instalar as dependências;

1.2) Entre na pasta do seu **projetoDell** e digite ```code .``` para que essa pasta seja aberta no seu Visual Code;


<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_criado_zero.png">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_criado_zero.png)">
</picture>

1.3) Na raiz da pasta, clique no arquivo **package.json** (penúltimo arquivo do menu vertical da esquerda). Aí dentro tem todas as dependências. Como estamos trabalhando com o **PostgreSQL**, não há pacotes default para ele. Então temos, que puxar manualmente. Então, digite **sails postgresql** no Google, e você vai cair nesse site [https://www.npmjs.com/package/sails-postgresql](https://www.npmjs.com/package/sails-postgresql)

1.4) Para instalar a biblioteca do **PostgreSQL no terminal, digite esse comando ```npm i sails-postgresql```. Quando terminar, vá no arquivo **package.json** que você vai encontrar o que a seta vermelha está apontando.

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_com_postgresql.png">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_com_postgresql.png)">
</picture>

1.5) Dê um ```npm install``` na raiz do seu projeto Sails para garantir que todas as instâncias foram baixadas e instaladas no PC.

1.6) Entre no seu [https://dashboard.render.com/](https://dashboard.render.com/) com a sua conta particular, e clique no botão **Connect** no canto direito superior e vá na aba **External Connection** e pegue a URL do campo **Connect from services outside of Render**. Usa URL é aquela que possui o nome do host, senha, banco de dados, etc. Copia e cola isso em um canto do seu computador.

1.7) Vamos preparar a conexão do seu banco através do Sails. Vá na seguinte pasta do seu projeto Sails:
* **Config** (onde ficam as conexões)
	* **datastores.js** (são as suas conexões de qualquer banco, tipo MySQL, PostgreSQL, etc)
 		* **linha 51** onde tem ```// adapter: 'sails-mysql',```, **apague** e substitua por ```adapter: 'sails-postgresql',``` sem as // barras
   		* **linha 52** adicione ```url: 'postgres://bdgodoi_user:ZmTVzKJXGWyB65nRGeW7S2AkMUEI3gZ1@dpg-cojpieu3e1ms73bflb6g-a.oregon-postgres.render.com/bdgodoi',```
       		* **linha 53** adicione ```ssl: true```

  
<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_datastores.png">
   <img alt="DataStores" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_datastores.png)">
</picture>


1.8) Vá na pasta para você conhecer as tabelas (emailAddress, emailStatus, emailChangeCandidate, etc) padrões que o Sails vai criar no seu banco de dados no Render:

* **api**
	* **models**
 		* **User.js** 

1.9) Volte no terminal CMD e digite **sails lift** [enter] e aguarde **info: Starting app...** Se der pau, execute novamente **sails lift**. Esse comando faz criar as entidadades descritas em user.js. Em outras palavras, as tabelas do **user.js** são criadas no seu Render.

1.10) Se você chegou nessa tela abaixo, então você teve sucesso na sua conexão do Render através do Sails.

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_conexao_ok.png">
   <img alt="Sails ok" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_conexao_ok.png)">
</picture>

1.11) Vá no seu DBeaver, atualize seu banco e procure pela tabela **user**. Se você estiver vendo essa tabela, **PARABÉNS**. Merece um Bis. Essa frase está sem destaque, então vá na mesa do prof sutilmente e pegue o seu Bis sem comentar com ninguém. Quem não for buscar o seu Bis, pode ser seu no final...

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/dbeaver_comprovando_user.png">
   <img alt="DBeaver" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/dbeaver_comprovando_user.png)">
</picture>

## Conclusões

No seu projeto, cabe o INNER e o LEFT.

INNER para juntar duas tabelas totalmente lisas e referenciadas sem problemas.

LEFT serveria para vc emitir um relatório entre as tabela **pedidos** e **notebooks** e o que vier **NULL** na tabela **notebooks** siginfica que são manuais sem referência, perdidos ou obsoletos no seu banco de dados.

Vamos criar uma situação hipotética onde a empresa DELL fabrica três modelos diferentes de notebooks: Inspiron, XPS e Alienware. Cada modelo tem seus próprios manuais de produção, e queremos usar um full join para visualizar quais manuais devem ser acessados para produzir cada modelo de notebook.

Considere as seguintes tabelas:

**Tabela notebooks:**

* id: identificador único do modelo de notebook.
* modelo: nome do modelo de notebook.

**Tabela manuais:**

* id: identificador único do manual.
* modelo_id: identificador do modelo de notebook associado ao manual.
* nome: nome do manual.

```
-- Criar a tabela notebooks
CREATE TABLE notebooks (
    id SERIAL PRIMARY KEY,
    modelo VARCHAR(50)
);

-- Popular a tabela notebooks
INSERT INTO notebooks (modelo) VALUES
(1, 'Inspiron'),
(2, 'XPS'),
(3, 'Alienware');

-- Criar a tabela manuais
CREATE TABLE manuais (
    id SERIAL PRIMARY KEY,
    modelo_id INTEGER REFERENCES notebooks(id),
    nome VARCHAR(100)
);

-- Popular a tabela manuais
INSERT INTO manuais (modelo_id, nome) VALUES
(1, 'Manual de Produção do Inspiron'),
(2, 'Manual de Produção do XPS'),
(3, 'Manual de Produção do Alienware'),
(1, 'Guia de Montagem do Inspiron'),
(2, 'Guia de Montagem do XPS');

```

Agora, podemos usar um full join para visualizar quais manuais estão disponíveis para cada modelo de notebook:

```
SELECT n.modelo, m.nome
FROM notebooks n
FULL JOIN manuais m ON n.id = m.modelo_id
ORDER BY n.modelo, m.nome;
```

Esta consulta SQL irá retornar todos os manuais associados a cada modelo de notebook, incluindo aqueles que não têm um manual correspondente (ou seja, modelos de notebook para os quais não há manual). Isso nos dará uma visão completa de quais manuais devem ser acessados na linha de produção para produzir cada modelo de notebook.

