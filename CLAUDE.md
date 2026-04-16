# CLAUDE.md — Data Engineering Dev Container

## Contexte du projet

Environnement de développement Data Engineering portable, basé sur Dev Containers (Docker + VS Code).
Ce container est régulièrement éteint et rallumé — la mémoire de conversation entre sessions ne survit pas au redémarrage.

**Stack principale :** Python 3.11, Pandas, PySpark, Airflow 2.8.1, dbt, DuckDB, FastAPI, JupyterLab.

---

## Règle de persistance de mémoire (OBLIGATOIRE)

### Au début de chaque session
1. **Lire le fichier de mémoire** : `C:\Users\Makci\.claude\projects\c--Users-Makci-Documents-data-env\memory\MEMORY.md`
   - Si ce fichier existe, résume son contenu à l'utilisateur pour reconstituer le contexte.
   - S'il n'existe pas encore, mentionner que c'est une nouvelle session sans historique.

### En cours de session
- **Sauvegarder systématiquement** toute information importante dans la mémoire (voir types ci-dessous).
- Thèmes à surveiller : décisions techniques, bugs résolus, choix d'architecture, objectifs en cours, packages ajoutés, DAGs Airflow créés, etc.

### En fin de session (ou dès qu'un sujet important est conclu)
Créer ou mettre à jour les fichiers mémoire dans :
`C:\Users\Makci\.claude\projects\c--Users-Makci-Documents-data-env\memory\`

**Types de mémoire à maintenir :**

| Fichier | Contenu |
|--------|---------|
| `project_status.md` | Travaux en cours, objectifs, décisions prises |
| `technical_decisions.md` | Choix d'architecture, pourquoi tel outil vs un autre |
| `bugs_and_fixes.md` | Problèmes rencontrés et leurs solutions |
| `user_preferences.md` | Préférences de travail, style de code, habitudes |
| `session_log.md` | Résumé chronologique de chaque session de travail |

---

## Format des entrées de session_log.md

```markdown
## Session YYYY-MM-DD
**Objectifs :** ...
**Réalisé :** ...
**En cours / À reprendre :** ...
**Décisions importantes :** ...
```

---

## Rappel sur la persistance container vs host

- La mémoire Claude est stockée sur le **host Windows** (`C:\Users\Makci\.claude\...`), pas dans le container.
- Elle **survit** aux redémarrages du container.
- Le code est dans `c:\Users\Makci\Documents\data-env\` (host) = `/workspaces/data-env/` (container).

---

## Comportement attendu

Quand l'utilisateur ouvre une nouvelle session, Claude doit :
1. Lire MEMORY.md automatiquement.
2. Dire : *"Voici ce que je me rappelle de nos dernières sessions : [résumé]"*
3. Demander si l'utilisateur veut continuer un travail en cours ou démarrer quelque chose de nouveau.
