# Environnement Dev Container - Data Engineering

Environnement de développement portable et synchronisé via Dev Containers pour Data Engineering et Web Development.

---

## ✨ Packages Installés

### 📊 Data Processing
- **pandas** 2.2.0 - Manipulation de données
- **numpy** 1.26.3 - Calcul numérique
- **polars** 0.20.6 - DataFrames ultra-rapides
- **pyarrow** 15.0.0 - Format columnar

### 🗄️ Databases
- **SQLAlchemy** 1.4.53 - ORM SQL
- **psycopg2-binary** 2.9.9 - PostgreSQL
- **DuckDB** 0.10.0 - Base analytique in-process

### 🔄 Workflow & Orchestration
- **Apache Airflow** 2.8.1 - Orchestration de pipelines
- **airflow-providers-postgres** 5.10.0
- **dbt-core** 1.7.6 - Transformation de données
- **dbt-postgres** 1.7.6

### ⚡ Big Data
- **PySpark** 3.5.0 - Traitement distribué

### 📈 Visualization
- **matplotlib** 3.8.2
- **seaborn** 0.13.1
- **plotly** 5.18.0

### 📓 Notebooks
- **JupyterLab** 4.0.10
- **ipykernel** 6.29.0

### 🌐 Web Development
- **FastAPI** 0.109.0 - API moderne
- **uvicorn** 0.27.0 - Serveur ASGI
- **Flask** (installé par Airflow, version 2.2.x)
- **Django** (installé par Airflow, version compatible)

### 🔧 Utilities
- **Celery** 5.3.6 - Tasks asynchrones
- **Redis** 5.0.1 - Cache
- **requests** 2.31.0 / **httpx** 0.26.0 - HTTP clients
- **pydantic** 2.5.3 - Validation de données
- **python-dotenv** 1.0.0 - Variables d'environnement
- **click** 8.1.7 - CLI

### 🧪 Testing & Quality
- **pytest** 7.4.4
- **pytest-asyncio** 0.23.3
- **black** 24.1.1 - Formatage
- **flake8** 7.0.0 - Linting
- **pylint** 3.0.3
- **mypy** 1.8.0 - Type checking

### 🤖 Machine Learning
- **scikit-learn** 1.4.0
- **scipy** (dépendance de great-expectations)

### ✅ Data Quality
- **great-expectations** 0.18.8

---

## 🚀 Installation Rapide

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
# Attendre 15-20 min (première fois seulement - téléchargement et installation)
```

**C'EST TOUT !** Vous êtes maintenant dans un environnement Python complet avec tous les packages.

---

## 💼 Utiliser avec Vos Projets

### Créer un Nouveau Projet

```bash
# Sortir du container (si dedans)
# Ctrl+Shift+P > "Reopen Folder Locally"

# Dans PowerShell/Terminal normal
cd Documents
mkdir projets-travail
cd projets-travail
mkdir mon-projet
cd mon-projet

# Copier la config Dev Container depuis data-env
cp -r ../data-env/.devcontainer .

# Créer la structure du projet
mkdir notebooks scripts data sql
echo "# Mon Projet" > README.md

# Initialiser Git
git init
git add .
git commit -m "Initial commit"

# Créer repo GitHub et push (optionnel)
git remote add origin https://github.com/votre-username/mon-projet.git
git push -u origin main

# Ouvrir dans VS Code
code .

# Dans VS Code : Ctrl+Shift+P > "Reopen in Container"
# Attendre 15-20 min (première fois)
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

## 🔄 Workflow Quotidien

### Sur PC Fixe (Matin)

```bash
cd mon-projet
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
cd mon-projet
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
git clone https://github.com/votre-username/mon-projet.git
cd mon-projet

# 3. Ouvrir dans VS Code
code .

# 4. Dans VS Code : Ctrl+Shift+P > "Reopen in Container"
# Attendre 15-20 min (build de l'image)

# 5. BOOM ! Même environnement que partout ailleurs
```

---

## 🛠️ Commandes Utiles

### Dans le Container

```bash
# Vérifier Python
python --version
# Python 3.11.14

# Tester packages essentiels
python -c "import pandas, numpy, airflow, dbt, pyspark, fastapi; print('Tous les packages OK')"

# Lancer JupyterLab
jupyter lab --ip=0.0.0.0 --no-browser
# Puis ouvrir http://localhost:8888

# Tester Airflow
airflow version

# Lancer un shell Python interactif
python
>>> import pandas as pd
>>> import numpy as np
```

### Ajouter un Package

**Temporaire (pour tester) :**
```bash
pip install nom-package
```
⚠️ Sera perdu au rebuild du container.

**Permanent (recommandé) :**
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

### Gestion Git

```bash
# Voir les changements
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

# Revenir en arrière
git checkout main
```

---

## 🐛 Dépannage

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

