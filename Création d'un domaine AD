# Objectifs Semaine 1 : AD-DS - Création d'un domaine AD   

	1.1 Un serveur Windows Server 2022 GUI avec les rôles AD-DS, DHCP, DNS   
	1.2 Un serveur Windows Server 2022 Core avec le rôle AD-DS   
	1.3 Les 2 serveurs sont des DC du domaine et ont une réplication complète gérée   


    
## 1. AD-DS - Création d'un domaine AD   

### 1.1 Un serveur Windows Server 2022 GUI avec les rôles AD-DS, DHCP, DNS

#### Installation de Windows Server GUI

1.1.1 **Télécharger et Installer VirtualBox**
   - Rendez-vous sur le site officiel de [VirtualBox](https://www.virtualbox.org/) et téléchargez la dernière version pour votre système d'exploitation (Windows, macOS, Linux).
   - Installez VirtualBox en suivant les instructions à l'écran.

1.1.2. **Télécharger l'ISO de Windows Server 2022**
   - Accédez au site officiel de Microsoft pour télécharger l'ISO de Windows Server 2022. Vous devrez peut-être vous inscrire ou vous connecter avec un compte Microsoft pour accéder au téléchargement.

1.1.3. **Créer une Nouvelle Machine Virtuelle**
   - Ouvrez VirtualBox et cliquez sur `Nouvelle`.
   - Donnez un nom à la machine virtuelle (par exemple, "Windows Server 2022").
   - Choisissez l'ISO que vous venez de télécharger.
   - Cochez la case "skip Unattended Installation".
   - Cliquez sur `Suivant`.

1.1.4. **Configurer la Mémoire et le Disque Dur**
   - Mémoire (RAM): Allouez au moins 8 - 16 Go de RAM. Pour de meilleures performances, vous pouvez allouer plus de mémoire en fonction des ressources de votre machine hôte.
   - CPU: 2-4
   - Disque Dur: Sélectionnez "Créer un disque dur virtuel maintenant". Sélectionnez la taille de votre disque dur entre 60-100 Go. Cliquez sur `Suivant` puis `Finish`.

1.1.5. **Démarrer l'Installation de Windows Server 2022**
   - Sélectionnez votre machine virtuelle et cliquez sur `Démarrer`.
   - La machine virtuelle devrait démarrer à partir de l'ISO et lancer l'installation de Windows Server 2022. Suivez les instructions à l'écran pour installer Windows Server 2022 :
     - Sélectionnez la langue, le format de l'heure et le clavier, puis cliquez sur `Suivant`.
     - Cliquez sur `Installer maintenant`.
     - Entrez une clé de produit si vous en avez une, sinon, sélectionnez "Je n'ai pas de clé de produit" pour une version d'évaluation.
     - Choisissez la version Windows Server 2022 Standard (expérience de bureau) pour avoir l'interface graphique.
     - Acceptez les termes du contrat de licence.
     - Choisissez "Personnalisé : installer uniquement Windows (avancé)".
     - Sélectionnez le disque où vous voulez installer Windows Server 2022 et cliquez sur `Suivant`.

1.1.6. **Finaliser l'Installation**
   - L'installation de Windows Server 2022 va démarrer. Cela peut prendre un certain temps.
   - Une fois l'installation terminée, la machine virtuelle va redémarrer et vous serez invité à configurer des détails supplémentaires comme le mot de passe de l'administrateur.
   - L'installation est terminée.

#### Configuration de Windows Server GUI

1.1.7. **Renommer le Serveur**
   - Renommez le nom du serveur (exemple: SR1).

1.1.8. **Installer ADDS (Active Directory Domain Services)**
   - Cliquez sur "Ajouter des rôles et des fonctionnalités".
   - Cliquez sur `Suivant`, puis sélectionnez votre serveur sur lequel vous souhaitez installer Active Directory. Une fois validé, sélectionnez le rôle du serveur "Service AD DS" (AD DS = Active Directory Domain Services), puis cliquez sur `Installer`.
   - Une fois l'installation terminée, vous pouvez apercevoir en haut à gauche, dans les notifications, un avertissement. Cliquez sur l'icône puis sur "Promouvoir ce serveur en contrôleur de domaine".
   - Cliquez sur "Ajouter une nouvelle forêt".
   - Donnez un nom de domaine (exemple:Ekoloclast.lan).
   - Choisissez un mot de passe robuste puis redémarrez Windows Server 2022.
   - Une fois redémarré, le nom de l'administrateur devrait avoir changé. Vous pouvez vérifier que le domaine a été correctement créé dans l'onglet "Serveur local".

1.1.9. **Installer DHCP**
   - Cliquez sur "Ajouter des rôles et des fonctionnalités".
   - Cliquez sur `Suivant`, puis sélectionnez votre serveur sur lequel vous souhaitez installer Active Directory. Une fois validé, sélectionnez le rôle du serveur "Service DHCP", puis installez.

1.1.10. **Configurer l'Adresse IP en Statique**
   - Tapez `Windows + R` et lancez `ncpa.cpl`.
   - Cliquez sur les propriétés du réseau, puis cliquez sur "Protocol Internet version 4 (TCP/IPv4)" > Propriétés.
   - Entrez l'adresse fournie dans le plan d'adressage en annexe (192.168.0.4/16).

### 1.2 Un serveur Windows Server 2022 Core avec le rôle AD-DS

#### Installation de Windows Server Core

1.2.1 **Créer une Nouvelle Machine Virtuelle**
   - Ouvrez VirtualBox et cliquez sur `Nouvelle`.
   - Donnez un nom à la machine virtuelle (par exemple, "Windows Server Core 2022").
   - Choisissez l'ISO que vous venez de télécharger.
   - Cochez la case "skip Unattended Installation".
   - Cliquez sur `Suivant`.

1.2.2. **Configurer la Mémoire et le Disque Dur**
   - Mémoire (RAM): Allouez au moins 4 - 8 Go de RAM. Pour de meilleures performances, vous pouvez allouer plus de mémoire en fonction des ressources de votre machine hôte.
   - CPU: 1-2
   - Disque Dur: Sélectionnez "Créer un disque dur virtuel maintenant". Sélectionnez la taille de votre disque dur entre 40-60 Go. Cliquez sur `Suivant` puis `Finish`.

1.2.3. **Démarrer l'Installation de Windows Server 2022**
   - Sélectionnez votre machine virtuelle et cliquez sur `Démarrer`.
   - La machine virtuelle devrait démarrer à partir de l'ISO et lancer l'installation de Windows Server 2022. Suivez les instructions à l'écran pour installer Windows Server 2022 :
     - Sélectionnez la langue, le format de l'heure et le clavier, puis cliquez sur `Suivant`.
     - Cliquez sur `Installer maintenant`.
     - Entrez une clé de produit si vous en avez une, sinon, sélectionnez "Je n'ai pas de clé de produit" pour une version d'évaluation.
     - Choisissez la version Windows Server 2022 Datacenter.
     - Acceptez les termes du contrat de licence.
     - Choisissez "Personnalisé : installer uniquement Windows (avancé)".
     - Sélectionnez le disque où vous voulez installer Windows Server 2022 et cliquez sur `Suivant`.

1.2.4. **Finaliser l'Installation**
   - L'installation de Windows Server 2022 va démarrer. Cela peut prendre un certain temps.
   - Une fois l'installation terminée, la machine virtuelle va redémarrer et vous serez invité à configurer des détails supplémentaires comme le mot de passe de l'administrateur.
   - L'installation est terminée.

#### Configuration de Windows Server Core

1.2.5. **Changer le Nom du Serveur**
   - Changez le nom du serveur par SR2.

1.2.6. **Paramétrer le Réseau depuis la Console PowerShell**
   - Tapez `route print` dans PowerShell pour regarder la liste d'interfaces, l'objectif étant de connaître l'interface à modifier.
   - Tapez les lignes de commande suivantes :
     ```bash
     netsh interface IP set address "5" static 192.168.0.5 255.255.0.0 192.168.0.4
     netsh interface IP set DNS "5" static 192.168.0.5 primary
     ```

1.2.7. **Vérifier la Connexion Réseau**
   - Effectuez un Ping pour vérifier que les serveurs communiquent correctement entre eux.
   - Si nécessaire, configurez les règles Firewall pour permettre les paquets ICMP IPv4.

### 1.3 Les deux serveurs sont des DC du domaine et ont une réplication complète gérée

1.3.1 **Ajouter le Serveur Core au Domaine**
   - Depuis le gestionnaire de serveur > Tous les serveurs, cliquez sur `Gérer` > `Ajouter des serveurs`.
   - Cliquez sur `Recherche`, trouvez SR2, puis cliquez sur la flèche à droite et `OK`.
   - Cliquez sur le serveur SR2, puis cliquez droit et sélectionnez "Ajouter des rôles et des fonctionnalités" > `Services AD DS`.
   - Sélectionnez "Ajouter un contrôleur de domaine à un domaine existant" et cochez "Contrôleur de domaine en lecture seule".

1.3.2 **Réplication des Serveurs**

Les deux contrôleurs de domaine doivent répliquer toutes les données de l'Active Directory entre eux de manière complète et automatisée, assurant ainsi la cohérence et la disponibilité des données AD sur les deux serveurs. Utilisez la commande suivante pour vérifier la réplication intersite :
```bash
repadmin /showrepl
```

En résumé, la réplication entre les contrôleurs de domaine doit être en bonne santé et doit fonctionner comme prévu. Vous pouvez continuer à surveiller la réplication régulièrement pour vous assurer que tout reste synchronisé et sans erreurs.
