**TD1**

**1. Ligne de commande : mode Interactif**

**1.1 Terminologie**

-interpréteur de commande : logiciel système de l’OS qui analyse, de traduit et exécute des commandes

-terminal : interface permettant d’interagir avec un interpréteur de commande.

-shell : interpréteur de commande destiné aux système d’exploitation unix

-prompt : indication signifiant que l’interpreteur de commande est prêt à executer une nouvelle commande. C’est une chaine de caractère qui se compose souvent du login, de « @ », du nom de la machine, de « : », et de l’endroit où on se situe.

-invite de commande : endroit où l’on saisit la commandes

-homedirectory : répertoire contenant toutes les donnés personnelles

-utilisateur : personne utilisant l’ordinateur

-login: identifiant d’un utilisateur qui lui permet de se connecter au système.

-root : identifiant du super-utilisateur. Ce dernier a tous les pouvoirs sur l’OS  sauf sur certain fichiers avec un attribut particulier

-racine :répertoire de plus au niveau dans l’arborescence des répertoires de l’OS     

-completion : fait de compléter une commande automatiquement si elle est deviner

-wildcard : caractère qui remplace le début ou la fin d’un mot

**1.2 Trouver de l’aide**
		
**1.2.1 Man pages**


La commande ```man man``` permet d’afficher les informations sur la commande « man ». De manière général la commande man sert à afficher la documentation de sa commande passer en paramètre.

**1.2.3 Manuel de la commande ls**

1. La commande ```ls``` affiche l'ensemble de ses arguments fichiers autres que des répertoires. Puis ```ls``` affiche l'ensemble des fichiers contenus dans chaque répertoire indiqué.
2. L’option ``` -a ``` permet d’afficher les fichiers cachés
3. L’option ``` -l ``` permet d’afficher les fichiers avec un format long en liste
4. L’option ```-sh ``` permet d’afficher la taille des fichiers sous une forme facilement lisible par l’homme
5. L’option ```-R``` permet d’afficher récursivement le contenue d’un repertoire

Pour lister tous les fichiers commençant par « u » à la racine du système on peut utiliser la commande la commande
```ls -d /u*```


**1.2.4 La commande cd**


-La commande cd permet de se déplacer du répertoire courant au répertoire spécifié en paramètre
-La commande ```cd -``` effectue un déplacement du répertoire courant au répertoire où l’on se trouvait précédemment

**1.2.5 Manuel de la commande mkdir**


L’option qui permet de créer une hiérarchie de répertoire en une seul commande est ```-p```


**1.3 La commande echo**
  	
La commande echo permet d’afficher une variable ou une chaîne de caractères.

 ```echo -ne "\n\n *\tHello World $LOGNAME\t\t*\n\n" ```

Avec cette commande l’option ```-n``` empêche le retour à la ligne supplémentaire que echo réalise.
L’option ```-e``` permet d’interpréter les caractères précédés d’un « \ »

Enfin les guillemets permettent d’afficher la valeur de la variable LOGNAME avec  ```$LOGNAME```.Des apostrophes à la place des guillemets ne permet pas cela.

**2. Les redirections**
**2.1 Premières redirections**
```
ls
ls> file1 #crée le fichier file1 puis y écrit le retour de la fonction ls
pwd>file1 #écrase le contenue du fichier file1 et y écrit le chemin du répertoire courant 
ps aux >file2.txt # crée file2.txt et y écrit un tableau de tous les processus couramment utilisés
cd>file3 #crée le fichier file3 vide
cat file1 file2.txt >file4 #crée le fichier file4 et y écrit la concaténation de file1 et file2.txt
cat file1>>file1 #commande impossible car l’entré est la sortie
pwd>> file1 #écrit en fin du fichier file1  le chemin du répertoire courant 
cat file1 > /dev/null # rediriger la sortie vers /dev/null permet de s’en débarrasser
```
**2.2 Le pipe**


**2.2.1 pipe et cat**


La commande ```cat``` sans argument recopie l’entrée standard sur la sortie standard.

**2.2.2 Exemple de pipe**

```
ls -R>file1 #écrase le contenue de file1 et y met la sortie de la commande ls -R 
less file1 #affiche le contenue de file file1 page par page
cat file1 #affiche le contenue de file1 sur la sortie standard
cat file1 | less # <=> less file1
ps aux # affiche sur la sortie standard un tableau de tous les processus couramment utilisés 
ps aux | grep -v root # affiche toutes les lignes du tableau des processus couramment utilisés qui ne 			contiennent pas la chaîne « root » sur la sorite standard
ps aux | grep  root 	# affiche toutes les lignes du tableau des processus couramment utilisés qui  			contiennent la chaîne « root » sur la sortie standard
ps aux > file2 # écrase le contenue de file2 et y écrit un tableau de tous les processus couramment 		utilisés 
cat file2 | grep -v root #affiche sur la sortie standard  les lignes du fichier file2 qui ne contienne pas 			la chaîne « root »
```
Pour lister les processus n’appartenant pas à root mais qui contiennent root dans leur nom on peut utiliser :
```
ps aux | grep -Ev "^root" |grep root >processwithroot
```
Ceci les consigne dans le fichier « processwithroot »

**2.3 Redirection d’entrées**

La commande ``` cat <<eob```  recopie l’entrée sur la sortie standard lorsque la chaine « eob » est rencontrer.

**3.Gestion de processus**


**3.3 Processus en tache de fond**

Lorsque l’on lance ```ls``` dans le nouveau terminal en sommeil rien ne passe car ce dernier est en sommeil donc arrête.

Lorsque le nouveau terminal est mis en tache de fond le processus reprend donc la commande ls fonctionne.

**3.3.1 Application sur les états de processus**
	

 Lorsque le processus du script est placé en arrière plan et attend une entrée, il y a un problème lorsque l’on envoie une entré au processus en premier plan avec ```ls```.Le processus en arrière plan n’a pas l’air de recevoir l’entré. La sortie standard est partagée mais pas l’entrer standard d’où le problème.

	
**3.5 Jobs**

```
emacs &
xterm &
firefox &
emacs
Ctrl + C # tue le processus emacs en avant plan
jobs #montre tous les processus fils du terminal
fg%3# remet firefox en premier plan
Ctrl + Z # Arrète firefox
bg # met firefox en arrière plan
fg%2 # remet xterm au premier plan
Ctrl + C # tue le processus xterm
kill%1 # tue emacs en arrière plan
jobs# affiche qu’il reste firefox en arrière plan les autre processus ont été tué
```
**3.6 Chaîner les processus**

