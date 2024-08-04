GLPI (Gestionnaire Libre de Parc Informatique) est un logiciel open source de gestion des services informatiques (ITSM) et de gestion des actifs informatiques (ITAM). Un serveur GLPI est un outil puissant pour la gestion des services et des actifs informatiques, offrant une solution intégrée pour l'inventaire, la gestion des incidents, la planification des changements, et bien plus encore, tout en permettant une automatisation et une personnalisation avancées.

Pour installer et configurer un serveur GLPI sur Debian 12 en ligne de commande, suivre les étapes ci-dessous :

### Pré-requis

Assurez-vous que votre système est à jour :
```bash
sudo apt update
sudo apt upgrade
```

Installez les dépendances nécessaires :
```bash
sudo apt install apache2 mariadb-server mariadb-client php php-mysql php-cli php-curl php-ldap php-imap php-mbstring php-xml php-gd php-zip wget unzip
```

### 1. Installation de GLPI

Téléchargez la dernière version de GLPI :
```bash
cd /tmp
wget https://github.com/glpi-project/glpi/releases/download/10.0.6/glpi-10.0.6.tgz
tar -xvzf glpi-10.0.6.tgz
sudo mv glpi /var/www/html/
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
```

Configurez Apache :
```bash
sudo nano /etc/apache2/sites-available/glpi.conf
```

Ajoutez les lignes suivantes dans le fichier :
```conf
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/glpi
    ServerName glpi.example.com

    <Directory /var/www/html/glpi>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/glpi_error.log
    CustomLog ${APACHE_LOG_DIR}/glpi_access.log combined
</VirtualHost>
```

Activez le site GLPI et redémarrez Apache :
```bash
sudo a2ensite glpi
sudo a2enmod rewrite
sudo systemctl restart apache2
```

### 2. Configuration de la base de données

Connectez-vous à MariaDB :
```bash
sudo mysql -u root -p
```

Créez une base de données et un utilisateur pour GLPI :
```sql
CREATE DATABASE glpi;
CREATE USER 'glpiuser'@'localhost' IDENTIFIED BY 'motdepasse';
GRANT ALL PRIVILEGES ON glpi.* TO 'glpiuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 3. Installation de GLPI via le navigateur

Ouvrez votre navigateur et accédez à `http://glpi.example.com`. Suivez les étapes pour terminer l'installation.

### 4. Synchronisation AD

1. Accédez à l'interface web de GLPI.
2. Allez dans **Configuration > Authentification > LDAP Directory**.
3. Cliquez sur **Ajouter** et remplissez les informations de votre serveur AD.

### 5. Gestion de parc : Inclusion des objets AD

1. Allez dans **Configuration > Plugins** et activez le plugin **FusionInventory**.
2. Installez et configurez les agents FusionInventory sur vos machines (utilisateurs, groupes, ordinateurs).

### 6. Gestion des incidents : Mise en place d'un système de ticketing

1. Allez dans **Administration > Entités** et créez une entité pour organiser vos tickets.
2. Configurez les profils et les groupes pour gérer les droits d'accès aux tickets.
3. Configurez les notifications pour les nouveaux tickets et les mises à jour de tickets dans **Configuration > Notifications**.

### 7. Accès et gestion à partir d'un client

Pour accéder à GLPI depuis un client :
1. Ouvrez un navigateur web et accédez à `http://glpi.example.com`.
2. Connectez-vous avec les identifiants de l'utilisateur.

Pour gérer GLPI via CLI (en utilisant GLPI Console) :
1. Connectez-vous au serveur GLPI via SSH.
2. Utilisez la console GLPI pour gérer les configurations :
```bash
cd /var/www/html/glpi
php bin/console glpi:ldap:synchronize_users
```

Ces étapes vous permettront d'installer et de configurer un serveur GLPI sur Debian 12 avec synchronisation AD, gestion de parc, système de ticketing et accès client.
