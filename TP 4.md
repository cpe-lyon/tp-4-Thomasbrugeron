# Compte rendu TP4
## Exercice 1 : Commandes de base


### Question 1 
```
sudo apt update
```
### Question 2
```
alias maj='sudo apt update'
```
Pour que l'alias soit permanent il faut modifier le fichier bashrc.

### Question 3
```
cat /var/log/dpkg.log | grep installed | tail -n 5
2022-09-22 06:57:42 status half-installed linux-headers-5.15.0-33:all 5.15.0-33.34
2022-09-22 06:57:44 status not-installed linux-headers-5.15.0-33:all <none>
2022-09-22 09:46:50 status half-installed acl:amd64 2.3.1-1
2022-09-22 09:46:50 status installed acl:amd64 2.3.1-1
2022-09-22 09:46:50 status installed man-db:amd64 2.10.2-1
```
### Question 4
```
apt list --installed
```
### Question 5
Pour compter le nombre de paquet installés sur la machine avec dpkg il faut utiliser la commande :  ```dpkg -l | wc -l```
Pour apt c'est la commande : ```apt list --installed | wc -l```
La différence de comptage est du au faite que la commande dpkg -l compte aussi les paquets supprimés. Il est impossible d'utiliser le fichier dpkg.log car il ne contient pas le nombre de paquets installés.
 
 ### Question 6
 
Pour vérifier cela on peut utiliser la commande : ```apt-cache search . | wc -l```
Il y a au total : 69052 

 ### Question 7

Glances est une application en ligne de commande qui permet d'afficher l'état des principales ressources d'un système, de sa charge et du fonctionnement des applications.

Le paquet tldr convertit les pages man de tldr en explications plus concises.

Le paquet Hollywood simule une fenêtre de hacking.

### Question 8

Les paquets qui proposent de jouer au sudoku est ```gnome-sudoku``` et ```Ksudoku```

### Exercice 2 

Pour obtenir cette information il faut utiliser la commande : ```dpkg -S ls```
```
#!/bin/bash

if [ $# -ne 1 ]; then
    echo "Usage: $0 <command>"
    exit 1
fi

dpkg -S 
```
### Exercice 3

Pour vérifier si le paquet est installé ou non on peut utiliser la commande :
```dpkg -s nom_du_paquet | grep Status```


### Exercice 4 

Pour afficher les programmes coreutils on peut utiliser la commande ```apt-cache show coreutils ```

### Exercice 5 

Pour installer les paquets emacs et lynx, il faut utiliser la commande : ```aptitude install emacs lynx```

### Exercice 6

Pour vérifier si le nouveau fichier a bien été crée il faut utiliser la commande : ```ls /etc/apt/sources.list.d```
Et on peut voir que le fichier a bien été crée, il contient les nouveaux dépôts de paque


### Exercice 7 

2. Pour installer et compiler ce programme il faut d'abord télécharger make en faisait un apt-get install make.
Puis la commande sudo make install permet d'installer le programme en local.

3. Checkinstall permet de créer très facilement un un paquet deb à partir des sources d'un logiciel

4. Pour compiler avec checkinstall il faut d'abord installer les paquets avec la commande apt-get install checkinstall 
	Puis avec la commande sudo checkinstall il est possible de compiler.

### Exercice 8 

1. Pour créer le sous dossier origine-commande on tape la commande :``` mkdir /script/origine-commande. ```
	Puis ```mkdir /script/origine-commande/DEBIAN ```pour créer le sous dossier DEBIAN.
	Pour finir on utilise la commande : ```mkdir -p script/origine-commande/usr/local/bin```

2. On crée le fichier avec touch control puis on l'ouvre avec nano control pour l'éditer. Et on rentre les différents champs indiqués.

### Création du dépôt personnel avec reprepro 

1.  Pour créer le dossier repo-cpe on utilise la commande ```mkdir repo-cpe```

2.On créer les sous dossiers en tapant: ```mkdir /repo-cpe/conf et mkdir /repo-cpe/packages```

3. Donc on crée le fichier distributions avec la commande touch distributions dans le dossier conf, puis on le rempli avec les différents champs

4. ```reprepro -b . export```
 
5.  On copie avec la commande ```cp origine-commande.deb ../repo-cpe/packages ```depuis le dossier script
	Puis on exécute la commande

6.  Donc on se rend dans ```/etc/apt/sources.list.d ```avec la commande cd, puis on crée le fichier avec la commande ```sudo touch repo-cpe.list``` et on l'édite avec ```sudo nano.```

7. Lorsqu'on lance sudo apt update on voit bien que le paquet a été intégré.

### Signature du dépôt avec GPG

1. On crée la paire de clés avec la commande ```gpg --gen-key```, on rentre un nom, une adresse mail et une passphrase à retenir.

2. On retourne dans le dossier conf avec ```cd /repo-cpe/conf``` et on édite le fichier distributions pour rajouter ```SignWith: yes```

3. On se met dans le dossier repo-cpe puis on tape la commande : ```reprepro --ask-passphrase -b . export```

4. Toujours dans le dossier on tape la commande ```gpg --export -a "auteur" > public.key```

5. Puis pour finir on ajoute cette clé dans la liste apt avec la commande ```sudo apt-key add public.key```