**3.6.1 Première chaîne de processus**

La commande à réaliser est la suivante :
```grep root /etc/passwd && echo "root existe"```
Le && est fait de façon à ce que la deuxième commande s’exécute que si la première renvoie un résultat positif.

**3.6.2  Chaîne plus évoluée**


La commande à réaliser est la suivante :
```ps aux | grep -v grep | grep firefox > /dev/null  && echo  "Firefox is running" || echo "Firefox is not running"```

Si la commande à gauche du « || » ne renvoie pas un résultat positif alors celle à sa droite est exécutée

**4. Le Système d’exploitation GNU/Linux **

**4.2 Questions**

-Mon répertoire personnel possède les droits  ```rwx r-x r-x```. Autrement dis j’ai le droit de lecture d’écriture  et d’éxecution. Mon groupe à le droit de lecture et d’éxécution. De même pour le reste du monde.

-Mon homedir appartient au groupe correspondant à mon numéro étudiant 
-de même j’appartient au groupe correspondant à mon numéro étudiant 
-mon GID est mon numéro étudiant
-Pour avoir les droits ```rwx------```:
```chmod u=rwx,g=,o=  mydir```
ou
```chmod 700 mydir```



-Pour avoir les droits ```rwxr-x---```:
```chmod u=rwx,g=rx,o=  mydir```
ou
```chmod 750 mydir```

-la commande ```chown``` pour changer de propriétaire doit être fait en mode root.



**5. Les variables**

**5.4 Exercices**

1. ```echo $HOME```. HOME contient le chemin absolue de mon home directory

2.```echo $PWD```. PWD contient  le chemin d'accès vers le répertoire où se situe l'utilisateur qui a entré la commande. 

3.```echo $PATH``` PATH est utilisée pour localiser les commandes dans l'arborescence des répertoires Unix. En définissant la variable PATH, on crée un ensemble fixe de répertoires dans lesquels le système cherche systématiquement les fichiers à utiliser lorsque l’on entre le nom d'une commande

4.```echo $PS1``` La variable PS1 définit le prompt Unix/Linux.

5.Tout dépend de la commande mais si c’est une commande externe comme ```ls``` et que la variable PATH ne contient plus /bin  ```ls``` ne fonctionnera pas car elle est localisé dans /bin/ls 

6.Le prompt ne change pas dans le nouveau terminal lorsque l’on modifie PS1 car la modification de PS1 n’est prise en compte que dans le shell où on l’a modifier. Or quand on ouvre un nouveau terminal on ouvre un nouveau shell.

7. Chaque shell lorsqu’il démarre possède les variables dont les valeurs sont contenues dans .bashrc En modifiant la variable PS1 dans .bashrc le nouveau terminal aura bien la valeur de PS1 que l’on voulait.

**5.5 Chaîne de caractères**
```
echo $HOME # Affiche le contenue de la variable HOME

echo "$HOME" # De même et a l'intérieur d'une paire de guillemets, tous les caractères de chaîne sauf " sont protégés de l'interprétation du shell.

echo ‘$HOME’ #Affiche « $HOME » car à l’intérieur d’une paire d’apostrophe tous les caractères de chaîne sont protégés de l'interprétation du shell.
echo `$HOME` : le shell tente d’exécuter la commande dont le nom est la valeur de la variable HOME
TEST=ls

echo  "`$TEST`" : est équivalent à faire echo sur la chaîne de caractère renvoyer par ls
test=$(ls);echo $test ; la varibale test reçoit  la chaîne de caractère renvoyer par ls.
```
**6. Les scripts**

myscript:
```
#!/usr/bin/bash

cd /tmp
ls
cd
```
En exécutant ```./myscript``` ça ne fonctionne pas pour 2 raisons :
-la première est que le fichier myscript n’a pas la permission d’être exécuté.
-la deuxième est que le fichier /usr/bin/bash n’existe pas.

Il faut donc modifier la permission de myscript avec chmod u+x myscript puis remplacer le shebang par # !/bin/bash

**6.1 Structures de controles**
		
**6.1.1 if...then...else**

Le script à réaliser est le suivant :
```
if [ -d "/var/log" ]
then
        echo "Le dossier /var/log existe !"
else
        echo "Le dossier /var/log existe pas"
fi

if [ -d "/var/lOg" ]
then
        echo "Le dossier /var/lOg existe !"
else
        echo "Le dossier /var/lOg existe pas !"
fi

if [ -w "/etc" ]
then
        echo "Alerte"
else
        echo "ok"
fi
```
L’option ```-d``` test l’existence d’un dossier et l’option  ```-w``` test le droit en écriture d’un fichier/dossier

**6.1.2 for...do...done**


Un script réalisable  pour afficher a b c d à raison d’une lettre par ligne est le suivant :
```
l="a b c d"
for a in $l
do
        echo $a
done
```

**6.1.3 while...do...done**

Dans la commande :
```
ls | while read a ;do echo $a; done
```
la sortie de la commande ls est redirigé sur l’entrée de la boucle while sous forme d’une chaine de caractères.
a prend successivement la valeur des chaînes de caractères séparées par un espacement contenuent dans la chaine de caractères à l’entrée du while.

**6.2 Scanner le réseau**

Voici un script solution   :
```
deb=1
fin=254
RES=1
for((i=deb;i<=fin;i++))
do
a=$( ping "132.227.114."$i -c1 | grep -E -o '[0-9]+ received' | cut -f1 -d ' ') 
if [ "$a" == "$RES" ]
then
echo "132.227.114."$i 
else
echo "no"
fi
done
```

a vaut 1 si le ping fonctionne.







**6.3 Script poubelle**

Voici un script solution   :
```
arg=$@
i=0
zero=0
for a in $arg
do

	if [ -f "$a" ];then
		mv "$a" "$HOME/.trash"
	else
		echo "le fichier $a n'existe pas"
	fi	


done

```
-f teste l’existence du fichier 

**7. Gestion des droits**
**7.1**

chmod permet de changer les droits d’un fichiers ou d’un dossiers
chown permet de changer le propriétaire d’un fichier ou d’un dossiers
chgrp permet de changer le groupe d'utilisateur possédant un fichier ou un dossier

**7.2**

mkdir data 
chmod 777 data 

**7.3**

L’utilisateur John pourra effectivement supprimer le fichier toto.txt car tout le monde possède les droits en écriture sur le dossier data.

**7.4**

Un utilisateur peut supprimer un fichier dont il n’est pas le propriétaire   

**7.5**

