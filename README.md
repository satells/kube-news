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

a)Construir a imagem

docker build -t msergiost/kube-news:v1 .

b) logar com o docker hub

docker login

c) enviar imagem ao docker hub

docker push msergiost/kube-news:v1

fds
fds
d) enviar a latest

docker tag msergiost/kube-news:v1 msergiost/kube-news:latest

docker push msergiost/kube-news:latest

e) criar network tipo bridge

docker network create kube_news_net

docker network inspect kube_news_net

f) criar volume

docker volume create kube_news_vol

g) criar container postgres

docker container run -d -p 5432:5432 --name kube_news_db -e POSTGRES_PASSWORD=Pg123 -e POSTGRES_USER=kubenews -e POSTGRES_DB=kubenews --network kube_news_net --mount type=volume,source=kube_news_vol,target=/var/lib/postgresql/data postgres:12.17

O volume pode ser especificado de duas maneiras

1. -v kube_news_vol:/var/lib/postgresql/data

2. --mount type=volume,source=kube_news_vol,target=/var/lib/postgresql/data

h) criar container da aplicação

docker container run -d -p 8080:8080 --name kube_news -e DB_DATABASE=kubenews -e DB_USERNAME=kubenews -e DB_PASSWORD=Pg123 -e DB_HOST=kube_news_db --network kube_news_net msergiost/kube-news:v1

Docker Compose

docker compose up -d

docker compose up -d --remove-orphans

docker compose down

docker compose stop

docker compose start
