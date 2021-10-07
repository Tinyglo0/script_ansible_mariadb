# Préambule

Ce projet a été crée dans un but purement pédagogique. Sa finalité est d'intégrer des utilisateurs depuis un fichier .CSV au sein d'un serveur MariaDB et de leurs permettre de créeer autant de bases de données qu'ils le souhaitent commençant par leur nom de famille suivi d'un underscore.

Exemple: L'utilisateur ayant pour identifiant DUPONT pourra créer autant de bases de données du moment qu'elles commencent par DUPONT_
Lors de l'execution du script (ou du playbook) de suppression, toutes ses bases de données seront supprimées.

Le projet a été conçu et testé sur une Debian 10 avec un serveur MariaDB 10.5.12.

# Prérequis

Afin de lancer il est nécessaire s'assurer de:
-  Pouvoir executer des commandes avec une élévation de privilèges (sudo)
- Avoir Ansible d'installé  (cf https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-debian pour l'installation sur Debian)
- Avoir le module read_csv d'installé: ``` ansible-galaxy collection install community.general ```
- Avoir intégré les adresses IP du ou des serveurs MySQL les dans le fichier d'inventaire situés dans /inventory/hosts

### Personnalisation des variables

Il existe 3 fichiers contenant des variables pouvant être personnalisées:
- le fichier hosts situé dans le dossier inventory: Il contient les adresses des serveurs à atteindre ainsi que l'utilisateur avec lequel on souhaite éxecuter le script.
- le fichier all.yml situé dans inventory/group_vars: Il contient le nom des bases de données à exclure; celles qui ne seront pas prises en compte lors de la suppression (par défaut celles utilisées pour le bon fonctionnement de MySQL).
- le fichier variables_connexion.yml à la racine du projet: Il est utilisé pour se connecter au serveur de base de données distant ainsi que le nom du fichier csv contenant la liste des utilisateurs.

### Execution du playbook Ansible

Le playbook peut être utilisé de deux manières:
1. En éxecutant les fichier ajout_utilisateurs.sh et suppression_utilisateurs.sh pour respectivement ajouter ou supprimer les utilsateurs à partir du fichiers hosts.csv.
2. En executant la commande ``` ansible-playbook -i inventory/hosts parse_ajout_utilisateurs.yml ``` pour l'ajout ou parse_suppression_utilisateurs.yml pour la suppression d'utilisateurs.
