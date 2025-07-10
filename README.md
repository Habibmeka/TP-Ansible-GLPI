# README – Déploiement de GLPI et FusionInventory

## Objectif

Automatiser l’installation et la configuration de GLPI ainsi que la mise en place de l’inventaire automatique via FusionInventory.

---

## 1. Déploiement de GLPI avec Ansible

### Prérequis

- OS cible : Debian
- Serveur web : Apache 2
- Base de données : MariaDB
- PHP et modules requis
- Domaine : glpi.local
- SSL : certificat auto-signé

### Organisation des fichiers

- Inventaire Ansible
- Playbook principal : `/etc/ansible/playbooks/glpi_server.yml`
- Variables : `group_vars/glpi_server.yml`

### Processus d’installation

1. Mise à jour des paquets
2. Installation des dépendances : Apache, MariaDB, PHP
3. Activation et démarrage des services
4. Sécurisation de MariaDB
   - Changement du mot de passe root
   - Création de la base `glpidb`
   - Création de l’utilisateur `glpiuser` avec privilèges limités
5. Téléchargement et installation de GLPI
6. Attribution des permissions (`www-data`)
7. Activation des modules Apache (`rewrite`, `ssl`)
8. Génération d’un certificat SSL auto-signé
9. Création et activation du VirtualHost SSL
10. Redémarrage d’Apache

### Bonnes pratiques de sécurité

- Restreindre la connexion root à l’hôte local
- Utiliser des mots de passe robustes
- Restreindre SSH, activer UFW et Fail2ban
- En production, privilégier Let's Encrypt

---

## 2. Installation et configuration de FusionInventory

### Installation du plugin FusionInventory sur GLPI

1. Télécharger le plugin :

```bash
wget https://github.com/fusioninventory/fusioninventory-for-glpi/releases/download/glpi10.0.6%2B1.1/fusioninventory-10.0.6+1.1.tar.bz2
