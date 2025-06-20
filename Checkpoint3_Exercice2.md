## Exercice 2 : Manipulations pratiques sur VM Linux  

### Partie 1 : Gestion des utilisateurs  

#### Q.2.1.1  

Pour créer un compte usage personnel, adduser afin d'avoir le /home + configuration de mot de passe.

`useradd alan`

![Creation-User](/Ressources/Exercice2/Q.2.1.1-1-Création-user.png)  

---

#### Q.2.1.2  

Etant donné qu'il est déconseillé d'utiliser le compte root de manière banaliser, je préconises :
- Ajout du compte **alan** au groupe sudo `sudo usermod -aG sudo alan

![Creation-group](/Ressources/Exercice2/Q.2.1.2-2-ajout-group.png)  

---

### Partie 2 : Configuration de SSH  
#### Q.2.2.1  

Pour la configuration SSH, les manipulations se font dans le dossier /etc/ssh/ et dans le fichier sshd_config.
La bonne pratique voudrait de modifier le fichier local_conf dans le dossier /etc/ssh/sshd_config.d/. Cela permet de modifier sa configuration sans changer le fichier originale.
Il faut penser à supprimer les # pour permettre l'execution de la ligne.

Pour la désactivation du compte root : PermitRootLogin no

La capture d'écran ci-dessous illustre aussi les réponses de la question Q.2.2.2 et Q.2.2.3

![SSH](/Ressources/Exercice2/Q.2.2.1-1-cancelroot-pubkey-nopasswd.png)  

#### Q.2.2.2  

Pour autoriser l'accès à distance à mon compte personnel alan : AllowUsers alan

#### Q.2.2.3  

Pour mettre en place une clé d'authentification et désactiver l'auth par mdp : 
- PubkeyAuthentification yes
- PasswordAuthentification no

---

### Partie 3 : Analyse du stockage  

#### Q.2.3.1  

Pour accéder à la liste des systemes de fichiers / volumes montés, entrez la commande `LSBLK`.

On peut voir sur la capture d'écran ci-dessous que les fichiers montés sont tous montés sur le disque SDA partionné en SDA1.
- la racine **/** sur le raid 1 et volume groupe cp3--vg-root avec le logiciel LVM (Logical Volume Manager)
- le **/boot** sur le raid 1 md0 et partition md0p1
- le **[SWAP]** ur le raid 1 et volume groupe cp3--vg-swap_1

![LSBLK](/Ressources/Exercice2/Q.2.3.1-1-LSBLK.png)  

---

#### Q.2.3.2  

Le systeme de stockage utilisé est un RAID-1, systeme de mirroring qui copy les données de la partition sda1.
Il utilise aussi lvm pour configurer les partitions.

#### Q.2.3.3  

Ouvrir virtualbox, selectionner la vm SRVLX01, storage, ajouter un disque dur, créer un disque 8GO, ajouter.
Relancer le serveur.

Lancer la commande `lsblk`. On peut appercevoir le nouveau disque sdb de 8GO.

Prenons un petit instantané...

En root, il faut suivre les commandes suivantes :
- fdisk /dev/sdb
- p
- enter
- enter
- enter
- t (pour lister les codes hexa)
- Soit 8E pour lvm soit FD pour raid autodetect
- w

![fdisk/dev/sdb](/Ressources/Exercice2/Q.2.3.1-1-LSBLK.png)  

![fdisk2](/Ressources/Exercice2/Q.2.3.3-2-lsblknewvolume.png)  

Pour ajouter ensuite le volume au raid1 ainsi que réparer le raid1, suivre les commandes ci-dessous.  

- mdadm --add/dev/md0 /dev/sdb1 (ajout du nouveau disque sdb1 à md0 raid1)  
- cat /proc/mdstat pour suivre la synchronisation  
- mdadm --detail /dev/md0 pour voir le statut "Clean" du raid. Voir capture ci dessous.  

![mdadm--detail](/Ressources/Exercice2/Q.2.3.3-3-lsblknewvolume.png)  

---

#### Q.2.3.4  

#### Q.2.3.5  

### Partie 4 : Sauvegardes  

#### Q.2.4.1  

Les rôles respectifs de Bareos sont :
- bareos-dir = Bareos Director, s'occupe de la planification, du controle et des taches de sauvegardes
- bareos-sd = Bareos Storage Daemon, s'occupe de sauvegarder et d'écrire sur les différents supports de stockage
- bareos-fd = Bareos File Daemon, s'occupe de la collecte des informations à sauvegarder et de les envoyer au Bareos Storage Daemon


### Partie 5 : Filtrage et analyse réseau  

#### Q.2.5.1  

#### Q.2.5.2  

#### Q.2.5.3  

#### Q.2.5.4  

### Partie 6 : Analyse de logs  

#### Q.2.6.1  

