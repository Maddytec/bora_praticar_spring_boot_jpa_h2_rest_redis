# Ôooopáaaa Bora Praticar Spring Boot, JPA, H2, Rest, e Redis
Nesta pratica vamos adicionar em nossa API Cliente Base o banco de dados Redis, que é uma banco de dados
não relaciona de chave e valor.

Problematica:
Api com muitas requisições simultaneas que podem onerar o banco de dados relacional, sejam eles Mysql, PostgreSQL, Oracle entre outros.

Objetivo:
Adicionar o Redis ao nosso ecosistema. Desta forma, sugiro que abstraia outras soluções que você possa enchergar.

Passos:

1. Criar o arquivo redis-docker-compose.yml para disponibilizar o Redis:
- Diretório docker/redis-docker-compose.yml
```
version: '3'

services:
  redis:
    image: redis:latest
    ports:
      - "6379:6379"
```
- No console acessar o diretório onde o redis-docker-compose.yml foi criado e executar o comando:
``` 
docker-compose -f redis-docker-compose.yml up -d 
```
    
2. Adicionar as configurações do Redis no Projeto

- 2.1. Adicionar as Dependencias do Redis no pom.xml do projeto
```
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
- 2.2. Adicionar configuração de conexão com o Redis no application.yml do projeto
  ```
  spring:
    cache:
        type: redis
        redis:
            host: localhost
            port: 6379
  ```
3. Implementações
  - 3.1. Criar objeto ClienteRedis
  - 3.2. Criar interface ClienteRedisRepository
  - 3.3. Criar service ClienteRedisService
       -  Adicionar metodo salvar 
       -  Adicionar metodo consultar
