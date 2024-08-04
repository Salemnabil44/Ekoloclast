## Création d'une VM Serveur Linux Debian mise sur le domaine AD accessible en SSH

Création d'une VM Serveur Linux Debian mise sur le domaine AD accessible en SSH 

Installer un serveur Debian sur VirtualBox est un processus simple mais implique plusieurs étapes. Voici les étapes détaillées à suivre :

### Étape 1 : Création d'un Serveur Debian

#### Prérequis

- **VirtualBox**: Assurez-vous d'avoir VirtualBox installé sur votre machine. Vous pouvez le télécharger depuis [le site officiel de VirtualBox](https://www.virtualbox.org/).
- **ISO Debian 12**: Téléchargez l'image ISO de Debian depuis [le site officiel de Debian](https://www.debian.org/distrib/).

#### Étapes d'Installation

1. **Lancer VirtualBox**:
   - Ouvrez VirtualBox.

2. **Créer une Nouvelle Machine Virtuelle**:
   - Cliquez sur le bouton `New` ou `Nouveau`.
   - Entrez un nom pour votre VM, par exemple `DebianServer`.
   - Cliquez sur `Next`.

3. **Configurer la Mémoire et le Disque Dur**
   - Mémoire (RAM): Allouez au moins 4 - 8 Go de RAM. Pour de meilleures performances, vous pouvez allouer plus de mémoire en fonction des ressources de votre machine hôte.
   - CPU: 1-2
   - Disque Dur: Sélectionnez "Créer un disque dur virtuel maintenant". Sélectionnez la taille de votre disque dur entre 40-60 Go. Cliquez sur `Suivant` puis `Finish`.

4. **Démarrer la Machine Virtuelle**:
   - Cliquez sur `Start`.
   - La VM va démarrer et lancer l'installation de Debian depuis l'ISO.

5. **Installation de Debian**:
   - Sélectionnez `Install` et appuyez sur `Enter`.
   - Choisissez la langue, le pays et le clavier.
   - Configurez le réseau en entrant un nom pour le serveur.
   - Définissez le mot de passe du superutilisateur `root`.
   - Créez un utilisateur standard.
   - Sélectionnez le fuseau horaire.
   - Partitionnez le disque. Pour une installation de base, choisissez `Guided - use entire disk`.
   - Sélectionnez le disque à partitionner et confirmez les modifications.
   - Laissez l'installateur copier les fichiers sur le disque dur.
   - Configurez l'outil de gestion des paquets. Si vous n'avez pas de miroir spécifique, utilisez les paramètres par défaut.
   - Sélectionnez les logiciels à installer. Pour un serveur de base, vous pouvez décocher toutes les options sauf `standard system utilities` et `SSH server`.
   - Installez le chargeur de démarrage GRUB.
   - Redémarrez la VM.

### Étape 2 : Mise dans le Domaine par le Biais d'une Connexion SSH

#### 2.1 Configurer l'Adresse IP du Serveur Debian

Pour configurer une adresse IP statique et ajouter un serveur DNS sans spécifier de passerelle (gateway) dans le fichier `/etc/network/interfaces` sur votre serveur Debian, vous pouvez modifier la section de l'interface `enp0s3` comme suit :

1. **Ouvrir le Fichier de Configuration :**
   ```bash
   sudo nano /etc/network/interfaces
   ```

2. **Modifier la Configuration de l'Interface `enp0s3` :**
   Remplacez la section actuelle concernant `enp0s3` par une configuration statique avec les informations nécessaires. Voici un exemple de configuration :
   ```plaintext
   # The primary network interface
   allow-hotplug enp0s1
   iface enp0s1 inet static
       address 192.168.0.7
       netmask 255.255.0.0
       dns-nameservers 192.168.0.4
   ```

3. **Enregistrer les Modifications et Quitter l'Éditeur :**
   - Pour `nano`, appuyez sur `Ctrl + X`, puis `Y`, et enfin `Entrée` pour enregistrer et quitter.
   - Pour `vim`, appuyez sur `Esc`, puis tapez `:wq` et appuyez sur `Entrée`.

4. **Redémarrer le Service Réseau :**
   Pour appliquer les modifications, redémarrez le service réseau avec la commande suivante :
   ```bash
   sudo systemctl restart networking
   ```

5. **Vérifier la Nouvelle Configuration :**
   Utilisez les commandes suivantes pour vérifier que l'adresse IP et le serveur DNS ont bien été configurés :
   ```bash
   ip addr show enp0s1
   ```

   Pour vérifier la configuration DNS :
   ```bash
   systemd-resolve --status
   ```

En suivant ces étapes, vous avez configuré votre adresse IP statique et spécifié le serveur DNS pour votre interface `enp0s3`. Pensez à configurer la carte réseau en réseau interne pour la suite de notre exercice.

#### 2.2 Connexion au Domaine via SSH

**Sur le Serveur Debian 12**

1. **Installer le Serveur SSH (si ce n'est pas déjà fait) :**
   ```bash
   sudo apt update
   sudo apt install openssh-server
   ```

2. **Vérifier que le Serveur SSH est en Cours d'Exécution :**
   ```bash
   sudo systemctl status ssh
   ```

   Si le serveur SSH n'est pas en cours d'exécution, vous pouvez le démarrer :
   ```bash
   sudo systemctl start ssh
   sudo systemctl enable ssh
   ```

**Sur le Serveur Windows Server 2022**

1. **Installer le Client OpenSSH (si ce n'est pas déjà fait) :**
   - Ouvrez `Paramètres`.
   - Allez dans `Applications`.
   - Cliquez sur `Fonctionnalités facultatives`.
   - Cliquez sur `Ajouter une fonctionnalité`.
   - Trouvez et sélectionnez `Client OpenSSH`, puis cliquez sur `Installer`.

2. **Ouvrir PowerShell ou l'Invite de Commandes :**
   - Recherchez `PowerShell` ou `Invite de commandes` dans le menu Démarrer et ouvrez-le.

3. **Utiliser la Commande SSH pour se Connecter au Serveur Debian :**
   ```bash
   ssh utilisateur@192.168.0.7
   ```
   Remplacez `utilisateur` par votre nom d'utilisateur sur le serveur Debian et `ip_du_serveur_debian` par l'adresse IP du serveur Debian.

En suivant ces étapes, vous devriez être en mesure d'établir une connexion SSH entre votre serveur Windows Server 2022 et votre serveur Debian 12.
