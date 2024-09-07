# docker
Comandos e curiosidades importantes sobre docker

### Comandos

Ver os containers que estão rodando: ```docker ps```<br>

Ver containers existentes: ```docker ps -a```<br>

Deletar um container: ```docker rm <3 primeiros nºs do container>```<br>

Parar a execução de um container: ```docker stop <3 primeiros nºs do container>```<br>

Rodar um container Ubuntu, sem levantar ele: ```docker run -it ubuntu bash```<br>

Subir o container: ```docker start <3 primeiros nºs do container>```<br>

Acessar o container via CLI: ```docker exec -it 9e7 /bin/bash```<br>
    exec-> executar o comando em um container que já está em execução<br>
    -it -> interagir com o terminal desse container<br>

<br>

### Docker file

<br>

### Docker Compose
Quando vou trabalhar com múltiplos containers