Il suffit de rajouter le sticky bit au dossier data 
```
chmod 1777 data
```
Ainsi seul le propriétaire d’un fichier peut le supprimer






**7.6**

/dev/null n’est pas un fichier standard c’est un fichier associé à un périphérique et on ne peut écrire dedans. De même pour /dev/sda et /dev/mem

**8. Setuid / Setgid**

**8.1**
Les deux fichiers possède le droit SUID et leur propriétaire est root. Cependant il faut que chaque utilisateur puisse changer son mot de passe avec la commande passwd. C’est-à-dire que lorsqu’un utilisateur lance la commande passwd, elle est lancée avec les droits du superutilisateur, ainsi l’écriture pourra se faire dans le fichier /usr/bin/passwd et l’utilisateur aura changé son mot de passe sans être root.

**8.2**

uid.c:
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
int main(){

	int uid=geteuid();
	int gid=getegid();
	printf("uid:%d , gid:%d \n",uid,gid);

	return 0;
}
```

**8.3**

```
gcc uid.c
chmod 6777 a.out 
```

**8.4**

Sachant que le propriétaire du fichier a.out est « demon », lorsque l’on le lance avec l’utilisateur root il renvoie le uid et le gid de demon. Car il est exécuter avec les droit de « demon »  et du groupe « demon » à cause des droits SUID et SGID

**8.5**
```
chmod 4777 a.out 
```
Cette fois ci a.out le ne possède plus le droit SGID donc lorsque l’on l’exécute avec l’utilisateur root il renvoie le uid de demon et le gid de root.







**TD2**

**5. Installation du système de base**

**5.1 Partitionnement de la VM**

On utilise ```fdisk```

**5.2 Création des systèmes de fichiers**

```
mkfs.ext4 /dev/sda1
mkswap /dev/sda5
```
**5.3 Montage des partitions **

```
mkdir target
mount /dev/sda1 target
```
**5.5 Écriture du système de base**
```
debootstrap –variant=minbase stable /target http://ftp.fr.debian.org/debian
```
**5.6 Entrée dans le futur environnement**


Pour pouvoir accéder aux périphériques dans le futur environnement :
```
mount -o bind /dev /target/dev 
```
Pour que le futur environnement  puisse agir sur les processus, interagir avec le noyau et possède les informations nécessaire sur les périphériques et leurs pilotes.

```
mount -t proc none /target/proc
mount -t sysfs none /target/sys
```

Ensuite ```chroot /target /bin/bash``` permet de lancer un shell bash où /target sera la nouvelle racine

**5.7 Mise à jour du systèmes**

Dans notre cas aucun paquet n’est mis à jour car le debootstrap pour installer le système l’a fait depuis une url où les fichiers sont à jour.

**5.8 Installation du noyau**

```
apt-get install linux-image-amd64 permet d’installer le noyau qui sera charger en mémoire au démarrage de la machine.
```

**5.9 Installation du Grub**

```
apt-get install grub2 
```
Permet d’installer le grub sur le MBR


On fait  ```vim /etc/default/grub``` et on rajoute  GRUB_CMDLINE_LINUX=« net.ifnames=0 »
Dans GRUB_CMDLINE_LINUX, on y met les paramètres à ajouter lors de la détection automatique du système lors d’un démarrage .  Mettre GRUB_CMDLINE_LINUX=« net.ifnames=0 » permet de faire en sorte que si l’utilisateur utilise une seul carte réseau elle s’appellera toujours eth0. Sans ça, il faudra à chaque fois chercher le nom de la carte réseau ce qui peut s’avérer pénible.

**5.10 Finalisation du nouvel environnement**

**5.10.2 Renseignement des points de montages**




Avec ```vim /etc/fstab``` on édit /etc/fstab  avec 
```
/dev/sda1 / ext4 defaults 0 0 
/dev/sda5 none swap defaults 0 0
```

**5.10.3 Installation de paquets additionels**

```
apt-get install systemd 
```
**5.10.4 Configuration du réseau**

On edite le fichier /etc/systemd/netwotk/eth0.network
avec :
```
[Match]
Name=eth0

