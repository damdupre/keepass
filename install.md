## **Installation de la base sécurisée SSH**

**I. Installation du serveur SSH**
Les serveurs Debian peuvent inclure dès leur création les applications et protocoles OpenSSH. Pour vérifier cela, vous pouvez rentrer la commande :

```
apt-cache policy openssh-server
```

Auquel cas le serveur devra répondre :

![verificationserveur.png]

Notez que vous pouvez également vérifier si l'installation est présente sur le système en recherchant le fichier de configuration du serveur avec la commande :
```
ls -al /etc/ssh/sshd_config
```

Ici, le serveur devra répondre :

![verifconfigserveur.png]

Maintenant que nous sommes certains que OpenSSH est bien installé, on peut passer à la gestion du serveur.

**II. Gestion d'OpenSSH**
Il faut déjà s'assurer que le serveur est en cours de fonctionnement :
```
systemctl status sshd
```
S'il est bien actif, le serveur répondra: 

![verifserveuractif.png]

Au besoin, les commandes pour le démarrer, le stopper et le redémarrer sont les suivantes :

```
systemctl start sshd
systemctl stop sshd
systemctl restart sshd
```
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

**III. Connexion depuis un poste client**
Maintenant que le serveur est configuré, on peut y connecter des postes-clients.

Depuis un client Windows, un logiciel est nécessaire pour établir la connexion avec un serveur. Le plus commun est [Putty](http://www.putty.org/) que vous pouvez télécharger. C'est un software développé pour windows permettant d'émuler un terminal ainsi qu'un client pour les protocoles SSH permettant des connexions directes.

Une fois téléchargé et exécuter, la fenêtre suivante va apparaître:

![puttyexe.png]

Dans l'onglet SSH, on saisit l'adresse IP du serveur que l'on peut trouver avec la commande suivante :

```
ip a
```

On la trouvera dans le bloc suivant :

![[afficherip.png](https://github.com/damdupre/keepass/blob/notice-install/screen_installmd/afficherip.png?raw=true)

Il faudra la rentrer dans le champ _"Host Name"_ et s'assurer que SSH est bien coché dans _"Connection type"_ . 
Un message d'erreur va apparaître : le client ne dispose pas de la clé du serveur SSH. Il va falloir accepter la clé. Cliquez sur "Oui".

![erreurputty.jpg]

Un Shell va s'ouvrir dans lequel il vous sera demandé de vous identifier avec les identifiants du serveur Debian.

![terminalputty.png]

Le poste client est désormais connecté au serveur SSH.

