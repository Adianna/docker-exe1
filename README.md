# docker-exe1

## EXERCICE 1
Creez un repo github nommé **docker-exe1**  
il doit etre public, avec un fichier README.md , un fichier  .gitignore valable pour le langage Python, une License MIT  
Faites un git clone dans votre directory project local   
mettre en place dans goland la connexion ssh vers votre VM   
attention a ne pas oublier le mapping sur le deployment path sur /home/ubuntu/docker-exe1  
Mettre les commandes de l'exercice suivant dans le fichier README.md

Dans une commande docker run
* vous devez etre en interactif et avec un tty pour le display
* le container doit etre nommé **myalpes**
* dans cette commande creer un volume /MountPoint
* image doit etre alpine
* passer la commande /bin/ash   
  Ensuite a l'interieur du container
* creer un fichier test.py
* et inserez le texte "WARNING: ret pointer is null"
---
* a partir de ce container créer une image nommée  myalpine:v12.
* Supprimer les metadata de cette image avec docker export et docker import
* Verifier aavec docker history
* mettez cette image dans docker hub sous votre compte docker hub

*******************************************************Correction*****************************************************************

## Commandes a executer

```shell
 
git clone https://github.com/Adianna/docker-exe1.git    # On clone le projet docker-exe1.git depuis notre github
cd docker-exe1/        # On se positonne dans ce répertoire
docker run -it --name myalpes  -v /MountPoint alpine /bin/ash       # Création de l'image myalpes en interactif + création du volume /Mountpoint, avec l'image alpine et on passe à /bin/ash

vi test.py  #creer un fichier test.py et inserez le texte "WARNING: ret pointer is null"

docker commit myalpes myalpine:v12    # a partir de ce container créer une image nommée  myalpine:v12
docker images          # On verifie que l'image a ete cree

# Nettoyer
docker stop $(docker ps -aq)         # Arreter tous les containers
docker rmi -f $(docker images -q)  # Supprimer toutes les images avec -f pour forcer la suppression

# Supprimer les metadata de cette image avec docker export et docker import
docker export myalpes > v12.tar     
ls -alrt
cat v12.tar | docker import - myalpine:v12
docker images
docker history myalpine:v12


# Mettre cette image dans docker hub sous votre compte docker hub
docker login -u "adianakhady" -p "************"
docker image tag myalpine:v12 "adianakhady"/myalpine:v12
docker push "adianakhady"/myalpine:v12

```