[Network]
DHCP=yes
```
Ensuite en active les service systemd-networkd et systemd-resolved avec les commandes
```
systemctl enable systemd-networkd
systemctl enable systemd-resolved
```

**7.Installation des outils d’administration**

Installation de OpenSSH :
```
apt-get install openssh-server
apt-get install openssh-client
```
PermitRootLogin permet en fonction de sa valeur de se connecter en ssh sur la machine en mode root.


**TD3**

**1 Gestion des utilisateurs, des groupes et des mots de passe**
	
**1.1 A la main**
		
**1.1.1**


- /etc/passwd

passwd contient des lignes du type 
```
a:b:c:d:e:f:g
```
a : nom d’utilisateur qui doit être unique

b:information sur le mot de passe de l’utilisateur. Dans les dernière version les informations sur le mot de passe son dans le fichier shadow

c: UID numéro identifiant un utilisateur

d : GID. C’est un numéro identifiant du groupe principal de l’utilisateur. Tous les fichier créer par l’utilisateur « a »  sont initialement accessible au membre de ce groupe

e: Divers information sur l’utilisateur. Ex : nom, téléphone, mail 
 
f:chemin vers le répertoire personnel de l’utilisateur 

g: programme qui est lancé chaque fois que l’utilisateur se connecte au système.


Finalement chaque ligne de passwd contient des informations sur un utilisateur  


- /etc/shadow

shadow contient des lignes du type 
```
a:b:c:d:e:f:g:h:i
```
a : nom d’utilisateur

b : 	Soit b est : «$» + type de hachage + «$» + sel + «$» + hash de (sel | mot de passe de 		l’utilisateur) 
	Soit une valeur d’exception

 c: date de la dernière modification du mot de passe ( exprimé en nombre de jours depuis 1970)

d: nombre de jours avant que le mot de passe puisse être changer

e:nombre de jour après lesquels l’utilisateur DOIT changer son mot de passe 


f : nombre de jours durant lesquels l’utilisateur sera informé de l’expiration prochaine de son mot de passe si il se connecte.

g : nombre de jour avant la désactivation du compte si le mot de passe à expiré

h:date de désactivation du compte exprimer en nombre de jours depuis 1970

i :?



- /etc/group

group contient des ligne de la forme :
```
a:b:c:d
```
a : nom du groupe 

b:mot de passe du groupe qui n’est en général pas utiliser

c : GID i.e. numéro unique identifiant du groupe

d:liste des utilisateurs appartenant au groupe

Chaque ligne de group contient des informations sur un groupe

-etc/gshadow
 
gshadow contient des lignes de la forme :
```
a:b:c:d
```
a: nom du groupe

b : mot de passe du groupe

c : liste des administrateurs du groupe qui peuvent modifier le mot de passe du groupe et les membres du groupe

d : liste des membre du groupe 


**1.1.2**
 
Ajout de ```sar :* :: » et « tp2 :* :: ```dans gshadow
Ajout de ``` sar:x:110 : » « tp2:x:111 ```dans group

		



**1.1.3**

1)
Ajout de 

```mike:x:22:11:mike:/home/mike:/bin/bash``` dans passwd

et
``` mike :::::::: ``` dans shadow

Tentative de connexion :
la connexion fonctionne mais on obtient le message
```No directory, logging in with HOME=/```
qui nous dit que notre home directory est la racine


2)

On effectue la commande ```passwd```

Tentative de connexion :

la connexion avec mot de passe  fonctionne mais on obtient le message
```No directory, logging in with HOME=/```
qui nous dit que notre home directory est la racine


3)

On effectue ```mkdir /home/mike``` avec root

Tentative de connexion :
la connexion avec mot de passe fonctionne, il y a plus de message d’erreur mais l’utilisateur mike no possède pas les droit d’écriture sur son home directory ce qui est problématique.

4)

On effectue ```chown mike /home/mike```  en root pour que l’utilisateur mike soit le propriétaire de son répertoire et puisse y ajouter/supprimer des fichiers.

Tentative de connexion :
la connexion avec mot de passe fonctionne, il y a plus de message d’erreur et l’utilisateur mike à tous les droits sur son home directory.

5)
On effectue en root :
```
cp /etc/skel/.bashrc  /home/mike/.bashrc
cp /etc/skel/.profile  /home/mike/.profile
```

Afin que l’utilisateur mike puisse personnaliser son environnement de travail 
		
	
**1.1.4**

Pour ajouter mike au groupe sar il suffit de rajouter « mike » dans la dernière colone de la ligne sar dans /etc/group et /etc/gshadow

**1.1.5**

Root ne peut pas voir le mot de passe de mike mais peut le changer 

**1.1.6**

```id``` renvoie le UID de l’utilisateur courant , le GID de l’utilisateur courant et le nom des groupes auquel appartient l’utilisateur courant
		
**1.1.7**

Pour fermer le compte d’un utilisateur il faut :
-supprimer la ligne mike dans /etc/shadow et /etc/group
-supprimer « mike » dans la liste des membres des groupes auxquels il appartient dans /etc/group et /etc/gshadow


**1.2 Avec des commandes**

**1.2.1**

-groupadd sert à créer un nouveau groupe,  groupadd new_group

-groupdel  sert à supprimer un groupe , groupdel groupeasuppimer

-useradd sert à ajouter un nouvelle utilisateur ,  useradd identifiant_utilisateur

-userdel  sert à supprimer un compte utilisateur,  userdel nom_utilisateur

-passwd sert à changer le mot de passe d’un compte,   passwd mike 

-gpasswd sert à changer le mot de passe d’un groupe,   gpasswd sar 

-usermod sert à modifier un compte utilisateur. Ex : son login, son gid,…

**1.2.2**
```
useradd elchapo
userdel elchapo
```
		
**1.2.3**

Pour bloquer le compte mike on peut soit  :

-remplacer /bin/bash par /bin/false dans /etc/passwd à la ligne mike 
-mettre un « ! »  devant le hash dans /etc/shadow à la ligne mike 

**1.2.4	**

En root :
```
adduser elchapo1
adduser elchapo2
passwd elchapo1 //mot de passe :elchapo
passwd elchapo2 //mot de passe :elchapo
```
On rappel que dans /etc/shadow chaque ligne est associé à un utilisateur est de la forme :
```
a:b:c:d:e:f:g:h:i
```
où b est la chaîne :
«$» + type de hachage + «$» + sel + «$» + hash de (sel | mot de passe de 	l’utilisateur) 

Pour elchapo1 et elchapo2 leur b est différent car leur sel est différent.

**2. Secure Shell**
	


**I Authentification du serveur par le client**

```
1)Le client demande à se connecter au serveur avec ssh  ….@…..
2)Le serveur envoie sa clé publique au client 
3)

Si le client ne s’est jamais connecter au serveur 
	Le client doit accepter ou non la clé publique du serveur
	Si le client accepte la clé publique du serveur 
		Linux enregistre que la clé publique du serveur dans ~/.ssh/known_hosts
	Sinon 
		La connexion est interrompu 
Sinon si le client s’est déjà connecter au serveur mais que la clé publique du serveur qu’il possède ne correspond pas à celle envoyé par le serveur
	Un message d’erreur est affiché et la connexion est interrompu

