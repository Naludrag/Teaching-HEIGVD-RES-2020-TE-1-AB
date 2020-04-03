# Protocole JOCC 0.9

**Auteur: Stéphane Teixeira Carvalho (`stéphane.teixeiracarvalho@heig-vd.ch`)**

## Introduction

### 1.1 Objetifs du protocole
Le protocole JOCC a été conçu pour permettre à des clients de recevoir ou envyoyer des Jokes sur un serveur, au travers d'un réseau TCP/IP.
Tout serveur implémentant ce protocol doit être capable de fournir des blagues de catégorie dark humour et COVID-19.

Il peut offrir des catégories de Jokes supplémentaires.
Les catégories qu'un serveur implémentent sont envoyer lors de la connexion d'un client.

Un client pourra effectuer une notation sur une Joke et également obtenir la liste des Jokes les mieux évalués(globale ou par catégorie),
les jokes les plus récentes ainsi qu'un classement sur les membres de la communauté qui ont fait le plus de jokes ou qui on les jokes les mieux évalués.

### 1.2 Fonctionnement général

Le protocol JOCC utilise le protocol TCP comme protocol de transport. Le port 4005 a été choisi comme port par défaut.
Après avoir accepté une demande de connexion, le serveur envoie la liste des catégories de Jokes qu'il peut accepter.

Le client peut ajouter des jokes aux serveurs et également en demander.

Chaque blague stockée sur le serveur ont un identifiant unique.
Une blague peut être évalué entre 1 et 10.

Si un message reçu n'est pas correct le serveur envoie un message EROR avec la nature de l'erreur

Lors du ranking il est possible de définir le type de ranking désiré 1 pour les utilisateur avec le plus de jokes ou 2 pour les utilisateur avec les meilleurs jokes(mieux évalué).
Seul les 10 meilleurs utilsateurs seront retournés.

Le client lorsqu'il désire se déconnecté va envoyer la commande QUIT le serveur ferme alors la connexion TCP.

## 2. Messages

Le protocole CALC définit 9 messages: WELCOME, STOREJOKE, GETJOKE, RESULTJOKE, EVALUATE, GETBESTJOKES, RESULTBESTJOKES, GETRECENTJOKES, RESULTRECENTJOKES, GETRANKING, RESULTRANKING, QUIT.
Le protocole est un protocole "ligne à ligne" (par oppostion à un protocole binaire).
Les clients et les serveurs DOIVENT utiliser la séquence CRLF (ASCII 13, ASCII 10) pour indiquer la fin d'une ligne.

### 1.1 WELCOME
Ce message est envoyé du serveur au client, immédiatement après que la connexion TCP ait été établie.
Le message est constitué de plusierus lignes indiquant les catégories disponibles. Après avoir lu la première ligne, le client doit lire une ligne ('- AVAILABLE CATEGORIES'),
 puis toutes les lignes jsuqu'à ce qu'il rencontre une ligne dont la valeur est '- END CATEGORIES'.
Chaque ligne lue indique les catégories supoortée par le serveur.

Exemple:
WELCOME CRLF
- AVAILABLE OPERATRIONS CRLF
- DARKHUMOUR CRLF
- COVID-19 CRLF
- END OPERATIONS CRLF

## 1.2 STOREJOKE
Ce message est envoyé du client au serveur, pour soumettre une nouvelle joke. Le message est défini par STOREJOKE, une catégorie et la Joke.
Les valeurs sont séparées par un espace.

Exemple: STOREJOKE DARKHUMOUR Je suis une blague CRLF

## 1.3 GETJOKE
Ce message est envoyé du client au serveur, pour demander une joke au serveur.
Le message est défini par la chaîne GETJOKE, suivie d'un espace et de la catégorie de la joke désirée.

Exemple: GETJOKE DARKHUMOUR CRLF

## 1.4 RESULTJOKE
Ce message est envoyé du serveur au client, pour envoyer une Joke.
Le message est défini par la chaîne RESULTJOKE, id de la Joke suivie de la Joke.

Exemple: RESULTJOKE 8 Je suis une blague CRLF

## 1.5 EVALUATE
Ce message permet d'évaluer une blague est il est envoyé du client au serveur.
Le message est défini par EVALUATE, l'id de la joke suivi de la note.

Exemple: EVALUATE 8 10 CRLF

## 1.6 GETBESTJOKES
Ce message permet de demander les meilleures blagues sur le serveur.
Il est envoyé du client au serveur.
Le message est défini par GETBESTJOKES suivi du nombre de jokes voulues.

Exemple: GETBESTJOKES 10 CRLF

## 1.7 RESULTBESTJOKES

Ce message permet de recevoir les meilleures blagues du serveur.
Il est envoyé du serveur au client.
Le message est défini par RESULTBESTJOKES, puis le nombre de Jokes renvoyé.
Chaque joke est ensuite une ligne avec son id et la joke.

Exemple : RESULTBESTJOKES 10 CRLF
          1 C'est une blague CRLF
          2 C'est une deuxième blague CRLF

## 1.8 GETRECENTJOKES
Ce message est envoyé du client vers le serveur, pour recevoir les blagues les plus récentes.
Le message est défini par GETRECENTJOKES suivi du nombre de jokes voulus.

Exemple: GETRECENTJOKES 10 CRLF

## 1.9 RESULTRECENTJOKES

Ce message permet de recevoir les blagues les plus récentes du serveur.
Il est envoyé du serveur au client.
Le message est défini par RESULTRECENTJOKES, puis le nombre de Jokes renvoyé.
Chaque joke est ensuite une ligne avec son id et la joke.

Exemple : RESULTRECENTJOKES 10 CRLF
          1 C'est une blague CRLF
          2 C'est une deuxième blague CRLF

## 1.10 GETRANKING
Ce message est envoyé du client vers les serveur, pour recevoir le ranking désiré.
Le message est défini par GETRANKING suivi du types de ranging désiré.

Exemple: GETRANKING 1 CRLF

## 1.11 RESULTRANKING
Ce message

## 1.12 QUIT

## 3. Elements spécifiques

## 3.1 Categories supportées

## 3.2 Extensibilité

## 3.3 Traitements d'erreurs

## 3.4 Statefull
Le serveur sera de type statefull car nous devrons garder les différents Jokes sur le serveur pour pouvoir retourner les meilleurs Jokes par exemple.


## 4. Exemples

S:


## Remarques

Pas assez de temps pour terminer donc pas de login utilisateur.
