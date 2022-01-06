# postgresql

## Introdução

Nesse repositório esterei explicando o **PostgreSQL**, mas antes de entrar no principal assunto, é preciso entender o que é um banco de dados: Como o próprio nome já diz, um banco da dados é um lugar no qual se armazena dados, mas muito além disso, é possível realizar diversas operações com esses dados, utilizando a linguagem **SQL** (*Structured Query Language*), uma linguagem de fácil entendimento e muito poderosa, nesse caso, os dados são armazenados em tabelas, formadas por linhas e colunas Então, de uma forma relacional (no qual diferentes tabelas podem ter relações entre elas).

**PostgreSQL** é um dos gerenciadores de bancos de dados mais utilizados em todo o mundo, sua fama deve-se ao fato de ser *open source*, robusto, possuir alta performance (lida bem com altos volumes de solicitações e com cargas de trabalho grandes) e pela sua alta compatibilidade com diferentes padrões de linguagem. **PostgreSQL** usa, como sua linguagem principal, **SQL** e é com essa linguagem que realizamos as operações envolvendo o banco de dados.

## Instalação

## psql

Nesse tutorial, não usaremos nenhuma interface gráfica para operar com os dados, e sim o `psql`, ou seja, realizaremos todaos os comandos pelo terminal do **PostgreSQL**, os comandos serão os mesmos para diferentes sistemas operacionais.

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

Para criar um novo banco de dados, use o comando `CREATE DEATABASE mydatabase;` (os comandos não são *case sensitive*, ou seja, você pode tanto digitar em maiúsculo quando minúsculo, mas para uma melhor diferenciação entre comandos do terminal e da linguagem **SQL**, optarei pelas letras maiúsculas ao executar comandos **SQL**).

```console
postgres=# CREATE DATABASE mydatabase;
CREATE DATABASE
```

Agora digite `\l` e veja a lista de bancos de dados novamente.

Para se conectar a um novo banco de dados é muito simples, basta digitar `\c mydatabase`, no caso `mydatabase` é o banco de dados que acabei de criar.

```console
postgres-# \c mydatabase
You are now connected to database "mydatabase" as user "postgres".
mydatabase-#
```

## Excluindo um banco de dados