Ici la clé publique du serveur envoyé par le serveur correspond à la clé publique du serveur posséder par le client 
```

L’étape suivante se fait automatiquement :
Le client génère un clé symétrique dit clé de session qu’il chiffre avec la clé publique du serveur.
Le serveur déchiffre la clé de session avec sa clé privé qui sera la clé qui va servir pour chiffrer toute les futurs communications





		
**II Authentification du client par le serveur**

Avant de commencer à communiquer le serveur va vouloir authentifier le client
Pour cela :
- soit il lui demande le mot de passe du compte sur lequel le client veut se connecter et si c’est le bon la communication peut démarrer

-soit l’authentification du client vas se faire par clés.
Pour que l’authentification par clé ait lieu il faut préalablement que le client ait  généré une pair de clé publique/privé et qu’il ait diffuser sa clé public au serveur.
Les étapes suivantes se font automatiquement.Pour authentifier le client, le serveur va chiffrer un message avec la clé public du client. Ensuite le serveur va l’envoyer au client. Le client va déchiffrer le message et le renvoyer au clair au serveur. Si le message correspond bien au message clair initialement envoyer alos le client est authentifié et la communication avec la clé de session peut démarrer.

**2.1**

```mv ~/.ssh/knwown_hosts{,.old}```
Renomme le fichier ~/.ssh/knwown_hosts en ~/.ssh/knwown_hosts.old
Le fichier ~/.ssh/knwown_hosts contient la clé publique des serveur de confiance.
Or ici il n’existe plus.
Donc lors de la connexion au serveur du département un message va demander au client si oui ou non il fait confiance à la clé public du serveur.

Si on remplace la clé publique du serveur par une autre clé publique par exemple celle de son propre serveur. Étant donner qu’on s’est déjà connecter au serveur du département, un message d’erreur est affiché. Ce message d’erreur nous informe que la clé publique du serveur du département que l’on a dans ~/.ssh/knwown_hosts  ne correspond pas à celle envoyé par le serveur du département. Il nouos previent que l’on est peut être victime d’une attaque man-in-the-middle.

Pour résoudre ce probleme, il suffit d’effacer la clé publique du serveur du département que l’on possède dans ~/.ssh/knwown_hosts  avec la commande 
```ssh-keygen -f "/home/mike/.ssh/known_hosts" -R [ssh.upfr-info-p6.jussieu.fr]```


**2.2 Génération d’un clé asymétrique**


On génère les clés secure et unsecure avec :
```ssh-keygen -t ecdsa```

Avec cat on voit que secure.pub et unsecure.pub sont les clés publiques et que  secure et unsecure sont les clés privées.

Dans la clé asymétrique il y a une partie chiffré et une autre qu’il ne l’est pas. La partie chiffré est utile de sorte que si quelqu'un se connecte sur mon compte même si il récupère la clé il ne pourra pas l’utiliser sans la paraphrase. La partie non chiffré sert à identifier le protocole de chiffrement asymétrique utiliser. Si elle était chiffré cela pourrait poser des problèmes pour identifier de quel chiffrement provient cette clé.

Si on perd la paraphrase on perd la clé.


**2.3 Authentification par clé**

Déploiement des clés publiques :
```
ssh-copy-id -i ~/.ssh/secure 3531763s@ssh.ufr-info-p6.jussieu.fr
ssh-copy-id -i ~/.ssh/unsecure 3531763s@ssh.ufr-info-p6.jussieu.fr
```
L’authentification ne marche pas car il faut faire 
```
chmod 600 unsecure 
chmod 600 secure
```
De plus, il faut se connecter en utilisant
```
ssh -i  ~/.ssh/secure 3531763s@ssh.ufr-info-p6.jussieu.fr
```
ou

```
ssh -i  ~/.ssh/unsecure 3531763s@ssh.ufr-info-p6.jussieu.fr
```
Par défault avec 
```
ssh  3531763s@ssh.ufr-info-p6.jussieu.fr
```
la connexion avec authentification par clé essaie de se faire avec  ~/.ssh/id_ecdsa qui n’existe pas, c’est pour cette raison qu’il necessaire préciser la clé privé.

	
**2.4 Personnalisation de ssh**

On édite  ~/.ssh/config :
```
Hostname	ssh.ufr-info-p6.jussieu.fr
Host		secure
User		3531763
IdentityFile	~/.shh/secure

Hostname	ssh.ufr-info-p6.jussieu.fr
Host		unsecure
User		3531763
IdentityFile	~/.shh/unsecure
```
Ainsi, la connexion se fait avec ssh secure ou ssh unsecure

**2.5 Utilisation d’un porte clé**

L’avantage principal de ssh-agent est qu’il évite de retaper la passphrase à chaque fois.
Un inconvénient que si un attaquant récupère la mémoire il peutretrouver la passphrase et la clé
```
ssh-agent bash

