DOCKER

Ce projet Docker est composé de deux dockerfiles ainsi que d'un docker compose.yml
----------------------------------
docker-compose up
----------------------------------
Le docker posséde trois services :

-server
-client
-mongo

Les Dockerfiles
---------------------------------
Les Dockerfiles sont des fichiers décrivant les différentes étapes permettant de partir d'une base pour aller vers une application.
---------------------------------
Backend

server :

FROM node:10       --> l'image basé sur Node 10

WORKDIR /app       --> Modifie le répertoire courant

COPY ./package.json ./  --> Copie les dépendances JSON

RUN npm install    --> Installe les package du projet

EXPOSE 8080             --> définie le port du service

CMD ["npm","start"]     --> lance le service

Frontend

client :

FROM mhart/alpine-node:3.12.0 --> l'image basé sur alpine avec Node

WORKDIR /app                  --> Modifie le répertoire courant

COPY ./package.json ./        --> Copie les dépendances JSON

RUN npm install               -->Installe les package du projet

EXPOSE 2368                   --> définie le port du service

CMD ["npm","start"]           --> lance le service

Le Docker compose
-------------------------------
Le Docker compose est un fichier qui permet de démarrer l'ensemble des conteneurs en une seule commande. Ce qui évite dans ce cas précis d'avoir à lancer les commandes docker run plusieurs fois pour les différents services.
-------------------------------
version: "3"
services:
    server:
        image: api
        restart: always
        ports: 
            - 8080:80
        depends_on: 
            - mongo
    client:
        image: client
        restart: always
        ports:
            - 2368:2368
    mongodb:
        image: mongo
        restart: always
        ports:
            - 27017:27017

Le dockercompose est structuré toujours de la même façon
-définition du service

-définition de l'image

-définition du ports


Mais dans ce cas si on peut également être plus précis en utilisant par exemple
-restart

-depend_on
