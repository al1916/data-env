# Environnement Dev Container - Data Engineering

Environnement de développement portable et synchronisé via Dev Containers.

---

## Installation Rapide

### Prérequis (sur chaque PC)
1. **Docker Desktop** : https://www.docker.com/products/docker-desktop
2. **VS Code** : https://code.visualstudio.com/
3. **Extension VS Code** : "Dev Containers" (ms-vscode-remote.remote-containers)

### Première Utilisation

```bash
# Cloner ce repo
git clone https://github.com/al1916/data-env.git
cd data-env

# Ouvrir dans VS Code
code .

# Dans VS Code : Ctrl+Shift+P
# Taper : "Dev Containers: Reopen in Container"
# Attendre 5-10 min (première fois seulement)
```

**C'EST TOUT !** Vous êtes maintenant dans un environnement Python complet.

---

## Packages Installés

### Data Processing
- pandas 2.2.0
- numpy 1.26.3
- polars 0.20.6

### Databases
- SQLAlchemy 1.4.53
- psycopg2-binary 2.9.9
- DuckDB 0.10.0

### Data Transformation
- dbt-core 1.7.6
- dbt-postgres 1.7.6

### Visualization
- matplotlib 3.8.2
- seaborn 0.13.1
- plotly 5.18.0

### Notebooks
- JupyterLab 4.0.10
- ipykernel 6.29.0

### Web Development
- FastAPI 0.109.0
- uvicorn 0.27.0

### Utilities
- requests 2.31.0
- httpx 0.26.0
- python-dotenv 1.0.0
- pyyaml 6.0.1
- tqdm 4.66.1

### Testing & Quality
- pytest 7.4.4
- black 24.1.1
- pylint 3.0.3

---

## Utiliser avec Vos Projets

### Créer un Nouveau Projet

```bash
# Sortir du container (si dedans)
# Ctrl+Shift+P > "Reopen Folder Locally"

# Dans PowerShell/Terminal normal
cd C:\Users\VotrNom\Documents
mkdir projets-travail
cd projets-travail
mkdir mon-projet-client
cd mon-projet-client

# Copier la config Dev Container
cp -r C:\Users\VotrNom\Documents\data-env\.devcontainer .

# Créer la structure du projet
mkdir notebooks scripts data sql
echo "# Mon Projet Client" > README.md

# Initialiser Git
git init
git add .
git commit -m "Initial commit"

# Créer repo GitHub (optionnel)
git remote add origin https://github.com/votre-username/mon-projet-client.git
git push -u origin main

# Ouvrir dans VS Code
code .

# Dans VS Code : Ctrl+Shift+P > "Reopen in Container"
```

### Structure Projet Recommandée

```
mon-projet/
├── .devcontainer/          # Config Dev Container (copié depuis data-env)
│   ├── Dockerfile
│   ├── devcontainer.json
│   └── requirements.txt
├── notebooks/              # Jupyter notebooks
├── scripts/                # Scripts Python
├── data/                   # Données (ignoré par Git)
├── sql/                    # Requêtes SQL
└── README.md
```

---

## Workflow Quotidien

### Sur PC Fixe (Matin)

```bash
cd mon-projet-client
git pull                    # Récupérer derniers changements
code .                      # Ouvrir VS Code

# Si pas déjà dans le container :
# Ctrl+Shift+P > "Reopen in Container"

# Travailler toute la journée...

# Fin de journée
git add .
git commit -m "Description des changements"
git push
```

### Sur Laptop Client (Après-midi)

```bash
cd mon-projet-client
git pull                    # Récupérer travail du matin
code .                      # Ouvrir VS Code
# Ctrl+Shift+P > "Reopen in Container"

# EXACTEMENT le même environnement qu'au bureau !

# Fin
git add .
git commit -m "Suite du travail"
git push
```

### Sur Nouveau PC (Première fois)

```bash
# 1. Installer Docker Desktop + VS Code + Extension "Dev Containers"

# 2. Cloner votre projet
git clone https://github.com/votre-username/mon-projet-client.git
cd mon-projet-client

# 3. Ouvrir dans VS Code
code .

# 4. Dans VS Code : Ctrl+Shift+P > "Reopen in Container"
# Attendre 5-10 min (build de l'image)

# 5. BOOM ! Même environnement que partout ailleurs
```

