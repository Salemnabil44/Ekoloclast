## 3.1.1. Nous avons à disposition un fichier excel avec les informations des départements, des utilisateurs etc... La première étapé sera de convertir le fichier xlsx en fichier csv pour cela nous allons utilisé Python 3.

### 1. Installer les bibliothèques nécessaires

Ouvrez le terminal et exécutez les commandes suivantes pour installer `pandas` et `openpyxl` :

```bash
pip3 install pandas openpyxl
```

### 2. Créer le script Python

Utilisez votre éditeur de texte préféré (par exemple, `nano`, `vim`, ou tout autre éditeur de votre choix) pour créer un nouveau fichier pour le script Python. Par exemple, avec `nano` :

```bash
nano convert_xlsx_to_csv.py
```

### 3. Copier le script Python

Copiez et collez le script Python suivant dans votre éditeur :

```python
import pandas as pd

# Remplacez par le chemin de votre fichier XLSX
xlsx_file = "path/to/your/file.xlsx"
# Remplacez par le chemin de destination pour le fichier CSV
csv_file = "path/to/your/file.csv"

# Lecture du fichier XLSX
df = pd.read_excel(xlsx_file)

# Écriture du fichier CSV
df.to_csv(csv_file, index=False)

print(f"Le fichier {xlsx_file} a été converti en {csv_file} avec succès.")
```

Remplacez `"path/to/your/file.xlsx"` par le chemin de votre fichier XLSX et `"path/to/your/file.csv"` par le chemin où vous voulez enregistrer le fichier CSV converti.

Pour enregistrer et quitter `nano`, appuyez sur `Ctrl + X`, puis `Y` pour confirmer et `Enter` pour sauvegarder.

### 4. Exécuter le script

Retournez dans le terminal et exécutez le script :

```bash
python3 convert_xlsx_to_csv.py
```

Assurez-vous que vous êtes dans le bon répertoire où se trouve votre script Python ou fournissez le chemin complet vers le script Python.

En suivant ces étapes, vous devriez pouvoir convertir votre fichier XLSX en CSV directement depuis un terminal.

3.1.2

Nous allons vérifier que le fichier CSV est bien lisible, Ce script PowerShell est conçu pour lire les données d'un fichier CSV, afficher ces données, et les stocker potentiellement dans un dictionnaire pour un traitement ultérieur. Voici une explication détaillée de chaque section du script :

# Charger le module Active Directory
# Import-Module ActiveDirectory

# Créer les OU de départements et de services
$csvFilePath = "C:\Users\Administrateur\Documents\Annexe.csv"
$dictionary = @{}

# Importer les données Excel
try {
    $data = Import-csv -Path $csvFilePath -Delimiter ","
    $lineNumber = 1

    foreach ($row in $data) {
        if ($row -ne $null) {
            Write-Host "Ligne $lineNumber :"
            foreach ($prop in $row.PSObject.Properties) {
                Write-Host " " $($prop.Name) : $($prop.Value)
            }

            # Votre logique de vérification et d'ajout au dictionnaire ici

        } else {
            Write-Host "Ligne $lineNumber ignorée : ligne vide ou nulle."
        }

        $lineNumber++
    }

} catch {
    Write-Host "Une erreur s'est produite lors de la lecture du fichier CSV : $_"
    exit 1
}

# Afficher le contenu du dictionnaire
foreach ($key in $dictionary.Keys) {
    Write-Host "$key :"
    foreach ($col in $dictionary[$key].Keys) {
        Write-Host " $col : $($dictionary[$key][$col])"
    }
}

Vérifier que le chemin vers le fichier csv est correct avant de lancer le script. En lançant le script vous devriez avoir ce résultat 

<img width="858" alt="Capture d’écran 2024-08-04 à 19 03 17" src="https://github.com/user-attachments/assets/2c896dfc-7bb5-4794-995e-8f936a274a03">

