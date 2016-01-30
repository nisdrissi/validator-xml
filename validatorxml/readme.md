##Application permettant de valider un XML et son XSD sur une machine supportant Docker

Ce travail permet de valider un fichier XML accompagné de son XSD sur une machine virtuelle Docker. 
Il a été réalisé en utilisant une machine dont le système d’exploitation est MAC OS X El Capitan, version 10.11.2. 

L’intérêt est d’utiliser Docker afin de créer un container dont l’objectif est de faire une seule chose. C’est un processus pour une application unique. Ainsi, le container va lancer une application à pleine performance directement au système. 

Pour cela, nous avons voir les différentes étapes nécessaires, de l’installation de Docker jusqu’à la commande permettant de savoir si le fichier XML et son XSD sont valides ou non. 

####I.	INSTALLATION DE DOCKER

Pour parvenir à la création de l’application de validation XML/XSD, nous allons dans un premier temps installer docker. 
Il faut se rendre sur le site <a href="https://www.docker.com">Docker.com</a> puis cliquer sur le boutton « Get Starded with Docker » afin de suivre les premières étapes d’installation. 
Au cours de ces étapes, il faudra :
<ol>
<li>Vérifier la version Mac actuelle, afin d’être sûr qu’elle est postérieure à la version 10.8, sinon Docker ne pourra être chargé sur l’ordinateur 
<li>Télécharger le package « Docker Toolbox » sur le lien suivant : <a href="https://www.docker.com/products/docker-toolbox">Docker Toolbox</a>
<li>Vérifier que l’installation est correcte en lançant un terminal Docker
</ol>
Dans le shell, la configuration s’effectue automatiquement comme le montre la figure suivante : 


####II.	DOCKER ET LES CONTAINERS

Pour tester la bonne installation de docker sur la machine, on peut lancer la commande docker pull debian nous permettant d’activer un container. 

Ensuite, on utilise la commande $ docker images afin d’avoir un aperçu des images actuellement en cours sur la machine. 


Ensuite, on peut créer un Dockerfile avec des paramètres spécifiques :

L’image d’origine est debian
<blockquote></strong>FROM debian:latest</strong></blockquote>
La maintenance est effectuée par un auteur
<blockquote><p>MAINTAINER drissi</p></blockquote>
On lance l’execution d’une mise à jour ET de l’installation de la librairie libxml2-utils
<blockquote><p>RUN apt-get update && apt-get install -y libxml2<p></blockquote>
On ajoute dans le container le script pour la validation du XML et de son XSD. Ce script est constitué de la commande suivante : 

xmllint $schemaXML --schema $schemaXSD --noout ;

ADD ScriptValidatorXMLandXSD.sh Users/nisrinedrissi/Desktop/validatorxml/ScriptValidatorXMLandXSD.sh

On y trouve 2 variables :
schemaXML : pour le fichier XML à valider
schemaXSD : pour le fichier XSD à valider

RUN chmod +x Users/nisrinedrissi/Desktop/validatorxml/ScriptValidatorXMLandXSD.sh
Enfin, on lance le script qui sera executé.