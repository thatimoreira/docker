# docker
Comandos e curiosidades importantes sobre docker, além de resumo do curso "[Descomplicando o Docker](https://www.youtube.com/watch?v=Wm99C_f7Kxw&list=PLf-O3X2-mxDn1VpyU2q3fuI6YYeIWp5rR&index=1)" da LinuxTips, separado em capítulos (acesse através do índice abaixo).

<br>


# Índice Geral

1. [Capítulo I: O que são Containers](capitulos/capitulo01-O_que_sao_Containers.md)
   - [Definição](capitulos/capitulo01-O_que_sao_Containers.md#definicao)
   - [Tipos de Isolamento](capitulos/capitulo01-O_que_sao_Containers.md#tipos-de-isolamento)
   - [Mecanismos de Isolamento](capitulos/capitulo01-O_que_sao_Containers.md#mecanismos-de-isolamento)
   - [Importância dos Containers](capitulos/capitulo01-O_que_sao_Containers.md#importância-dos-containers)
   
2. [Capítulo II: O que é o Copy on Write](capitulos/capitulo02-O_que_e_o_Copy_on_Write.md)
   - [Definição](capitulos/capitulo02-O_que_e_o_Copy_on_Write.md#definicao)
   - [O que é Copy on Write?](capitulos/capitulo02-O_que_e_o_Copy_on_Write.md#o-que-e-copy-on-write?)
   - [Vantagens do Copy on Write](capitulos/capitulo02-O_que_e_o_Copy_on_Write.mdvantagens-do-copy-on-write)
   - [Práticas com Dockerfile](capitulos/capitulo02-O_que_e_o_Copy_on_Write.md#praticas-com-dockerfile)

   
3. [Capítulo III: Namespaces, cgroups e Netfilter](capitulos/capitulo03-Namespaces_cgroups_e_Netfilter.md)
   - [Namespaces](capitulos/capitulo03.md#namespaces)
   - [Cgroups](capitulos/capitulo03.md#cgroups)
   - [Netfilter](capitulos/capitulo03.md#netfilter)

4. [Capítulo IV: Um pouco de prática](capitulos/capitulo04-Um_pouco_de_pratica.md)
   - [Comandos básicos](capitulos/capitulo04.md#comandos-básicos)
   - [Criando um container](capitulos/capitulo04.md#criando-um-container)

5. [Capítulo V: Instalando o Docker](capitulos/capitulo05-Instalando_o_Docker.md)
   - [Requisitos para instalação](capitulos/capitulo05.md#requisitos-para-instalação)
   - [Passos para instalação](capitulos/capitulo05.md#passos-para-instalação)

...



--- 

### Comandos

Ver os containers que estão rodando: ```docker ps```<br>

Ver containers existentes: ```docker ps -a```<br>

Deletar um container: ```docker rm <3 primeiros nºs do container>```<br>

Parar a execução de um container: ```docker stop <3 primeiros nºs do container>```<br>

Rodar um container Ubuntu: ```docker run -it ubuntu bash```<br>

Subir o container: ```docker start <3 primeiros nºs do container>```<br>

Acessar o container via CLI: ```docker exec -it 9e7 /bin/bash```<br>
    exec-> executar o comando em um container que já está em execução<br>
    -it -> interagir com o terminal desse container<br>

<br>

### Docker file

<br>

### Docker Compose
Quando vou trabalhar com múltiplos containers

