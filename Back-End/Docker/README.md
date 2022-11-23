# Docker quick  commands

![Docker](https://raw.githubusercontent.com/ederssouza/docker-quick-commands/master/images/docker.png)

## Get Started

For more informations [access the official documentation](https://docs.docker.com/get-started/).

## Installation

- [Install Docker for Mac](https://docs.docker.com/docker-for-mac/install/)
- [Get Docker CE for Ubuntu](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
- [Install Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

## Commands

###   Ver comandos disponíveis
```js
docker --help
```
###   Criar um container

```js
  docker run
```
###   Listar containers
```js
docker -v
```

###   Listar containers no Docker
```js
docker ps -a
```
```js
docker container ps -a 
```
```js
docker container ls -a
```
```js
docker container list -a
```

###  Criando um container sem executar
```js
  docker create -it 
```
```js
  docker start 
```
### Entrando em um container já em execução 
```js
  docker container attach 
```

### Criando contêiner em segundo plano
```js
  docker container run -tid ubuntu
```
### Parando um contêiner
```js
  docker stop
```
### Iniciando um contêiner parado
```js
  docker start 
```
### Reiniciar contêiner 
```js
  docker restart 
```
### Pausar um contêiner
```js
  docker pause 
```
### "Despausar" um contêiner
```js
  docker unpause 
```
### Remover contêiner 
```js
  docker rm 
```
### Remove contêiner parados
```js
  docker container prune
```

```js
  docker rm $(docker ps -a -q)
```
### Remove Todos os contêiner ( parados ou não )
```js
  docker rm -f $(docker ps -aq) 
```
   Obs: -f: força remoção dos em execução
   -q: não mostar o retorno da lista, apenas ID

### Remove image

```bash
$ docker rmi REPOSITORY_NAME
```
   

### Remove Todos as imagens
```js
  docker rmi $(docker images -q)
```
   -q: não mostar o retorno da lista, apenas ID
   
   
