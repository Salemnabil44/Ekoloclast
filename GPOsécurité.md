### 1. Politique de mot de passe (complexité, longueur, etc.)

1. Ouvrez la console de gestion des stratégies de groupe (GPMC).
2. Allez à **Forêt > Domaines > Votre_Domaine > Contrôleurs de domaine**.
3. Faites un clic droit sur **Default Domain Policy** (Stratégie par défaut du domaine) et sélectionnez **Modifier**.
4. Naviguez à **Configuration de l'ordinateur > Stratégies > Paramètres Windows > Paramètres de sécurité > Stratégies de compte > Stratégie de mot de passe**.
5. Configurez les paramètres suivants selon vos besoins :
   - **Le mot de passe doit respecter des exigences de complexité**
   - **Longueur minimale du mot de passe**
   - **Durée de vie maximale du mot de passe**
   - **Durée de vie minimale du mot de passe**
   - **Historique des mots de passe**

### 2. Verrouillage de compte

1. Dans la même GPO **Default Domain Policy**, allez à **Stratégies de compte > Stratégie de verrouillage de compte**.
2. Configurez les paramètres suivants :
   - **Durée du verrouillage du compte**
   - **Seuil de verrouillage du compte**
   - **Réinitialiser le compteur de verrouillage du compte après**

### 3. Restriction d'installation de logiciel pour les utilisateurs non-administrateurs

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Composants Windows > Windows Installer**.
3. Configurez le paramètre **Interdire les installations utilisateur**.

### 4. Gestion de Windows Update

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Composants Windows > Windows Update**.
3. Configurez les paramètres suivants selon vos besoins :
   - **Configurer les mises à jour automatiques**
   - **Spécifier l'emplacement du service de mise à jour Microsoft sur l'intranet**
   - **Ne pas redémarrer automatiquement avec les utilisateurs connectés pour les installations planifiées des mises à jour automatiques**

### 5. Blocage de l'accès à la base de registre

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'utilisateur > Stratégies > Modèles d'administration > Système**.
3. Activez le paramètre **Interdire l'accès aux outils de modification du Registre**.

### 6. Blocage complet ou partiel au panneau de configuration

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'utilisateur > Stratégies > Modèles d'administration > Panneau de configuration**.
3. Configurez les paramètres suivants selon vos besoins :
   - **Interdire l'accès au Panneau de configuration et aux paramètres PC**
   - **Afficher uniquement les éléments spécifiés du Panneau de configuration**
   - **Masquer les éléments spécifiés du Panneau de configuration**

### 7. Restriction des périphériques amovibles

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Système > Accès au stockage amovible**.
3. Configurez les paramètres selon vos besoins (par exemple, **Refuser l'accès en lecture** et **Refuser l'accès en écriture**).

### 8. Gestion d'un compte du domaine qui est administrateur local des machines

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Paramètres Windows > Paramètres de sécurité > Groupes restreints**.
3. Ajoutez le groupe **Administrateurs** et ajoutez le compte du domaine souhaité.

### 9. Gestion du pare-feu

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Réseau > Connexions réseau > Pare-feu Windows**.
3. Configurez les paramètres selon vos besoins, notamment pour les profils Domaine, Privé et Public.

### 10. Écran de veille avec mot de passe en sortie

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'utilisateur > Stratégies > Modèles d'administration > Panneau de configuration > Personnalisation**.
3. Activez le paramètre **Mot de passe requis à la reprise de l'écran de veille**.
4. Configurez également **Délai d’inactivité de l’écran de veille**.

### 11. Forçage du type d'utilisation sécurisée du bureau à distance

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Composants Windows > Services Bureau à distance > Hôte de session Bureau à distance > Sécurité**.
3. Configurez le paramètre **Exiger l'utilisation d'une couche de sécurité spécifique pour les connexions Bureau à distance (RDP)** et sélectionnez **SSL (TLS 1.0)** ou une autre option sécurisée.

### 12. Limitation des tentatives d'élévation de privilèges

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Paramètres Windows > Paramètres de sécurité > Stratégies locales > Options de sécurité**.
3. Configurez les paramètres relatifs à l'UAC, comme **Contrôle de compte d'utilisateur : comportement de l'invite d'élévation pour les utilisateurs standard**.

### 13. Définition de scripts de démarrage pour les machines et/ou les utilisateurs

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Paramètres Windows > Scripts (démarrage/arrêt)** pour les scripts de démarrage/arrêt des machines.
3. Allez à **Configuration de l'utilisateur > Stratégies > Paramètres Windows > Scripts (ouverture de session/fermeture de session)** pour les scripts de connexion/déconnexion des utilisateurs.
4. Ajoutez les scripts nécessaires dans les sections correspondantes.

### 14. Politique de sécurité PowerShell

1. Créez ou éditez une GPO.
2. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Composants Windows > Windows PowerShell**.
3. Configurez les paramètres comme **Activer l'exécution des scripts** et définissez le niveau d'exécution souhaité (par exemple, **AllSigned**, **RemoteSigned**, etc.).

Ces étapes vous guideront à travers la configuration des GPOs nécessaires. Assurez-vous de tester les GPOs dans un environnement de test avant de les appliquer en production.
