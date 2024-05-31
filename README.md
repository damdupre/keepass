<div align="center">![logo](https://imtc.qccdn.fr/test/gestionnaires-de-mots-de-passe/zoom/keepass-password-safe_001.jpg)</div>
## Membre du staff
Mr Jiani carel BATCHI  
Mr Nicolas TOUREAU Procuct owner (s1) scrum master (s2)     
Mr Damien DUPRÉ scrum master (s1) product owner (s2)

## Le projet Keepass
Keepass est un gestionnaire de mot de passe open-source. 
Son principe est très simple : KeePass sauvegarde tous vos mots de passe dans une base de données qui lui est propre et qui est en réalité un fichier chiffré (« crypté »).

Cette base de données n’est alors accessible que grâce à votre mot de passe principal, le seul que vous avez à retenir et que vous aurez préalablement judicieusement choisi.

Nous avons fait un serveur debian, sur lequel nous avons fait une connexion SSH par clé sécurisée pour pouvoir avoir accés à la base de données du logiciel keepass.

### Nos probléme
La mise en place du serveur debian  avec la clé ssh nous a prit pas mal de temps.
En effet nous avons essayer pendant un moment d'avoir une connexxion SSh à distance sur le serveur debian fait sur le promox de la wild .
Nous avons finalement fait une machine win 10 comme client sur ce promox.

