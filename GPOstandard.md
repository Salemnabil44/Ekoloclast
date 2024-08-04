### 1. Fond d'écran

1. Ouvrez la console de gestion des stratégies de groupe (GPMC).
2. Créez une nouvelle GPO ou éditez une GPO existante.
3. Allez à **Configuration de l'utilisateur > Stratégies > Modèles d'administration > Bureau > Active Desktop**.
4. Activez le paramètre **Active Desktop Wallpaper** (Fond d'écran Active Desktop).
5. Spécifiez le chemin d'accès à l'image du fond d'écran (par exemple, `\\Serveur\Partage\fond_ecran.jpg`).
6. Sélectionnez **Style de papier peint** (par exemple, **Centred**, **Stretched**).

### 2. Mappage de lecteurs

1. Ouvrez la console de gestion des stratégies de groupe (GPMC).
2. Créez une nouvelle GPO ou éditez une GPO existante.
3. Allez à **Configuration de l'utilisateur > Préférences > Paramètres Windows > Lecteurs réseau**.
4. Faites un clic droit et sélectionnez **Nouveau > Lecteur mappé**.
5. Configurez les paramètres :
   - **Action** : Créer
   - **Emplacement** : Chemin réseau du partage (par exemple, `\\Serveur\Partage`)
   - **Lettre du lecteur** : Sélectionnez une lettre disponible (par exemple, Z:)

### 3. Gestion de l'alimentation

1. Ouvrez la console de gestion des stratégies de groupe (GPMC).
2. Créez une nouvelle GPO ou éditez une GPO existante.
3. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Système > Gestion de l'alimentation**.
4. Configurez les paramètres selon vos besoins, tels que :
   - **Stratégie d'alimentation préférée**
   - **Configuration de la veille**
   - **Paramètres de gestion de l'alimentation pour les systèmes de batterie**

### 4. Déploiement (publication) de logiciels

1. Ouvrez la console de gestion des stratégies de groupe (GPMC).
2. Créez une nouvelle GPO ou éditez une GPO existante.
3. Allez à **Configuration de l'ordinateur > Stratégies > Paramètres logiciels > Installation de logiciels**.
4. Faites un clic droit et sélectionnez **Nouveau > Package**.
5. Parcourez le partage réseau contenant le fichier MSI du logiciel (par exemple, `\\Serveur\Partage\Logiciel.msi`).
6. Sélectionnez **Attribué** pour installer le logiciel automatiquement ou **Publié** pour le rendre disponible dans Ajout/Suppression de programmes.

### 5. Redirection de dossiers (Documents, Bureau, etc.)

1. Ouvrez la console de gestion des stratégies de groupe (GPMC).
2. Créez une nouvelle GPO ou éditez une GPO existante.
3. Allez à **Configuration de l'utilisateur > Stratégies > Paramètres Windows > Redirection de dossiers**.
4. Sélectionnez le dossier à rediriger (par exemple, **Documents**).
5. Faites un clic droit et sélectionnez **Propriétés**.
6. Configurez les paramètres :
   - **Paramètre** : Basé sur l'emplacement du groupe
   - **Chemin du dossier cible** : Spécifiez le chemin réseau (par exemple, `\\Serveur\Partage\Documents\%USERNAME%`).

### 6. Configuration des paramètres du navigateur (Firefox ou Chrome)

#### Pour Firefox :

1. Téléchargez et installez le fichier de modèle ADMX pour Firefox.
2. Copiez les fichiers ADMX et ADML dans le dossier **PolicyDefinitions** de votre contrôleur de domaine.
3. Créez une nouvelle GPO ou éditez une GPO existante.
4. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Mozilla > Firefox**.
5. Configurez les paramètres selon vos besoins (par exemple, définir la page d'accueil, désactiver les mises à jour automatiques).

#### Pour Chrome :

1. Téléchargez et installez le fichier de modèle ADMX pour Google Chrome.
2. Copiez les fichiers ADMX et ADML dans le dossier **PolicyDefinitions** de votre contrôleur de domaine.
3. Créez une nouvelle GPO ou éditez une GPO existante.
4. Allez à **Configuration de l'ordinateur > Stratégies > Modèles d'administration > Google > Google Chrome**.
5. Configurez les paramètres selon vos besoins (par exemple, définir la page d'accueil, désactiver les mises à jour automatiques).

Ces étapes vous permettront de créer et configurer les GPOs nécessaires pour répondre à vos besoins en matière de gestion des fonds d'écran, des lecteurs mappés, de la gestion de l'alimentation, du déploiement de logiciels, de la redirection de dossiers et de la configuration des paramètres des navigateurs.
