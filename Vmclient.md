Création d'une VM client
 - Sur le domaine AD
 - Avec un compte utilisateur ayant un accès SSH sur le serveur Linux

### 1. Préparation de l'Infrastructure

1. **Configurer un hôte d'hyperviseur (comme Hyper-V, VMware, ou VirtualBox)** :
   - Assurez-vous que l'hôte d'hyperviseur est correctement configuré et que vous pouvez créer des machines virtuelles (VM).

### 2. Création d'une VM Client

1. **Créer une nouvelle machine virtuelle sur l'hôte d'hyperviseur** :
   - **Hyper-V** :
     - Ouvrez le Gestionnaire Hyper-V.
     - Cliquez sur "Nouvelle" puis sur "Machine Virtuelle".
     - Suivez l'assistant pour configurer la VM (nom, emplacement, génération, mémoire, disque dur virtuel, etc.).
   - **VMware** :
     - Ouvrez le VMware vSphere Client.
     - Cliquez sur "Create a New Virtual Machine".
     - Suivez l'assistant pour configurer la VM.
   - **VirtualBox** :
     - Ouvrez VirtualBox.
     - Cliquez sur "New".
     - Suivez l'assistant pour configurer la VM.

2. **Installer un système d'exploitation sur la VM** :
   - Insérez le média d'installation de votre système d'exploitation (par exemple, Windows 10, Ubuntu, etc.).
   - Démarrez la VM et suivez les instructions pour installer le système d'exploitation.

### 3. Joindre la VM au Domaine AD

1. **Configurer les paramètres réseau** :
   - Assurez-vous que la VM peut communiquer avec le contrôleur de domaine (DC).
   - Configurez une adresse IP fixe ou utilisez DHCP selon votre configuration réseau.

2. **Joindre la VM au domaine AD** :
   - **Windows** :
     - Ouvrez les "Paramètres Système".
     - Allez dans "Système" -> "Informations Système" -> "Paramètres de Nom de l'Ordinateur, Domaine et Groupe de Travail".
     - Cliquez sur "Modifier" et sélectionnez "Domaine".
     - Entrez le nom de domaine AD (par exemple, `ekoloclast.lan`) et fournissez les informations d'identification d'un compte ayant les permissions nécessaires pour joindre des machines au domaine.
   - **Linux** :
     - Installez les paquets nécessaires :
       ```bash
       sudo apt update
       sudo apt install realmd sssd sssd-tools samba-common packagekit adcli
       ```
     - Rejoignez le domaine AD :
       ```bash
       sudo realm join --user=admin_user ekoloclast.lan
       ```

### 4. Créer un Compte Utilisateur sur le Domaine AD

1. **Utiliser le Gestionnaire Utilisateurs et Ordinateurs Active Directory (ADUC)** :
   - Ouvrez "Utilisateurs et Ordinateurs Active Directory".
   - Naviguez jusqu'à l'OU où vous souhaitez créer l'utilisateur.
   - Cliquez droit et sélectionnez "Nouveau" -> "Utilisateur".
   - Remplissez les informations requises (nom, nom d'utilisateur, mot de passe, etc.).
   - Assurez-vous que l'utilisateur est configuré pour ne pas changer son mot de passe lors de la première connexion si vous le souhaitez.

### 5. Configurer l'Accès SSH sur le Serveur Linux

1. **Installer et configurer OpenSSH sur le serveur Linux** :
   - Installez OpenSSH :
     ```bash
     sudo apt update
     sudo apt install openssh-server
     ```
   - Vérifiez que le service SSH est en cours d'exécution :
     ```bash
     sudo systemctl status ssh
     ```

2. **Configurer les autorisations pour l'utilisateur AD** :
   - Modifiez la configuration SSH pour autoriser les utilisateurs AD :
     ```bash
     sudo nano /etc/ssh/sshd_config
     ```
   - Ajoutez ou modifiez les lignes suivantes pour permettre les utilisateurs de domaine :
     ```
     UsePAM yes
     AllowGroups sshusers
     ```
   - Créez le groupe `sshusers` et ajoutez l'utilisateur AD au groupe :
     ```bash
     sudo groupadd sshusers
     sudo usermod -aG sshusers 'DOMAINE\utilisateur'
     ```
   - Redémarrez le service SSH :
     ```bash
     sudo systemctl restart ssh
     ```

### 6. Test de la Configuration

1. **Tester la connexion SSH** :
   - Depuis la VM ou une autre machine ayant accès au serveur Linux, essayez de vous connecter via SSH avec les informations d'identification AD :
     ```bash
     ssh 'DOMAINE\utilisateur'@adresse_ip_du_serveur
     ```

En suivant ces étapes, vous devriez être en mesure de créer une VM client sur le domaine AD et de configurer un utilisateur ayant un accès SSH sur le serveur Linux. Si vous avez des questions ou des problèmes spécifiques, n'hésitez pas à demander de l'aide supplémentaire.
