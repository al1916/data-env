# Environnement de Développement - Dev Container

Environnement Data Engineering portable via Dev Containers.

## Installation Rapide

### 1. Prérequis (sur chaque PC)
- Docker Desktop : https://www.docker.com/products/docker-desktop
- VS Code : https://code.visualstudio.com/
- Extension VS Code : "Dev Containers" (ms-vscode-remote.remote-containers)

### 2. Utiliser cet environnement

```bash
# Cloner ce repo
git clone https://github.com/votre-username/data-env.git
cd data-env

# Ouvrir dans VS Code
code .

# Dans VS Code : Ctrl+Shift+P
# Taper : "Dev Containers: Reopen in Container"
# Attendre 5-10 min (première fois)
```

**C'EST TOUT !**

---

## Utilisation avec Vos Projets

### Workflow Recommandé

```
Documents/
├── data-env/           # Ce repo (environnement)
│   └── .devcontainer/
│
└── mes-projets/
    ├── projet-A/       # Repo Git séparé
    ├── projet-B/       # Repo Git séparé
    └── projet-C/
```

### Travailler sur un Projet

**Option 1 - Dev Container par Projet (Recommandé)**

Copiez le dossier `.devcontainer` dans chaque projet :

```bash
cp -r data-env/.devcontainer mon-projet/
cd mon-projet
code .
# Ctrl+Shift+P > Reopen in Container
```

**Option 2 - Environnement Partagé**

Utilisez Docker Compose pour les services :

```bash
# Lancer les services (PostgreSQL, etc.)
cd data-env
docker-compose up -d

# Travailler sur votre projet
cd ../mon-projet
code .
# Python se connecte à localhost:5432
```

---

## Packages Installés

- pandas, numpy, polars
- SQLAlchemy, PostgreSQL
- dbt-core, dbt-postgres
- DuckDB
- FastAPI, uvicorn
- JupyterLab
- matplotlib, seaborn, plotly
- pytest, black, pylint

---

## Ajouter des Packages

1. Modifier `.devcontainer/requirements.txt`
2. Rebuild le container :
   - `Ctrl+Shift+P` > "Dev Containers: Rebuild Container"

---

## Synchronisation entre PC

```bash
# PC Fixe
cd data-env
git pull
# Travailler...
git add .
git commit -m "Ajout package X"
git push

# Laptop
cd data-env
git pull
# Ctrl+Shift+P > Rebuild Container
# Même environnement !
```

---

**Bon développement !** 🚀
