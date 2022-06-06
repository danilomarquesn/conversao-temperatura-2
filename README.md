# conversao-temperatura-2
Iniciativa Devops - Fabricio Veronez - Kube Dev

* Rodar Gerenciador de Pacotes: NPM 

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ npm install
```
* Rodar aplicação local

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ node server.js
Servidor rodando na porta 8080

```

* Construindo Dockerfile e Image

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker build -t orbite82/conversao-temperatura-2:v1 .
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker image ls
REPOSITORY                         TAG       IMAGE ID       CREATED             SIZE
orbite82/conversao-temperatura-2   v1        cb38c1e89678   40 seconds ago      1.05GB
```

* Reutilizando o cache: Alterando no arquivo server.js com comentário

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker build -t orbite82/conversao-temperatura-2:v1 .
Sending build context to Docker daemon  21.08MB
Step 1/7 : FROM node
 ---> e3cb0fb99b7c
Step 2/7 : WORKDIR /app
 ---> Using cache
 ---> 29cfbac4033d
Step 3/7 : COPY package*.json ./
 ---> Using cache
 ---> cfebe90cd5a6
Step 4/7 : RUN npm install
 ---> Using cache
 ---> 91347e7e514e
Step 5/7 : COPY . .
 ---> 334f8efdf92c
Step 6/7 : EXPOSE 8080
 ---> Running in d5deb26d374b
Removing intermediate container d5deb26d374b
 ---> 9c7379686556
Step 7/7 : CMD ["node", "server.js"]
 ---> Running in ae7aba5e1178
Removing intermediate container ae7aba5e1178
 ---> 1aa42081a58e
Successfully built 1aa42081a58e
Successfully tagged orbite82/conversao-temperatura-2:v1
```

* Testar a aplicação e imagem do Docker

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker container run -d -p 8080:8080 orbite82/conversao-temperatura-2:v1
cdc1a722b1c7cd00147bd077a83e983f1fa587105e1e328cff4935f7417c2e42
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker image ls
REPOSITORY                         TAG       IMAGE ID       CREATED             SIZE
orbite82/conversao-temperatura-2   v1        1aa42081a58e   4 minutes ago       1.05GB
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker container ls
CONTAINER ID   IMAGE                                 COMMAND                  CREATED              STATUS              PORTS                                             NAMES
1e6cde14b97b   orbite82/conversao-temperatura-2:v1   "docker-entrypoint.s…"   About a minute ago   Up About a minute   8080/tcp, 0.0.0.0:8080->80/tcp, :::8080->80/tcp   quirky_chatterjee
e7a1653c14f2   postgres                              "docker-entrypoint.s…"   3 hours ago          Up 3 hours          0.0.0.0:5432->5432/tcp, :::5432->5432/tcp         romantic_liskov
```

* Versão do Node

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ node --version
v14.19.3
```

* Atualizando Versão do Node: 16.X

Node.js v12.x:

```
$ curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
$ sudo apt-get install -y nodejs

```
sudo apt-get install -f
sudo apt-get remove npm nodejs
sudo apt-get install npm nodejs

Dependências desencontradas e pacotes quebrados que impediam de instalar um programa conseguir resolver consegui resolver dando um:

sudo aptitude safe-upgrade
sudo aptitude update
sudo aptitude install npm
node -v

[Link](https://pt.stackoverflow.com/questions/215927/erro-npm-e-node-ubuntu)

* Versão Atualizada:16.X

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ node --version
v16.15.1
```

* Image nova V2

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker build -t orbite82/conversao-temperatura-2:v2 .
Sending build context to Docker daemon  21.08MB
Step 1/7 : FROM node:16.15.1
 ---> b59df4e04d61
Step 2/7 : WORKDIR /app
 ---> Using cache
 ---> 8bd5988d50c8
Step 3/7 : COPY package*.json ./
 ---> Using cache
 ---> 413594f09f93
Step 4/7 : RUN npm install
 ---> Using cache
 ---> adf5fb46a222
Step 5/7 : COPY . .
 ---> e1e918a9dc24
Step 6/7 : EXPOSE 8080
 ---> Running in e95bf87bd6ad
Removing intermediate container e95bf87bd6ad
 ---> 233e25db35ef
Step 7/7 : CMD ["node", "server.js"]
 ---> Running in cdb4423797f5
Removing intermediate container cdb4423797f5
 ---> b98110872971
Successfully built b98110872971
Successfully tagged orbite82/conversao-temperatura-2:v2

```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker image ls
REPOSITORY                         TAG       IMAGE ID       CREATED          SIZE
orbite82/conversao-temperatura-2   v2        b98110872971   2 minutes ago    959MB
orbite82/conversao-temperatura-2   v1        1aa42081a58e   32 minutes ago   1.05GB
node                               16.15.1   b59df4e04d61   2 hours ago      907MB
node                               latest    e3cb0fb99b7c   2 hours ago      996MB
postgres                           latest    5b21e2e86aab   9 days ago       376MB

```

* Executando V2 container

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker container run -d -p 8080:8080 orbite82/conversao-temperatura-2:v2
a44744f98ef30ccd72911a615db92234c07a35045cb3d08abe44bf6200a7207c
```