![logo](https://imtc.qccdn.fr/test/gestionnaires-de-mots-de-passe/zoom/keepass-password-safe_001.jpg)
# Création d'une Base de Données Sécurisée sur KeePass avec un Serveur Debian pour un Client Microsoft

## Présentation du Projet

Ce projet a pour objectif de mettre en place une base de données sécurisée utilisant KeePass, un gestionnaire de mots de passe open source, intégrée à un serveur Debian. L'idée est de centraliser la gestion des mots de passe pour une organisation, tout en garantissant une sécurité maximale des données sensibles. KeePass sera installé sur un serveur Debian, offrant ainsi une solution robuste et flexible pour le stockage et la gestion des mots de passe. Les utilisateurs finaux, utilisant des postes clients sous Microsoft, auront accès à leurs mots de passe via des configurations spécifiques qui leur permettent d'interagir avec le serveur KeePass hébergé sous Debian.

## Membres du Groupe

- **Damien**
- **Nicolas**
- **Jiani**

## Rôles des Membres du Groupe pendant le Premier Sprint


### Damien (Scrum Master)

Damien est responsable de la rédaction de la documentation pour les clients utilisant KeePass. Ses tâches incluent :

- Rédiger la documentation sur l'utilisation de KeePass par les clients.
- Assurer la qualité et la clarté des guides utilisateurs.
- Coordonner les efforts du sprint et faciliter les réunions de sprint.
- Garantir que l'équipe respecte les méthodologies agiles et les délais du projet.

### Nicolas (Product Owner)

Nicolas est chargé de la rédaction de la documentation sur l'installation du serveur. Ses tâches incluent :

- Rédiger des guides détaillés sur l'installation du serveur Debian pour héberger KeePass.
- Décrire les étapes de configuration nécessaires pour assurer la sécurité et l'efficacité du serveur.
- Recueillir et intégrer les retours des utilisateurs pour améliorer la documentation.
- Prioriser les fonctionnalités et les besoins du projet selon les feedbacks et les exigences des utilisateurs.

### Jiani

Jiani est responsable de la rédaction de la documentation sur l'installation du poste client. Ses tâches incluent :

- Rédiger des guides détaillés sur l'installation de KeePass sur les postes clients sous Microsoft.
- Fournir des instructions claires sur la configuration et l'utilisation de KeePass par les utilisateurs finaux.
- Collaborer avec Damien et Nicolas pour assurer la cohérence de la documentation.
- Tester les procédures d'installation pour s'assurer qu'elles sont faciles à suivre et sans erreurs.

## Rôles des Membres du Groupe pendant le Second Sprint

### Jiani (Scrum Master)

Jiani est responsable de la coordination du second sprint et de la gestion des outils de documentation. Ses tâches incluent :

- Coordonner les efforts du sprint et faciliter les réunions de sprint.
- Ajouter les informations du sprint de la semaine 2 dans la documentation.
- Intégrer Miro dans la documentation GitHub pour améliorer la collaboration visuelle et la planification.
- Assurer que l'équipe respecte les méthodologies agiles et les délais du projet.

### Damien (Product Owner)

Damien est chargé des aspects techniques liés à la génération et à la gestion des clés SSH. Ses tâches incluent :

- Générer les clés SSH via PuTTY.
- Sauvegarder les clés privée et publique de manière sécurisée.
- Ajouter la clé publique sur le serveur pour permettre l'accès sécurisé.
- Installer et configurer le protocole IOprotocoleExt sur le serveur.

### Nicolas

Nicolas est responsable de la configuration de l'authentification par clé SSH et de la création de tunnels sécurisés. Ses tâches incluent :

- Configurer l'authentification par clé SSH sur le serveur.
- Créer un tunnel SSH pour sécuriser les communications entre le client et le serveur.
- Collaborer avec Damien pour s'assurer que les clés SSH sont correctement générées et installées.
- Tester les configurations pour garantir qu'elles fonctionnent correctement et sans erreurs.

## Difficultés Rencontrées

Ajout clé publique sur serveur

## Solutions trouvées

Installation IOProtocleEXT

## Test Réalisés

Des tests ont été effectués pour évaluer l'efficacité et l'intégration de notre Base de Données Sécurisée sur KeePass avec un Serveur Debian pour un Client Microsoft. Les résultats ont été concluants :

- **Sécurité des Données** : Les tests ont confirmé que la base de données est bien sécurisée et les accès non autorisés sont empêchés.
- **Compatibilité** : L'installation et la configuration de KeePass sur un serveur Debian pour un client Microsoft ont été réussies sans problèmes de compatibilité.
- **Performance** : La performance du serveur et du client a été optimale, avec des temps de réponse rapides et une utilisation efficace des ressources.
- **Facilité d'Utilisation** : Les utilisateurs finaux ont trouvé les guides d'installation et d'utilisation clairs et faciles à suivre.
- **Stabilité** : Le système s'est avéré stable pendant les tests, avec une disponibilité continue et sans interruptions.

Les tests confirment que notre solution de Base de Données Sécurisée sur KeePass avec un Serveur Debian pour un Client Microsoft est fiable et efficace.

## Outils de Travail Collaboratif : Miro

Pour faciliter la collaboration et la planification visuelle, nous utilisons Miro. Cet outil permet à l'équipe de :

- Créer et partager des tableaux de bord visuels pour suivre l'avancement du projet.
- Brainstormer des idées et organiser des sessions de mind mapping.
- Planifier et structurer les sprints de manière interactive.
- Faciliter les discussions et les décisions en temps réel grâce à une interface visuelle intuitive.

Les tableaux Miro sont intégrés dans notre documentation GitHub pour un accès facile et une meilleure coordination au sein de l'équipe. Voici nos sprints :

![Tableau Miro](https://github.com/damdupre/keepass/blob/notice-poste-client/sprint1.png)
![Tableau Miro](https://github.com/damdupre/keepass/blob/notice-poste-client/sprint2.png)


---

Nous nous engageons à fournir une solution sécurisée et facile à utiliser pour la gestion des mots de passe grâce à KeePass et un serveur Debian pour des clients sous Microsoft. Chaque membre de l'équipe joue un rôle essentiel dans la réalisation de cet objectif, en apportant son expertise et en travaillant ensemble pour garantir le succès du projet.
