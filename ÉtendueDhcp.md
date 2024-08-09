Une étendue DHCP (ou DHCP scope en anglais) est une gamme d'adresses IP définie sur un serveur DHCP (Dynamic Host Configuration Protocol) qui est utilisée pour attribuer automatiquement des adresses IP aux appareils (comme les ordinateurs, les imprimantes, les téléphones, etc.) sur un réseau.

Pour créer des étendues DHCP (Dynamic Host Configuration Protocol) sur un serveur Windows qui fait partie d'un domaine Active Directory, voici la démarche à suivre :

### 1. **Prérequis :**
   - Assurez-vous que le rôle "DHCP" est installé sur le serveur.
   - Le serveur doit être joint au domaine Active Directory.
   - Vous devez avoir les droits administratifs sur le serveur.

### 2. **Ouvrir la Console DHCP :**
   1. Connectez-vous au serveur Windows avec un compte administrateur.
   2. Ouvrez le "Gestionnaire de serveur" (`Server Manager`).
   3. Cliquez sur "Outils" (`Tools`) et sélectionnez "DHCP".

### 3. **Créer une Étendue DHCP :**
   1. **Sélectionnez le serveur DHCP** dans la console DHCP.
   2. Faites un clic droit sur "IPv4" (ou "IPv6" selon votre besoin) sous le serveur DHCP, puis sélectionnez "Nouvelle étendue" (`New Scope`).

<img width="745" alt="Capture d’écran 2024-08-09 à 20 54 03" src="https://github.com/user-attachments/assets/c2842c57-4937-4566-bb66-bac1a5ce0c49">

   
   3. **Assistant Nouvelle Étendue :**
      - **Nom de l'étendue :** Donnez un nom descriptif à l'étendue (par exemple "Étendue Bureau Principal").
      - **Description :** (Optionnel) Donnez une description qui clarifie l'utilisation de cette étendue.

<img width="749" alt="Capture d’écran 2024-08-09 à 20 54 40" src="https://github.com/user-attachments/assets/2d60971a-ce2a-4f4a-ac77-110ae0f7b622">


   4. **Plage d'adresses IP :**
      - **Adresse IP de début :** Indiquez la première adresse IP de la plage.
      - **Adresse IP de fin :** Indiquez la dernière adresse IP de la plage.
      - **Longueur du masque de sous-réseau** : Spécifiez la longueur du masque (par exemple, /24 pour un masque de 255.255.255.0).

<img width="751" alt="Capture d’écran 2024-08-09 à 20 55 13" src="https://github.com/user-attachments/assets/d465ca8a-28c7-4b8c-bb59-7a2f7c528e21">


   5. **Ajouter des exclusions et délais d'attente :**
      - Vous pouvez exclure certaines adresses IP de la plage, si nécessaire (pour des serveurs ou autres équipements).
      - Spécifiez le délai d'attente du bail (par défaut, c'est 8 jours).

   6. **Configurer les options DHCP :**
      - Vous pouvez configurer les options DHCP directement après avoir créé l'étendue, ou les configurer plus tard. Les options incluent :
         - **Passerelle par défaut** (`Router`): Indiquez l'adresse IP de la passerelle.

<img width="747" alt="Capture d’écran 2024-08-09 à 20 56 24" src="https://github.com/user-attachments/assets/38359f56-3a62-48a4-9717-d056a3bf042f">

      
         - **Serveur DNS :** Ajoutez les adresses IP des serveurs DNS que les clients vont utiliser.
         - **Nom de domaine :** Indiquez le nom de domaine que les clients doivent utiliser.

<img width="749" alt="Capture d’écran 2024-08-09 à 20 56 57" src="https://github.com/user-attachments/assets/e9a92c5b-7642-474f-9c52-f149b2170f10">


   8. **Activer l'étendue :**
      - À la fin de l'assistant, vous aurez la possibilité d'activer immédiatement l'étendue. Sélectionnez "Oui, je veux activer cette étendue maintenant" (`Yes, I want to activate this scope now`).

### 4. **Vérifier et configurer les options avancées (optionnel) :**
   - Si vous avez besoin de configurer des options supplémentaires, comme des classes utilisateur ou des réservations, vous pouvez le faire via la console DHCP sous les options de serveur ou les options d'étendue spécifiques.

### 5. **Superviser et tester :**
   - Une fois l'étendue activée, vérifiez que les clients du réseau obtiennent correctement des adresses IP de cette étendue.
   - Vous pouvez superviser les baux actifs dans la console DHCP pour vous assurer que tout fonctionne comme prévu.

### 6. **Gestion et maintenance :**
   - Revenez régulièrement pour vérifier les baux, ajuster les exclusions ou les réservations, et garantir que l'étendue reste suffisante pour les besoins du réseau.

C’est ainsi que vous pouvez créer et configurer des étendues DHCP dans un environnement Active Directory, Voici le résultat des étendues créées.

<img width="748" alt="Capture d’écran 2024-08-09 à 20 52 42" src="https://github.com/user-attachments/assets/c2d363ff-684a-42e3-82b4-c335efb3cf4f">