ssh-add ~/.ssh/secure
```
=> ```ssh secure``` ne demande plus de passphrase


**2.6 Différents modes de connexions**


**2.6.1 Connexion par rebond**


Depuis la VM 
```
ssh 3531763@ppti-14-302-04.ufr-info-p6.jussieu.fr
```
puis
```
ssh 3531763@ppti-14-302-04.ufr-info-p6.jussieu.fr 
ssh 3531763@ppti-14-302-03.ufr-info-p6.jussieu.fr
ssh 3531763@ppti-14-302-02.ufr-info-p6.jussieu.fr
```
Depuis la VM 
```
ssh 3531763@ssh.ufr-info-p6.jussieu.fr
```
puis
```
3531763@ppti-14-302-04.ufr-info-p6.jussieu.fr 
3531763@ppti-14-302-03.ufr-info-p6.jussieu.fr
3531763@ppti-14-302-02.ufr-info-p6.jussieu.fr
```


**2.6.2 Redirection de port**

Après avoir installer gnome sur la VM
Depuis on lance un terminal
puis un second ou l’on exécute la commande
```
ssh -L 2222:ppti-14-302-03.ufr-info-p6.jussieu.fr:22 3531763@ssh.ufr-info-p6.jussieu.fr
```
En faisant ça on a redirigé le port 2222 de la VM vers le port 22 de l’ordinateur  ppti-14-302-03 via la passerelle ssh ufr-info-p6.jussieu.fr

Ainsi avec le second terminal ouvert en faisant
```
ssh -p 2222 3531763@localhost
```
on se connecte en ssh à nous même mais sur le port 2222 rediriger sur ppti-14-302-03 . Donc on se connecte à  ppti-14-302-03.

Lorsque l’on essaie  depuis la VM de faire :
```
ssh -L 1000:ppti-14-302-03.ufr-info-p6.jussieu.fr:22  3531763@ssh.ufr-info-p6.jussieu.fr
```
on obtient le message d’erreur :
Privileged ports can only be forwarded by root.

En effet, les port non privilégié sont ceux dont le numéro est supérieur à 1024. Pour le port 2000, cela marche bien.
	
**2.6.3 Le pivot**

L’option -W permet de faire une redirection de port de la machine courante vers la machine cible représenter par %h sur le port %p via la machine pivot donnée à la ligne ProxyCommand 

Ainsi, pour de connecter depuis la machine la VM vers la machine  ppti-14-302-03 en utilisant comme pivot la passerelle ssh ufr-info-p6.jussieu.fr et suffit d’éditer ~/.ssh/config en rajoutant :
```
Hostname 		ppti-14-302-03.ufr-info-p6.jussiepivotu.fr
Host 			pivot
User 			3531763
ProxyCommand	ssh 3531763@ssh.ufr-info-p6.jussieu.fr -W %h:%p
```


**TD4 : Containers et packaging**

**1 « Chroot » prison fragile**

L’utilisation de base de strace est de lancer une commande. Strace permet d’intercepter et d’enregistrer les appels système qui sont fait par la commande et les signaux qui sont reçu par la commande. 
Avec la commande 
```
strace  -o out ls 
```
strace lance ls et ecrit le résultat dans le fichier out.


ldd  est un utilitaire Unix affichant les bibliothèques logiciels utilisé par un programme. 
Par exemple, on peut lancer ldd /bin/bash


Sur la VM avec l’utilisateur root :
On crée le dossier chroot dans /root
On passe en mode root 

On crée le fichier /etc/schroot/chroot.d/trusty.conf que l’on édite comme ceci :
```
[trusty.conf]
directory=/root/chroot
users=root
```

On lance :
```
debootstrap –variant=buildd –arch=i386 trusty /root/chroot/ http://archive.ubuntu/ubuntu/
```
Ensuite on rentre dans le chroot avec
```
schroot -c trusty.conf
```
On crée un fichier 
```
touch f
```
On sort du chroot
```
exit
```
On remarque bien que le fichier f n’est pas présent à la racine.

Si on rentre à nouveau dans la prison puis qu’on install openvpn. Lors de l’installation le message d’erreur suivant apparaît :
```Failed to connect to socket /com/ubuntu/upstart : connection refused```




Lorsque que l’on fait par exemple ```ping -c 1 google.com``` dans la prison le ping fonctionne donc la connexion internet fonctionne.

Or si il y a bien une connexion internet mais quel ne vient pas d’ubuntu alors c’est que la configuration réseau utiliser est celle du système de base hors prison. Donc c’est systemd de debian qui est utiliser pour gérer la connexion réseau. D’où le fait que la prison ne soit bien isolé.


**2. les conteneurs lxc**


Pour créer le conteneur nommer « testconteneur » avec debian on utilise la commande :
```lxc-create -n test  -t  debian```

Ensuite pour lancer le conteneur on utilise :
```lxc-start -n test```

Puis, on definit  un mot de passe pour root :
```lxc-attach -n test – passwd root```

Après, on se connecte en root  avec :
```lxc-console -n test -t 0```

Enfin, on crée un nouvel utilisateur avec :
```
useradd mike
passwd mike
```


**3. Utilisation de gestion des paquetage**

Pour lister les paquetages installés, on utilise :
```
dpkg --get-selections
```
Pour lister les fichier d’un paquetage, on utilise,par exemple pour vim :
```
dpkg -L vim
```

Pour savoir quel paquetage contient le fichier /etc/sudoers on utilise :
```
dpkg -S /etc/sudoers
```
On obtient alors le retour suivant :
```sudo: /etc/sudoers```
Ceci signifie que le paquetage sudo contient le fichier etc/sudoers 


Avec la commande 
```dpkg -L bind9```
on observe les fichiers installés par le paquet bind9.
Le script de démarrage de bind est le fichier : /etc/init.d/bind9
qui lit le fichier de configuration /etc/default/bind9


```apt-get remove``` supprime les fichiers liés à l’installation d’un paquet mais ne supprime pas les fichiers de configuration associés au paquet.
```apt-clean``` permet de supprimer les paquets téléchargés encor stockés dans le dossier  
/var/cache/apt/archives/ qui fait office de cache.

```apt-get install``` <=> ```dpkg -i et apt-get -f install```

Cette deuxième commande permet d’installer les dépendances nécessaire à l’installation du paquet car dpkg ne gère pas les dépendances contrairement à apt-get.


```apt-get remove``` <=>  ```dpkg -r``` 

```apt-get purge``` <=> ```dpkg -P ```

**TD5**


**I Mise en place des containers et configuration**

On travail avec un Machine virtuel sous Debian Buster.

Après avoir télécharger et installer lxc, on désactive le service lxc-net avec la commande 
```
systemctl disable lxc-net 
```
Puis on s’assure que le service ne se relancera pas au démarrage avec 
```
systemctl mask lxc-net.
```
On désactive ce service car sinon toute la mise en place de l’interface réseau et sa configuration sera automatiquement faite par le script /usr/lib/x86_64-linux-gnu/lxc/lxc-net éxécuté au démarrage. Tout y est configurable à souhait pour peut qu’on y mette  USE_LXC_BRIDGE=«true».

Une fois le service désactiver on redémarre.

Ensuite on modifie le fichier /etc/lxc.default.conf en y écrivant ceci : 
```
lxc.net.0.type = veth
lxc.net.0.link = lxcbr0
lxc.net.0.flags = up
lxc.net.0.hwaddr = 00:16:3e:00:00:00
```

Les clés commençant par lxc.net permettent de définir les paramètre de l’interfaces réseau du des futurs conteneur créer. Le 0 permet de spécifier que les clés paramettront l’interface eth0 des futurs conteneurs.


-lxc.net.0.type = veth permet de spécifier que  la virtualisation est faite sur la base d’une connexion ethernet avec un câble branché d’un coté sur  l’interface veth de l’hôte de l’autre sur l’interface réseau n°0 du conteneur.

-lxc.net.0.link = lxcbr0 permet de spécifier le nom de l’interface réseau de l’hôte qui servira de pont   sur lequel seront seront brancher les interfaces veth 



-lxc.net.0.hwaddr = 00:16:3e:xx:xx:xx
permet de spécifier l’adresse MAC de l’interface réseau lxcbr0
Enfin, lxc.net.0.flags = up permet d’activer l’interface eth0 des conteneurs.



Il faut ensuite créer l’interface réseau lxcbr0.

Pour cela il suffit d’appliquer les commandes suivantes :

-On crée l’interface réseau lxcbr0 avec la commande :
```
ip link add dev lxcbr0 type bridge
```
-On associe à l’interface lxcbr0 une adresse ip et un masque avec la commande :
```
ip addr add 192.168.3.253/255.255.255.0 dev lxcbr0
```
-On associe à l’interface une adresse mac avec 
```
ip link set dev lxcbr0 address 00:16:3e:00:00:00
```
-On active l’interface avec 
```
ip link set dev lxcbr0 up
```
Avec cette configuration, malheureusement l’interface disparaîtra au redémarrage de la VM.
Pour que cela reste persistent il faut procéder autrement :

-On indique à systemd de créer l’interface lxcbr0 au démarrage en créant les fichiers suivants :

/etc/systemd/network/uplink.network que l’on édite avec :
```
[Match]
Name=eth0

[Network]
Bridge=lxcbr0
```
/etc/systemd/network/br0.netdev  que l’on édite avec :
```
[NetDev]
Name=lxcbr0
Kind=bridge
```
Au démarrage une fois que systemd aura créer l’interface, la commande ifup sera lancée. Cette dernière va lire dans le fichier /etc/network/interfaces pour configurer les interfaces reseau.
Dans notre cas on remplira ce fichier comme ceci :
```
auto lxbr0
iface lxcbr0 inet static
	address 192.168.253
	network 192.168.3.0
	netmask 255.255.255.0
	hwaddress ether 00:16:3e:00:00:00
