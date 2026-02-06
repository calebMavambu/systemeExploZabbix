# systemeExploZabbix
ceci est notre travail de systeme d'explotation sur zabbix

# Zabbix Installation et Configuration

## Description
Ce projet explique l'installation et la configuration de **Zabbix**, un outil open source de supervision des systèmes informatiques.  
Zabbix permet de surveiller les serveurs, services, applications et équipements réseau en temps réel et d’envoyer des alertes automatiques en cas de problèmes.

---

## Prérequis
Avant de commencer, assurez-vous d'avoir :
- Un serveur avec **Ubuntu 20.04 ou 22.04**  
- Accès root ou sudo  
- **MariaDB/MySQL** installé  
- **Apache2 et PHP** installés  
- Connexion Internet pour télécharger les paquets

---

## Installation de Zabbix Server

1. **Mettre à jour le système**
```bash
sudo apt update && sudo apt upgrade -y
Ajouter le dépôt Zabbix

bash
Copier le code
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu20.04_all.deb
sudo dpkg -i zabbix-release_6.4-1+ubuntu20.04_all.deb
sudo apt update
Installer le serveur, l’agent et l’interface web

bash
Copier le code
sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-agent -y
Créer la base de données Zabbix

bash
Copier le code
sudo mysql -u root -p
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER 'zabbix'@'localhost' IDENTIFIED BY 'votre_mot_de_passe';
GRANT ALL PRIVILEGES ON zabbix.* TO 'zabbix'@'localhost';
FLUSH PRIVILEGES;
EXIT;
Importer le schéma initial

bash
Copier le code
zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix
Configuration du serveur Zabbix
Modifier le fichier /etc/zabbix/zabbix_server.conf :

conf
Copier le code
DBName=zabbix
DBUser=zabbix
DBPassword=votre_mot_de_passe
Redémarrer le serveur et l’agent :

bash
Copier le code
sudo systemctl restart zabbix-server zabbix-agent apache2
sudo systemctl enable zabbix-server zabbix-agent apache2
Vérifier que le serveur écoute sur le port 10051 :

bash
Copier le code
ss -tulnp | grep 10051
Configuration de l’interface web
Ouvrir un navigateur et accéder à :

arduino
Copier le code
http://IP_DU_SERVEUR/zabbix
Suivre l’assistant d’installation :

Vérifier les prérequis PHP

Configurer la connexion à la base de données

Créer un compte administrateur

Une fois connecté, vous pouvez :

Ajouter des hôtes et des templates

Configurer des triggers et alertes

Visualiser graphiques et tableaux de bord

Agents Zabbix sur les hôtes
Installer l’agent sur un serveur distant :

bash
Copier le code
sudo apt install zabbix-agent -y
Configurer l’agent (/etc/zabbix/zabbix_agentd.conf) :

conf
Copier le code
Server=IP_DU_SERVEUR
Hostname=Nom_de_l_hote
Redémarrer l’agent :

bash
Copier le code
sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent
Vérification
Connectez-vous à l’interface web et vérifiez que le serveur Zabbix est “Running”.

Assurez-vous que les agents apparaissent comme connectés.

Testez les alertes en simulant une panne (ex. arrêt d’un service).













ChatGPT peut faire des erreurs. Envisagez de vérifier les informations importantes.