---

## Commandes Utiles

### Dans le Container

```bash
# Vérifier Python
python --version

# Tester packages
python -c "import pandas, numpy, dbt, sqlalchemy, fastapi; print('OK')"

# Lancer JupyterLab
jupyter lab --ip=0.0.0.0 --no-browser
# Puis ouvrir http://localhost:8888

# Installer un nouveau package
pip install nom-package

# Puis l'ajouter dans requirements.txt
echo "nom-package==X.Y.Z" >> .devcontainer/requirements.txt

# Rebuild le container
# Ctrl+Shift+P > "Dev Containers: Rebuild Container"
```

### Gestion Git

```bash
# Status
git status

# Sauvegarder
git add .
git commit -m "Description claire"
git push

# Récupérer
git pull

# Créer une branche
git checkout -b feature/nouvelle-fonctionnalite

# Voir l'historique
git log --oneline
```

---

## Ajouter des Packages

### Méthode 1 - Temporaire (pour tester)

```bash
# Dans le terminal du container
pip install nom-package
```

⚠️ Ce package sera perdu au rebuild du container.

### Méthode 2 - Permanent (recommandé)

```bash
# 1. Ajouter dans .devcontainer/requirements.txt
echo "nom-package==X.Y.Z" >> .devcontainer/requirements.txt

# 2. Rebuild le container
# Ctrl+Shift+P > "Dev Containers: Rebuild Container"

# 3. Commit le changement
git add .devcontainer/requirements.txt
git commit -m "Ajout package nom-package"
git push
```

---

## Dépannage

### Le container ne démarre pas

```bash
# Nettoyer Docker
docker system prune -a

# Relancer
# Ctrl+Shift+P > "Dev Containers: Rebuild Container"
```

### Package manquant

```bash
# Vérifier qu'il est dans requirements.txt
cat .devcontainer/requirements.txt | grep nom-package

# Si absent, l'ajouter et rebuild
echo "nom-package==X.Y.Z" >> .devcontainer/requirements.txt
# Ctrl+Shift+P > "Rebuild Container"
```

### Git demande credentials à chaque fois

```bash
# Configurer SSH (recommandé)
ssh-keygen -t ed25519 -C "votre@email.com"
cat ~/.ssh/id_ed25519.pub
# Copier la clé et l'ajouter sur GitHub : https://github.com/settings/keys
```

---

## Synchronisation Entre Machines

### Ce qui EST synchronisé (via Git)
✅ Code Python
✅ Notebooks Jupyter
✅ Configuration (.devcontainer)
✅ Scripts
✅ Documentation

### Ce qui N'est PAS synchronisé (via .gitignore)
❌ Données volumineuses (data/)
❌ Fichiers temporaires
❌ Cache Python (__pycache__)
❌ Secrets (.env)

### Pour les données volumineuses

**Option A - Cloud Storage**
```python
# Utiliser AWS S3, Google Cloud Storage, etc.
import boto3
s3 = boto3.client('s3')
s3.download_file('bucket', 'data.csv', 'data/data.csv')
```

**Option B - DVC (Data Version Control)**
```bash
pip install dvc
dvc init
dvc add data/large_file.csv
git add data/large_file.csv.dvc .dvc/config
```

---

## Avantages de cette Approche

✅ **Portable** - Même environnement sur tous les PC
✅ **Isolé** - N'affecte pas votre système Windows
✅ **Versionné** - Tout dans Git, historique complet
✅ **Reproductible** - Partagez le repo = partagez l'environnement
✅ **Production-ready** - Même config qu'en production
✅ **Simple** - 3 commandes pour démarrer

---

## Support

### Vérifications
1. Docker Desktop est lancé ?
2. Extension "Dev Containers" installée ?
3. Vous êtes dans le bon dossier ?

### Logs
```bash
# Voir les logs Docker
docker logs nom-container

# Voir les logs du build
# Ctrl+Shift+P > "Dev Containers: Show Container Log"
```

---

**Bon développement !** 🚀