PfSense est une distribution open-source basée sur FreeBSD, spécialisée dans la création de pare-feu et de routeurs. Utilisée principalement pour sécuriser et gérer des réseaux, elle offre une interface web conviviale pour configurer des fonctionnalités avancées comme le filtrage de paquets, la traduction d'adresses réseau (NAT), la gestion de VPN, la détection d'intrusions, et bien plus encore. pfSense est réputée pour sa robustesse, sa flexibilité, et sa capacité à remplacer des équipements réseau coûteux, tout en restant accessible pour les petites entreprises, les professionnels et les utilisateurs expérimentés.

## Installation Pfsense

Installer pfSense sur VirtualBox est une excellente manière de créer un pare-feu ou un routeur virtuel pour expérimenter ou configurer un réseau. Voici les étapes à suivre pour l'installer :

### 1. **Télécharger pfSense et VirtualBox**
   - **pfSense** : Téléchargez l'image ISO de pfSense depuis le site officiel [pfSense.org](https://www.pfsense.org/download/). Choisissez l'architecture correspondant à votre machine (généralement AMD64) et le format "ISO Installer".
   - **VirtualBox** : Téléchargez et installez Oracle VirtualBox depuis le site [VirtualBox.org](https://www.virtualbox.org/).

### 2. **Créer une nouvelle machine virtuelle dans VirtualBox**
   1. **Ouvrez VirtualBox** et cliquez sur **"Nouvelle"** pour créer une nouvelle machine virtuelle.
   2. **Nom** : Donnez un nom à votre machine virtuelle, par exemple "pfSense".
   3. **Type** : Sélectionnez "BSD".
   4. **Version** : Choisissez "FreeBSD (64-bit)".

<img width="540" alt="Capture d’écran 2024-08-08 à 14 51 28" src="https://github.com/user-attachments/assets/74ba4b2f-e2d2-43f2-8214-5bf7c52f60c0">
 
   5. **Mémoire** : Allouez au moins 1 Go de RAM. Vous pouvez augmenter cette valeur en fonction de vos besoins et des ressources de votre système hôte.
   6. **Disque dur** : Choisissez une taille d'au moins 10 Go (vous pouvez ajuster selon vos besoins).

### 3. **Configurer les paramètres réseau**
   - Allez dans les **paramètres** de la machine virtuelle (sélectionnez-la, puis cliquez sur "Configuration").
   - **Adaptateurs Réseau** : Configurez deux interfaces réseau :
     - **Adaptateur 1** : Réseau NAT (cela permettra à pfSense d'accéder à Internet).
     - **Adaptateur 2** : Réseau interne (choisissez "Internal Network" ou "Réseau Interne"). Cela servira de LAN pour vos machines virtuelles connectées à pfSense.

### 4. **Monter l'image ISO de pfSense**
   - Dans les paramètres de la machine virtuelle, allez dans l'onglet **Stockage**.
   - Cliquez sur **Vide** sous "Contrôleur : IDE" et ensuite sur l'icône de disque à droite.
   - Choisissez "Choisir un fichier de disque" et sélectionnez l'image ISO de pfSense que vous avez téléchargée.

### 5. **Démarrer la machine virtuelle et installer pfSense**
   1. Cliquez sur **Démarrer** pour lancer la machine virtuelle.
   2. Suivez les instructions à l'écran pour installer pfSense :
      - Appuyez sur "Enter" pour démarrer l'installation.
      - Choisissez "Install" dans le menu de démarrage.
      - Sélectionnez votre configuration clavier.
      - Lorsque vous êtes invité à partitionner le disque, choisissez "Auto (UFS)" ou "Auto (ZFS)" selon vos préférences.
      - Une fois l'installation terminée, retirez l'ISO (via le menu "Périphériques > Lecteur optique > Retirer le disque de l'invité" dans VirtualBox) et redémarrez la machine.

## Configuration Pfsense 

### 6. **Configurer pfSense**
   - Après le redémarrage, pfSense détectera et configurera automatiquement les interfaces réseau. Vous devrez attribuer les interfaces WAN et LAN :
     - **WAN** : Correspond généralement à l'Adaptateur 1 (NAT).
     - **LAN** : Correspond généralement à l'Adaptateur 2 (Réseau Interne).
   - Suivez les instructions pour finaliser la configuration.
   - Configurer l'adresse IP LAN qui sera dans notre projet l'adresse 192.168.0.1 (Voir plan d'adressage en annexe).

<img width="475" alt="Capture d’écran 2024-08-08 à 14 54 43" src="https://github.com/user-attachments/assets/7581b25a-bc59-43f5-8c89-7d45206f42f1">

### 7. Pour que les serveurs ou autres machines virtuelles puissent accéder à Internet via pfSense, il est crucial de configurer la passerelle par défaut sur ces machines.

1. Obtenez l'adresse IP de la passerelle (LAN de pfSense)
Lorsque vous avez configuré pfSense, l'adresse IP attribuée à l'interface LAN est la suivante 192.168.0.1. Elle devient la passerelle par défaut pour tout appareil connecté au réseau LAN interne.

2. Configurer la passerelle par défaut sur les serveurs ou machines virtuelles

Sous Windows :
Allez dans Panneau de configuration > Réseau et Internet > Centre Réseau et partage > Modifier les paramètres de la carte.
Faites un clic droit sur l'interface réseau correspondant à votre connexion LAN et choisissez Propriétés.
Sélectionnez Protocole Internet version 4 (TCP/IPv4) et cliquez sur Propriétés.
Cochez Utiliser l'adresse IP suivante et entrez une adresse IP statique dans la plage du réseau 192.168.0.4, avec un masque de sous-réseau de 255.255.0.0.
Pour la passerelle par défaut, entrez l'adresse IP du LAN de pfSense 192.168.0.1.
Pour les serveurs DNS, vous pouvez également entrer l'adresse de pfSense ou celle des serveurs DNS publics comme Google (8.8.8.8).

<img width="294" alt="Capture d’écran 2024-08-08 à 15 42 27" src="https://github.com/user-attachments/assets/2868a2f4-92b4-49c4-9f54-7b4fae2569ce">

Sous Linux :
Ouvrez un terminal.
Modifiez le fichier de configuration réseau (par exemple /etc/network/interfaces sous Debian/Ubuntu, ou /etc/sysconfig/network-scripts/ifcfg-eth0 sous CentOS/RHEL).
Ajoutez ou modifiez la ligne GATEWAY=192.168.0.1 avec l'adresse IP du LAN de pfSense.
Redémarrez le service réseau avec sudo systemctl restart networking (Debian/Ubuntu) ou sudo systemctl restart network (CentOS/RHEL).

<img width="591" alt="Capture d’écran 2024-08-08 à 15 23 29" src="https://github.com/user-attachments/assets/80d5c04f-7a5b-4921-96bc-fc83385d1d8d">


### 8. **Accéder à l'interface Web de pfSense**
   - Pour configurer pfSense via une interface graphique, ouvrez un navigateur web sur une autre machine virtuelle connectée au réseau interne ou sur votre hôte.
   - Tapez l'adresse IP LAN de pfSense dans la barre d'adresse `https://192.168.0.1`.
   - Vous accéderez à l'interface web de pfSense où vous pouvez vous connecter avec les identifiants par défaut :
     - **Utilisateur** : `admin`
     - **Mot de passe** : `pfsense`

### 9. **Configurer et utiliser pfSense**
   - Une fois connecté à l'interface web, vous pouvez commencer à configurer pfSense selon vos besoins : créer des règles de pare-feu, configurer le NAT, gérer les VPN, etc.

### 10. **Sauvegarde et instantanés**
   - Une fois la configuration de base effectuée, vous pouvez créer un **instantané** (snapshot) de la machine virtuelle dans VirtualBox, pour pouvoir revenir facilement à cet état en cas de problème.

Et voilà, pfSense est maintenant installé et fonctionnel sur VirtualBox ! Vous pouvez l'utiliser pour gérer et protéger votre réseau virtuel.