```




On crée ensuite le container c1 sous Debian Buster avec la commande 
```
lxc-create -n c1 -t debian 
```
On le configure  via le fichier /var/lib/lxc/c1/config.
On y ajoute :
```
lxc.net.0.ipv4.address = 192.168.3.5/24
lxc.net.0.ipv4.gateway = 192.168.3.253
```
pour lui donner une adresse ip fixe et configurer sa passerelle.

On prépare c1 pour qu’il puis utiliser la commande ping en lui fournissant le paquet iputils-ping :
```
cp /var/cache/apt/archives/iputils-ping_3%3a20180629-2+deb10u1_amd64.deb /var/lib/lxc/c1/rootfs/var/cache/apt/archives/
```
On configure ensuite le par-feu avec iptables :
```
echo 1 > /proc/sys/net/ipv4/ip_forward 
```
Mettre un 1 dans ce fichier permet d’autoriser le forwarding

```
iptables -A FORWARD -i lxcbr0 -o eth0  ! -d  192.168.3.0/24 -j ACCEPT
```
Ici, on établit la règle qui que tous les paquets arrivant sur lxcbr0 sont forwarder via eth0 si ils n’ont pas pour destination le réseau 192.168.3.0/24


iptables peut utiliser des modules additionnels de correspondance de paquets. Ceux-ci peuvent être chargés  avec l'option -m ou --match, suivie du nom du module de correspondance.
```
iptables -A FORWARD -i lxcbr0 -o eth0 -m state –state ESTABLISHED,RELATED -j ACCEPT
```
Ici le module state est chargé. Les paramètre  ESTABLISHED,RELATED permertte respectivement de signifier que les paquets sont forwarder si ils sont associés à une connexion connue ou si ils appartiennent à une nouvelle connexion mais qui est associé à une connexion établie (ftp par exemple)

Enfin, 
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

permet d’ajouter un règle dans la table nat en postrouting qui dit que tous les paquets allants vers l’interface eth0  i.e. vers internet n’auront pas pour adresse source celle du réseau local de nos conteneur car comme il n’appartient pas à la même classe de réseau les paquet envoyés sur internet ne reviendraientt jamais .


	

Enfin par mesure de sécurité on peut redémarrer le service lxc avec 
```
systemctl restart lxc
```

Ensuite pour lancer le conteneur on utilise :
```
lxc-start -n c1
```
Ceci à pour effet d’activer l’interface réseau veth sur l’hôte

Puis, on définit  un mot de passe pour root :
```
lxc-attach -n c1 – passwd root
```
On se connecte à c1 :
```
lxc-console -n c1 -t 0
```

On install ping et on ping lxcbr0 et une adresse internet par exemple 78.254.0.62
```
apt-get install iputils-ping
ping -c2 192.168.3.253
ping -c2 78.254.0.62
```

Résumé des IPs:
lxcbr0		192.168.3.253
c1 		192.168.3.5


Enfin on stop le conteneur c1 :
```
lxc-stop -n c1
```
et on clone le conteneur c1 avec 
```
lxc-copy -n c1 -N c2
lxc-copy -n c1 -N c3
```
On attribue à c2 l’adresse IP static temporaire 192.168.3.6 en modifiant 
 /var/lib/lxc/c2/config

On redémarre c1 et c2 et on vérifie que c1 peut pinger c2 
```
ping -c2 192.168.3.6
```

Enfin on retire l’ip statique de c2 en modifiant  /var/lib/lxc/c2/config en retirant la ligne 
```lxc.net.0.ipv4.address = 192.168.3.6```



**II Mise en place  et configuration du serveur DHCP**


On modifie l’adresse mac de eth0 de c1  en modifiant  /var/lib/lxc/c1/config avec 
lxc.net.0.hwaddress= 00:16:3e:f5:e5:3e

On modifie l’adresse mac de eth0 de c2  en modifiant  /var/lib/lxc/c2/config avec 
lxc.net.0.hwaddress= 00:16:3e:f5:e5:3d

Pour résumer :
```
		IP 					Adresse mac

lxcrbr0  	192.168.3.253				00:16:00:00:00:00
c1		192.168.3.5				00:16:3e:f5:e5:3e
c2							00:16:3e:f5:e5:3d
```
Ensuite on installe isc-dhcp-server sur c1 avec 
```
apt-get install  isc-dhcp-server
```
on édite le ficher /etc/dhcp/dhcpd.conf de c1 avec :
```
default-lease-time 86400;
max-lease-time 172800;

subnet 192.168.3.0 netmask 255.255.255.0 {
 	range 192.168.3.128 192.168.3.192;  		#plage d’ip à attibuer
 	option domain-name-servers 192.168.0.254;	#DNS
 	option routers 192.168.3.253;			#passerel

 
# c1 ne doit pas s’attribuer d’ip car elle est déjà fixé dans /var/lib/lxc/c1/config

	host banni {						
		hardware ethernet 00:16:3e:f5:e5:3e;	#adresse mac de eth0 de c1
		deny booting;					
	}

	host client2 {						#c2 aura l’ip fixe 192.168.3.64
		hardware ethernet 00:16:3e:f5:e5:3d;	#adresse mac de eth0 de c2
		fixed-address 192.168.3.64;
	}

}

```
Ensuite en édite /etc/default/isc-dhcp-server de c1 en remplaçant
```INTERFACESv4= «»```
avec 
```INTERFACESv4= «eth0»```
pour informer le serveur sur  quelle interface il doit travailler.

On démarre ensuite c2 et on édite  son fichier /etc/network/interfaces avec :

```

