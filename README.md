# Projeto kube-news

### Objetivo

O projeto Kube-news é uma aplicação escrita em NodeJS e tem como objetivo ser uma aplicação de exemplo pra trabalhar com o uso de containers.

### Configuração

Pra configurar a aplicação, é preciso ter um banco de dados Postgre e pra definir o acesso ao banco, configure as variáveis de ambiente abaixo:

DB_DATABASE => Nome do banco de dados que vai ser usado.

DB_USERNAME => Usuário do banco de dados.

DB_PASSWORD => Senha do usuário do banco de dados.

DB_HOST => Endereço do banco de dados.

docker container run -d -p 5432:5432 --name postgres -e POSTGRES_PASSWORD=Pg123 -e POSTGRES_USER=kubenews -e POSTGRES_DB=kubenews -v kubenews_vol:/var/lib/postgresql/data postgres:14.10

DB_DATABASE=kubenews DB_USERNAME=kubenews DB_PASSWORD=Pg123 DB_HOST=192.168.56.101 node server.js