**Option A - Token GitHub :**
1. Aller sur https://github.com/settings/tokens
2. Generate new token (classic)
3. Cocher `repo`
4. Copier le token
5. L'utiliser comme mot de passe

**Option B - SSH (recommandé) :**
```bash
# Générer une clé SSH
ssh-keygen -t ed25519 -C "votre@email.com"
# Appuyer sur Entrée 3 fois

# Copier la clé publique
cat ~/.ssh/id_ed25519.pub

# Ajouter sur GitHub : https://github.com/settings/keys
# Puis changer l'URL du repo
git remote set-url origin git@github.com:votre-username/mon-projet.git
```

### Conflits de versions

Si vous avez des conflits après `git pull` :
```bash
# VS Code montrera les conflits
# Choisir quelle version garder
# Puis :
git add .
git commit -m "Merge: résolution conflits"
git push
```

---

## 📂 Synchronisation Entre Machines

### Ce qui EST synchronisé (via Git)
✅ Code Python
✅ Notebooks Jupyter  
✅ Configuration (.devcontainer)
✅ Scripts
✅ Documentation

### Ce qui N'est PAS synchronisé (.gitignore)
❌ Données volumineuses (data/)
❌ Fichiers temporaires
❌ Cache Python (__pycache__)
❌ Secrets (.env)
❌ Logs

### Pour les données volumineuses

**Option A - Cloud Storage**
```python
# AWS S3
import boto3
s3 = boto3.client('s3')
s3.download_file('bucket', 'data.csv', 'data/data.csv')

# Google Cloud Storage
from google.cloud import storage
client = storage.Client()
bucket = client.bucket('mon-bucket')
blob = bucket.blob('data.csv')
blob.download_to_filename('data/data.csv')
```

**Option B - DVC (Data Version Control)**
```bash
pip install dvc
dvc init
dvc add data/large_file.csv
git add data/large_file.csv.dvc .dvc/config
git commit -m "Track large file with DVC"
```

---

## 💡 Cas d'Usage

### Data Engineering

```python
# ETL avec Pandas + DuckDB
import pandas as pd
import duckdb

# Lire CSV
df = pd.read_csv('data/sales.csv')

# Transformer
df['revenue'] = df['price'] * df['quantity']

# Charger dans DuckDB
con = duckdb.connect('data/analytics.db')
con.execute("CREATE TABLE sales AS SELECT * FROM df")
```

### Airflow DAG

```python
# Dans dags/mon_pipeline.py
from airflow import DAG
from airflow.operators.python import PythonOperator
from datetime import datetime

def extract():
    print("Extract data...")

with DAG('mon_pipeline', start_date=datetime(2024, 1, 1)) as dag:
    task = PythonOperator(task_id='extract', python_callable=extract)
```

### FastAPI

```python
# Dans scripts/api.py
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"message": "Hello World"}

# Lancer : uvicorn scripts.api:app --reload
```

### dbt

```bash
# Initialiser dbt
dbt init mon_projet_dbt

# Compiler et exécuter
dbt run
```

---

## 🎯 Avantages de cette Approche

✅ **Portable** - Même environnement sur tous les PC (Windows, Mac, Linux)
✅ **Isolé** - N'affecte pas votre système
✅ **Versionné** - Tout dans Git, historique complet
✅ **Reproductible** - Partagez le repo = partagez l'environnement
✅ **Production-ready** - Même config qu'en production
✅ **Simple** - 3 commandes pour démarrer
✅ **Complet** - Tous les outils data engineering + web dev

---

## 📚 Ressources

- **Docker** : https://docs.docker.com/
- **VS Code Dev Containers** : https://code.visualstudio.com/docs/devcontainers/containers
- **Apache Airflow** : https://airflow.apache.org/docs/
- **dbt** : https://docs.getdbt.com/
- **FastAPI** : https://fastapi.tiangolo.com/
- **PySpark** : https://spark.apache.org/docs/latest/api/python/

---

## 🆘 Support

### Vérifications de base
1. ✅ Docker Desktop est lancé ?
2. ✅ Extension "Dev Containers" installée dans VS Code ?
3. ✅ Vous êtes dans le bon dossier ?

### Voir les logs
```bash
# Logs Docker
docker logs nom-container

# Logs du build
# Ctrl+Shift+P > "Dev Containers: Show Container Log"
```

---

## 📝 Notes Importantes

### Versions de Flask et Django
Airflow 2.8.1 installe automatiquement :
- **Flask 2.2.x** (compatible avec Airflow)
- **Django** (version compatible)

Ne pas spécifier manuellement ces versions dans requirements.txt pour éviter les conflits.

### Temps de Build
- **Première fois** : 15-20 minutes (téléchargement + installation)
- **Rebuild après changement** : 5-10 minutes
- **Ouverture normale** : 30 secondes

---

**Bon développement !** 🚀

Créé avec ❤️ pour un environnement data engineering professionnel et portable.