auto lo 
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```
de même pour c3 en paramétrant  /var/lib/lxc/c3/config sans ipv4 statique et avec l’adresse MAC 00:16:3e:df:eb:04

On revient sur c1 pour modifier /etc/dhcp/dhcpd.conf  en rajoutant au début du fichier l’option
```
deny unknown-clients;
```
pour interdire les machines inconnues et également dans l’accolade de subnet
```
host client3 {						
	hardware ethernet 00:16:3e:f5:e5:3d;	#adresse mac de eth0 de c3
}
```
pour autoriser c3 à se connecter.

Ensuite on créer une machine c4
```
lxc-copy -n c3 -N c4
```
On relance lxc,c1,c2,c3 et on démarre c4
On revient sur la vm et on vérifie la configuration avec lxc-ls –fancy ce qui donne 
```
NAME 	STATE   	AUTOSTART GROUPS 	IPV4          	IPV6 	UNPRIVILEGED
c1   		RUNNING 	0         		-      		192.168.3.5   	-    	false        
c2   		RUNNING 	0         		-      		192.168.3.64  	-    	false        
c3   		RUNNING 	0        	 	-      		192.168.3.132 -    	false        
c4   		RUNNING 	0         		-      		-             	-   	false       
```
c4 est bien sans adresse ip.
Pour le parfeu de c2 on applique les commande suivantes :
```
iptables -P OUTPUT ACCEPT
```
Pour accepter le trafic sortant

```
iptables -A INPUT -p tcp -i eth0 --dport ssh -j ACCEPT
```
pour autoriser le ssh

```
iptables -I INPUT -i eth0 -p udp --dport 67:68 --sport 67:68 -j ACCEPT
```
pour autoriser le dhcp
```
iptables -P INPUT DROP
iptables -P FORWARD DROP
```
pour interdire le FORWARD et le trafic entrant.



**III Mise en place  et configuration du serveur DNS**

On remarque pour chaque machine que  lorsque l’on modifie /etc/resolv.conf et qu’on la rédémarre le fichier à annuler la modification. Les machines sont sous Debian Buster et lors du redémarrage c’est le serveur DHCP qui réécrit en dernier le fichier resolv.conf. Ainsi en modifiant simplement le fichier /etc/dhcp/dhcpd.conf de c1 comme ce ceci :
```
#On rappelle que c1 à pour adresse ip 192.168.3.5

deny unknown-clients;
default-lease-time 86400;
max-lease-time 172800;

subnet 192.168.3.0 netmask 255.255.255.0 {
 	range 192.168.3.128 192.168.3.192;  		
	option domain-name « asr.fr »;				#Nouvelle ligne
 	option domain-search « asr.fr »				#Nouvelle ligne
	option domain-name-servers 192.168.0.254;	
 	option routers 192.168.3.253;			

 
# c1 ne doit pas s’attribuer d’ip car elle est déjà fixé dans /var/lib/lxc/c1/config

	host banni {						
		hardware ethernet 00:16:3e:f5:e5:3e;	#adresse mac de eth0 de c1
		deny booting;					
	}

	host client2 {						#c2 aura l’ip fixe 192.168.3.64
		hardware ethernet 00:16:3e:f5:e5:3d;	#adresse mac de eth0 de c2
		fixed-address 192.168.3.64;
	}
	host client3 {						
		hardware ethernet 00:16:3e:f5:e5:3d;	#adresse mac de eth0 de c3
	}
}
```
On renomme les containers avec leur fichier /etc/hostname en c1,c2 et c3
Ensuite on édite le fichier /etc/resolve.conf de c1, avec :
```
domain asr.fr
search asr.fr
nameserver 192.168.3.55
```
Le contenue de ce dernier ne sera pas effacer au redémarrage car c1 est exclu du DHCP.
Enfin, on édite dans c1 /etc/bind.named.conf.local
```
zone «asr.fr» {
	type master
	file «/etc/bind/db.asr.fr»
}
```

et
/etc/bind/db.asr.fr :

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     c1.asr.fr. root.asr.fr. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      c1.asr.fr.
c2      IN      A       192.168.3.64
c3      IN      A       192.168.3.132
c1      IN      A       192.168.3.5
@       IN      AAAA    ::1
```
On redémarre bind9 sur c1.
On constate alors que 
```
ping -c2 c1.asr.fr
ping -c2 c2.asr.fr
ping -c2 c3.asr.fr
```
fonctionne correctement. De même pour c2 et c3.

En ce qui conserve le forwarding, si Bind9 ne trouve pas l'ip correspondant à l'url "pinger", par défaut il va 
exploiter la base de donné de la zone ".". Cette base de donnée se trouve à l'emplacement indiqué au début du fichier 
/etc/bind/named.conf.default-zones:
```
zone "." {
	type hint;
	file "/usr/share/dns/root.hints";
};

...

```
et si bind9 est à jour alors il trouvera l'ip associé à l'url.

Si l'on souhaite par exemple empécher bind9 d'utiliser cette base de données et forwarder sur un autre dns,
par exemple 8.8.8.8 (le dns de google), il suffit de rajouter au fichier /etc/bind/named.conf.options dans l'accolade de options :
```
forward only;
forwarders{
	8.8.8.8;
};

```

En ce qui concerne la résolution de nom inverse le shéma est le même.
Dans un premier temps on ajoute au fichier /etc/bind/named.conf.local:

```
zone "3.168.192.in-addr.arpa" {
        type master;
        file "/etc/bind/db.3.168.192.in-addr.arpa";

};
```
Puis on crée le fichier /etc/bind/db.3.168.192.in-addr.arpa que l'on édite comme ceci:
```
$TTL    604800
@       IN      SOA     c1.asr.fr. root.asr.fr. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      c1.asr.fr.
5       IN      PTR     c1.asr.fr.
64      IN      PTR     c2.asr.fr.
132     IN      PTR     c3.asr.fr.
```
On redémare bind9 et enfin on vérifie que la résolution inverse fonctionne avec la commande dig:
```
dig -x 192.168.3.5
dig -x 192.168.3.64
dig -x 192.168.3.132
```

Pour le serveur dns secondaire , on confgure c4 avec l'ip static 192.168.3.6 en modifiant
/var/lib/lxc/c4/config. On édite le fichier /etc/resolv.conf de c4 avec:
```
domain asr.fr
search asr.fr
nameserver 192.168.3.5
nameserver 192.168.3.6
```
On édite de même /etc/resolv.conf de c1 puis on installe bind9.

Ennsuite on configure le fichier /etc/dhcp/dhcpd.conf de c1 en rajoutant l'ip 192.168.3.6 à la ligne
```domain-name-servers``` pour que le serveur secondaire soit paramettré pour c2 et c3.

On édite alors /etc/bind/named.local en rajoutant la ligne ```notify yes;```
à la zone asr.fr et la zone 3.168.192.in-addr.arpa.

On rajoute les lignes à /etc/bind/db.asr.fr
```
 @      IN      NS      c4.asr.fr.
c4	IN	A	192.168.3.6
```
et à /etc/bind/db.3.168.192.in-addr.arpa
```
 @      IN      NS      c4.asr.fr.
 6      IN      PTR     c4.asr.fr.



```
On rajoute  à /etc/bind/named.conf.options ```allow-transfert {192.168.3.6}```
On se connecte à c4 pour y éditer le fichier named.conf.local exactement comme pour c1 en remplaçant
```type master;``` par ```type slave;``` et ```notify yes;``` par ```masters {192.168.3.5;};``` dans chaque zone.













