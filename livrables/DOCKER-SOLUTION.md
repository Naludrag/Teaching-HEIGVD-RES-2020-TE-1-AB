# Rendu de l'exercice Docker

**Auteur: Stéphane Teixeira Carvalho (`stephane.teixeiracarvalho@heig-vd.ch`)**

## Compte rendu

Expliquez ici quelle stratégie vous avez utilisée pour vous connecter au service exécuté dans le container, en décrivant les étapes suivies:

* docker image ls : voir si l'images est existante
* docker run oliechti/faq : Lance une première image
* docker run oliechti/faq : Lance une deuxième image
* docker ps : affiche les contaiers en éxecutation
* docker inspect <container> | grep -i ipaddr: affiche l'adresse ip de la machine
* docker run -it <container> /bin/bash : ouvrir un invite de commande avec un container.
* netcat adresseip port : pour se connecter au service

## Capture d'écran

Assurez-vous que vous avez placé la capture d'écran dans un fichier nommé `CAPTURE-RES.png`.

## Remarques

Si vous avez des choses à partager au sujet de l'exercice, utilisez cette dernière section.
