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

### Partie 3 : Analyse du stockage  

#### Q.2.3.1  

#### Q.2.3.2  

#### Q.2.3.3  

#### Q.2.3.4  

#### Q.2.3.5  

### Partie 4 : Sauvegardes  

#### Q.2.4.1  

### Partie 5 : Filtrage et analyse réseau  

#### Q.2.5.1  

#### Q.2.5.2  

#### Q.2.5.3  

#### Q.2.5.4  

### Partie 6 : Analyse de logs  

#### Q.2.6.1  

