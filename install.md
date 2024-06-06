## Table des Matières

1. [Installation du serveur SSH](#installation-du-serveur-ssh)
2. [Gestion d'Open SSH](#gestion-dopenssh)
3. [Connexion depuis un poste client](#connexion-depuis-un-poste-client)
4. [En cas de coupure du serveur SSH](#en-cas-de-coupure-du-serveur-ssh)
5. [Configuration de Keepass sur le serveur SSH](#configuration-de-keepass-sur-le-serveur)
6. [Installation de la base de données sur le serveur](#installation-de-la-base-de-données-sur-le-serveur)
7. [Installation de KeePass](#installation-de-keepass)
8. [Création d'une Nouvelle Base de Données](#création-dune-nouvelle-base-de-données)
9. [Ajout de Mots de Passe](#ajout-de-mots-de-passe)
10. [Organisation des Mots de Passe](#organisation-des-mots-de-passe)
11. [Utilisation des Mots de Passe](#utilisation-des-mots-de-passe)
12. [Sauvegarde et Synchronisation](#sauvegarde-et-synchronisation)
13. [Conseils de Sécurité](#conseils-de-sécurité)
14. [FAQ](#faq)


# **Installation de la base sécurisée SSH**

## **Installation du serveur SSH**
Les serveurs Debian peuvent inclure dès leur création les applications et protocoles OpenSSH. Pour vérifier cela, vous pouvez rentrer la commande :

```
apt-cache policy openssh-server
```

Auquel cas le serveur devra répondre :

![verificationserveur.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/verificationserveur.png?raw=true)

Notez que vous pouvez également vérifier si l'installation est présente sur le système en recherchant le fichier de configuration du serveur avec la commande :
```
ls -al /etc/ssh/sshd_config
```

Ici, le serveur devra répondre :

![verifconfigserveur.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/verifconfigserveur.png?raw=true)

Maintenant que nous sommes certains que OpenSSH est bien installé, on peut passer à la gestion du serveur.

## **Gestion d'OpenSSH**
Il faut déjà s'assurer que le serveur est en cours de fonctionnement :
```
systemctl status sshd
```
S'il est bien actif, le serveur répondra: 

![verifserveuractif.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/verifserveuractif.png?raw=true)

Au besoin, les commandes pour le démarrer, le stopper et le redémarrer sont les suivantes :

```
systemctl start sshd
systemctl stop sshd
systemctl restart sshd
```

## **En cas de coupure du serveur SSH**
Ces commandes sont primordiales en cas de coupure inoportune du serveur SSH. Celui-ci peut notamment survenir dans les cas suivants :
- Extinction du serveur distant depuis la session SSH
- Redémarrage serveur qui ne se produit pas correctement
- Extinction du service SSH du serveur depuis la session SSH
- Coupure du port SSH à cause d'un pare-feu
- Erreur lors du changement de port d'écoute
- Coupure du réseau après mauvaise configuration


Il est nécessaire de s'assurer quel port est écouté par le serveur. Par défaut, celui-ci est configuré sur le **port 22 en TCP**

```
ss -lntp |grep "22"
```

## **Connexion depuis un poste client**
Maintenant que le serveur est configuré, on peut y connecter des postes-clients.

Depuis un client Windows, un logiciel est nécessaire pour établir la connexion avec un serveur. Le plus commun est [Putty](http://www.putty.org/) que vous pouvez télécharger. C'est un software développé pour windows permettant d'émuler un terminal ainsi qu'un client pour les protocoles SSH permettant des connexions directes.

Une fois téléchargé et exécuter, la fenêtre suivante va apparaître:

![puttyexe.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/puttyexe.png?raw=true)

Dans l'onglet SSH, on saisit l'adresse IP du serveur que l'on peut trouver avec la commande suivante :

```
ip a
```

On la trouvera dans le bloc suivant :

![afficherip.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/afficherip.png?raw=true)

Il faudra la rentrer dans le champ _"Host Name"_ et s'assurer que SSH est bien coché dans _"Connection type"_ . 
Un message d'erreur va apparaître : le client ne dispose pas de la clé du serveur SSH. Il va falloir accepter la clé. Cliquez sur "Oui".

![erreurputty.jpg](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/erreurputty.jpg?raw=true)

Un Shell va s'ouvrir dans lequel il vous sera demandé de vous identifier avec les identifiants du serveur Debian.
La liaison entre les deux appareils n'est pas sécurisée. Il faut désormais générer la clé SSH.

En installant _Putty_, _PuttyGen_ l'a également été. Lancez PuttyGen, assurez-vous de bien sélectionner le bon type de clé (SSH-RSA) et entrez votre passphrase. Cliquez sur "Generate".
Il faut enfin cliquer sur "Save public key" et "Save private key".

Il faut désormais envoyer la clé publique sur le serveur. 
<<<<<<< HEAD
=======

```
scp C:\Users\user\.ssh\clépublique admin@serveur:~/.ssh.authorized_keys
```

Une série de messages de confirmation valideront que la clé a bien été ajoutée au serveur.
Il sera désormais possible de se connecter au serveur via la commande :

```
ssh utilisateur@serveur
```

Il faut désormais renseigner _Putty_ sur l'endroit où se trouve notre clé privée. Lancez _Putty_ et renseignez l'IP du serveur (192.168.1.14). Dans la partie "_Connexion_">"_SSH_">"_Auth_" puis enfin sur "_Browse_" pour aller récupérer la clé. La connexion s'effectuera en cliquant sur "_Open_". Sélectionnez l'utilisateur où est stockée la clé et entrez la passphrase.

## Configuration de Keepass sur le serveur

Il est nécessaire de télécharger le plugin [IOProtocolExt](https://keepass.info/extensions/v2/ioprotocolext/IOProtocolExt-1.17.zip) pour permettre la connexion de Keepass en FSTP au serveur. 

Une fois installé, vous pourrez joindre le serveur via Keepass > synchroniser avec l'URL. Renseignez l'url suivante : "fstp://ssh utilisateur@serveur//home/user/keepass/bdd.kdbx" et complétez l'identifiant et le mot de passe sur serveur.
Voilà, Keepass est maitenant configuré sur le serveur. 

## Installation de la base de données sur le serveur

Après avoir créé la base de données sur le poste client, utilisez la commande 

```
scp C:\Users\user\Documents\basetest.kdbx admin@serveur:~/bddkeepass
```

Cela collera la base de données sur le serveur.


# Guide complet de l'installation keepass sur Poste client 


## Installation de KeePass

### Pour Windows

1. **Télécharger KeePass** :
   - Rendez-vous sur le site officiel de KeePass : [KeePass Downloads](https://keepass.info/download.html).
   - Téléchargez la version appropriée pour Windows (généralement KeePass 2.x).

2. **Installer KeePass** :
   - Exécutez le fichier téléchargé et suivez les instructions à l'écran pour installer KeePass.


## Création d'une Nouvelle Base de Données

1. **Ouvrir KeePass** :
   - Lancez l'application KeePass.

2. **Créer une Nouvelle Base de Données** :
   - Cliquez sur "File" dans la barre de menu.
   - Sélectionnez "New..." pour créer une nouvelle base de données.
   - Choisissez un emplacement sur le serveur pour enregistrer votre base de données et donnez-lui un nom.
   - Cliquez sur "Enregistrer" (Save).

3. **Définir un Mot de Passe Principal** :
   - Créez un mot de passe principal fort et mémorable.
   - Vous pouvez également utiliser une clé de fichier pour une sécurité supplémentaire en cliquant sur "Add key file".
   - Cliquez sur "OK".

4. **Configurer les Options de Sécurité** :
   - Vous pouvez ajuster les paramètres de sécurité, mais les valeurs par défaut sont généralement suffisantes.
   - Cliquez sur "OK" pour finaliser la création de la base de données.

## Ajout de Mots de Passe

1. **Ajouter une Nouvelle Entrée** :
   - Cliquez sur "Entries" puis "Add Entry..." ou utilisez le raccourci `Ctrl+I`.
   - Remplissez les champs requis (titre, nom d'utilisateur, mot de passe, URL).
   - Vous pouvez générer un mot de passe sécurisé en cliquant sur le bouton avec une clé.
   - Cliquez sur "OK" pour enregistrer l'entrée.

## Organisation des Mots de Passe

1. **Créer des Groupes** :
   - Cliquez avec le bouton droit de la souris dans le panneau de gauche sur "Groupes" puis "Add Group...".
   - Donnez un nom au groupe (par exemple, "Personnel", "Travail").
   - Cliquez sur "OK".

2. **Déplacer des Entrées** :
   - Glissez-déposez les entrées dans les groupes appropriés pour les organiser.

## Utilisation des Mots de Passe

1. **Trouver et Copier un Mot de Passe** :
   - Recherchez l'entrée souhaitée en utilisant la barre de recherche en haut.
   - Cliquez avec le bouton droit sur l'entrée et sélectionnez "Copy Password" (ou utilisez le raccourci `Ctrl+C`).
   - Collez le mot de passe là où il est nécessaire (`Ctrl+V`).

2. **Auto-Taper** :
   - Cliquez avec le bouton droit sur l'entrée et sélectionnez "Perform Auto-Type" pour remplir automatiquement le formulaire de connexion.

## Sauvegarde et Synchronisation

1. **Sauvegarde Manuelle** :
   - Sauvegardez régulièrement votre base de données en copiant le fichier `.kdbx` à un emplacement sécurisé (clé USB, disque dur externe).

2. **Synchronisation avec un Service Cloud** :
   - Utilisez des services comme OneDrive, Google Drive, ou Dropbox pour synchroniser votre base de données entre plusieurs appareils.
   - Placez simplement votre fichier `.kdbx` dans le dossier synchronisé de votre service cloud.

## Conseils de Sécurité

- **Utilisez un mot de passe principal fort et unique**.
- **Activez l'authentification à deux facteurs (2FA)** là où c'est possible.
- **Ne partagez pas votre base de données** ou votre mot de passe principal.
- **Effectuez des sauvegardes régulières** de votre base de données.
- **Gardez KeePass à jour** pour bénéficier des dernières améliorations de sécurité.

## FAQ

### Comment puis-je récupérer mon mot de passe principal si je l'ai oublié ?

Malheureusement, il n'est pas possible de récupérer un mot de passe principal oublié. Assurez-vous de le noter en lieu sûr.

### Puis-je utiliser KeePass sur plusieurs appareils ?

Oui, en utilisant des services de synchronisation cloud comme OneDrive, Google Drive, ou Dropbox.

### Comment puis-je importer des mots de passe depuis un autre gestionnaire de mots de passe ?

KeePass permet d'importer des mots de passe à partir de formats CSV ou d'autres gestionnaires. Allez dans "File" > "Import" et suivez les instructions.


![terminalputty.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/terminalputty.png?raw=true)
>>>>>>> 0bfa4da252d949085d5536877ac4d5cf11951d1b

```
scp C:\Users\user\.ssh\clépublique admin@serveur:~/.ssh.authorized_keys
```

Une série de messages de confirmation valideront que la clé a bien été ajoutée au serveur.
Il sera désormais possible de se connecter au serveur via la commande :

```
ssh utilisateur@serveur
```

Il faut désormais renseigner _Putty_ sur l'endroit où se trouve notre clé privée. Lancez _Putty_ et renseignez l'IP du serveur (192.168.1.14). Dans la partie "_Connexion_">"_SSH_">"_Auth_" puis enfin sur "_Browse_" pour aller récupérer la clé. La connexion s'effectuera en cliquant sur "_Open_". Sélectionnez l'utilisateur où est stockée la clé et entrez la passphrase.

## Configuration de Keepass sur le serveur

Il est nécessaire de télécharger le plugin [IOProtocolExt](https://keepass.info/extensions/v2/ioprotocolext/IOProtocolExt-1.17.zip) pour permettre la connexion de Keepass en FSTP au serveur. 

Une fois installé, vous pourrez joindre le serveur via Keepass > synchroniser avec l'URL. Renseignez l'url suivante : "fstp://ssh utilisateur@serveur//home/user/keepass/bdd.kdbx" et complétez l'identifiant et le mot de passe sur serveur.
Voilà, Keepass est maitenant configuré sur le serveur. 

## Installation de la base de données sur le serveur

Après avoir créé la base de données sur le poste client, utilisez la commande 

```
scp C:\Users\user\Documents\basetest.kdbx admin@serveur:~/bddkeepass
```

Cela collera la base de données sur le serveur.


# Guide complet de l'installation keepass sur Poste client 


## Installation de KeePass

### Pour Windows

1. **Télécharger KeePass** :
   - Rendez-vous sur le site officiel de KeePass : [KeePass Downloads](https://keepass.info/download.html).
   - Téléchargez la version appropriée pour Windows (généralement KeePass 2.x).

2. **Installer KeePass** :
   - Exécutez le fichier téléchargé et suivez les instructions à l'écran pour installer KeePass.


## Création d'une Nouvelle Base de Données

1. **Ouvrir KeePass** :
   - Lancez l'application KeePass.

2. **Créer une Nouvelle Base de Données** :
   - Cliquez sur "File" dans la barre de menu.
   - Sélectionnez "New..." pour créer une nouvelle base de données.
   - Choisissez un emplacement sur le serveur pour enregistrer votre base de données et donnez-lui un nom.
   - Cliquez sur "Enregistrer" (Save).

3. **Définir un Mot de Passe Principal** :
   - Créez un mot de passe principal fort et mémorable.
   - Vous pouvez également utiliser une clé de fichier pour une sécurité supplémentaire en cliquant sur "Add key file".
   - Cliquez sur "OK".

4. **Configurer les Options de Sécurité** :
   - Vous pouvez ajuster les paramètres de sécurité, mais les valeurs par défaut sont généralement suffisantes.
   - Cliquez sur "OK" pour finaliser la création de la base de données.

## Ajout de Mots de Passe

1. **Ajouter une Nouvelle Entrée** :
   - Cliquez sur "Entries" puis "Add Entry..." ou utilisez le raccourci `Ctrl+I`.
   - Remplissez les champs requis (titre, nom d'utilisateur, mot de passe, URL).
   - Vous pouvez générer un mot de passe sécurisé en cliquant sur le bouton avec une clé.
   - Cliquez sur "OK" pour enregistrer l'entrée.

## Organisation des Mots de Passe

1. **Créer des Groupes** :
   - Cliquez avec le bouton droit de la souris dans le panneau de gauche sur "Groupes" puis "Add Group...".
   - Donnez un nom au groupe (par exemple, "Personnel", "Travail").
   - Cliquez sur "OK".

2. **Déplacer des Entrées** :
   - Glissez-déposez les entrées dans les groupes appropriés pour les organiser.

## Utilisation des Mots de Passe

1. **Trouver et Copier un Mot de Passe** :
   - Recherchez l'entrée souhaitée en utilisant la barre de recherche en haut.
   - Cliquez avec le bouton droit sur l'entrée et sélectionnez "Copy Password" (ou utilisez le raccourci `Ctrl+C`).
   - Collez le mot de passe là où il est nécessaire (`Ctrl+V`).

2. **Auto-Taper** :
   - Cliquez avec le bouton droit sur l'entrée et sélectionnez "Perform Auto-Type" pour remplir automatiquement le formulaire de connexion.

## Sauvegarde et Synchronisation

1. **Sauvegarde Manuelle** :
   - Sauvegardez régulièrement votre base de données en copiant le fichier `.kdbx` à un emplacement sécurisé (clé USB, disque dur externe).

2. **Synchronisation avec un Service Cloud** :
   - Utilisez des services comme OneDrive, Google Drive, ou Dropbox pour synchroniser votre base de données entre plusieurs appareils.
   - Placez simplement votre fichier `.kdbx` dans le dossier synchronisé de votre service cloud.

## Conseils de Sécurité

- **Utilisez un mot de passe principal fort et unique**.
- **Activez l'authentification à deux facteurs (2FA)** là où c'est possible.
- **Ne partagez pas votre base de données** ou votre mot de passe principal.
- **Effectuez des sauvegardes régulières** de votre base de données.
- **Gardez KeePass à jour** pour bénéficier des dernières améliorations de sécurité.

## FAQ

### Comment puis-je récupérer mon mot de passe principal si je l'ai oublié ?

Malheureusement, il n'est pas possible de récupérer un mot de passe principal oublié. Assurez-vous de le noter en lieu sûr.

### Puis-je utiliser KeePass sur plusieurs appareils ?

Oui, en utilisant des services de synchronisation cloud comme OneDrive, Google Drive, ou Dropbox.

### Comment puis-je importer des mots de passe depuis un autre gestionnaire de mots de passe ?

KeePass permet d'importer des mots de passe à partir de formats CSV ou d'autres gestionnaires. Allez dans "File" > "Import" et suivez les instructions.


![terminalputty.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/terminalputty.png?raw=true)
