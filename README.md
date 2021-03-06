# postgresql

<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" width="180" height="180" />

## Introdução

Nesse repositório esterei explicando o que é o **PostgreSQL**, mas antes de entrar nesse assunto, é preciso entender o que é um banco de dados. Como o próprio nome já diz, um banco da dados é um ambiente no qual se armazena dados, mas muito além disso, é possível realizar diversas operações com esses dados, utilizando a linguagem **SQL** (*Structured Query Language*), uma das linguagens mais famosas, de fácil entendimento e muito poderosa. Nesse caso, os dados são armazenados em tabelas, formadas por linhas, colunas e identificadores, ou seja, de uma forma relacional (no qual diferentes tabelas podem ter relações entre si).

**PostgreSQL** é um dos gerenciadores de bancos de dados mais utilizados em todo o mundo, sua fama deve-se ao fato de ser *open source*, robusto, possuir alta performance (lida bem com grandes quantidades de solicitações) e pela sua alta compatibilidade com diferentes padrões de linguagem. **PostgreSQL** usa, como sua linguagem principal, **SQL** e é com essa linguagem que realizamos as operações envolvendo os bancos de dados.

## Instalação

## psql

Nesse tutorial, não usaremos nenhuma interface gráfica para operar com os dados, e sim o `psql`, ou seja, realizaremos todos os comandos pelo terminal do **PostgreSQL**, os comandos são os mesmos para os diferentes sistemas operacionais.

![image](https://user-images.githubusercontent.com/86558706/148416826-21720130-ee92-4e64-973d-05966ddd7b30.png)

## Lista de comandos e dos bancos de dados

Para obter a lista completa dos comandos, digite `\?`. Note que os comandos começam com `\`. Veja também o `-- Mais  --` no final, intuitivamente com a tecla `Enter` você pode expandir a lista de comandos.

```console
postgres=# \?
General
  \copyright             show PostgreSQL usage and distribution terms
  \crosstabview [COLUMNS] execute query and display results in crosstab
  \errverbose            show most recent error message at maximum verbosity
  \g [(OPTIONS)] [FILE]  execute query (and send results to file or |pipe);
                         \g with no arguments is equivalent to a semicolon
  \gdesc                 describe result of query, without executing it
  \gexec                 execute query, then execute each value in its result
  \gset [PREFIX]         execute query and store results in psql variables
  \gx [(OPTIONS)] [FILE] as \g, but forces expanded output mode
  \q                     quit psql
  \watch [SEC]           execute query every SEC seconds

Help
  \? [commands]          show help on backslash commands
  \? options             show help on psql command-line options
  \? variables           show help on special variables
  \h [NAME]              help on syntax of SQL commands, * for all commands
-- Mais  --
```

Para obter a lista dos seus bancos de dados digite `\l`, note que alguns, por padrão, já aparecem.

```console
postgres=# \l
                                             List of databases
   Name    |  Owner   | Encoding |        Collate         |         Ctype          |   Access privileges
-----------+----------+----------+------------------------+------------------------+-----------------------
 postgres  | postgres | UTF8     | Portuguese_Brazil.1252 | Portuguese_Brazil.1252 |
 template0 | postgres | UTF8     | Portuguese_Brazil.1252 | Portuguese_Brazil.1252 | =c/postgres          +
           |          |          |                        |                        | postgres=CTc/postgres
 template1 | postgres | UTF8     | Portuguese_Brazil.1252 | Portuguese_Brazil.1252 | =c/postgres          +
           |          |          |                        |                        | postgres=CTc/postgres
(3 rows)
```

## Criando e se conectando a um novo banco de dados

Para criar um novo banco de dados, use o comando `CREATE DEATABASE mydatabase;`, (os comandos não são *case sensitive*, ou seja, você pode tanto digitar em maiúsculo quando minúsculo, mas para uma melhor diferenciação entre comandos do terminal e da linguagem **SQL**, optarei pelas letras maiúsculas ao executar comandos **SQL**).

```console
postgres=# CREATE DATABASE mydatabase;
CREATE DATABASE
```

Agora digite `\l` e veja a lista de bancos de dados novamente.

Para se conectar a um novo banco de dados é muito simples, basta digitar `\c mydatabase`, no caso `mydatabase` é o banco de dados que acabei de criar.

```console
postgres-# \c mydatabase
You are now connected to database "mydatabase" as user "postgres".
```

## Excluindo um banco de dados

Para deletar um banco de dados basta simplesmente digitar `DROP DEATABASE mydatabase;`. Criando e deletando um banco de dados:

```console
mydatabase=# CREATE DATABASE test;
CREATE DATABASE
mydatabase=# DROP DATABASE test;
DROP DATABASE
```

Tenha cuidado pois essa ação é irreversível, ou seja, uma vez deletado, você nunca mais poderá recuperá-lo. Por isso é sempre importante realizar back-ups regularmente dos seus dados.

## Criando tabelas de dados

Para criar uma nova tabela no seu banco de dados, você deve utilizar o comando `CREATE TABLE` seguido do nome, e como argumentos, o nome da coluna seguido do tipo de dado. Veja o exemplo a seguir para um melhor entendimento:

```console
mydatabase=# CREATE TABLE person(
mydatabase(#    id INT,
mydatabase(#    name VARCHAR(50),
mydatabase(#    birth DATE
mydatabase(# );
CREATE TABLE
```

A partir do momento que você abre o parênteses e aperta `Enter`, o comando não será executado até que você feche o parênteses inicial.

Observe a tabela abaixo.

![image](https://user-images.githubusercontent.com/86558706/150802419-2a3111dd-0459-4567-910c-8cc4734a7560.png)

## Verificando as tabelas de dados

Para verificar todas as tableas de dados em seu banco de dados, use o comando `\d`, a letra `d` vem da palavra *describe* (em portugês, descrever).

```console
mydatabase=# \d
         List of relations
 Schema |  Name  | Type  |  Owner
--------+--------+-------+----------
 public | person | table | postgres
(1 row)
```

Para detalhar alguma tabela, repita o comando anterior e em seguida digite o nome da tabela.

```console
mydatabase=# \d person
                      Table "public.person"
 Column |         Type          | Collation | Nullable | Default
--------+-----------------------+-----------+----------+---------
 id     | integer               |           |          |
 name   | character varying(50) |           |          |
 birth  | date                  |           |          |
```
