# Exercice 1 – Configuration DVC (Projet Iris)

Ce projet correspond à la correction de l’Exercice 1 : configuration de DVC et préparation du dataset *Iris*.

## 1. Prérequis

- Python 3.10+
- `pip`
- `git`
- `dvc` (installé via `pip` ou `conda`)

## 2. Installation des dépendances

```bash
python -m venv venv
source venv/bin/activate  # sous Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## 3. Étapes de l'exercice

1. Initialiser Git et DVC :
   ```bash
   git init
   dvc init
   ```

2. Télécharger / générer le dataset Iris :
   ```bash
   python scripts/download_iris.py
   ```

3. Ajouter le dataset brut à DVC :
   ```bash
   dvc add data/iris.csv
   git add data/.gitignore data/iris.csv.dvc
   git commit -m "Add raw Iris dataset tracked by DVC"
   ```

4. Configurer un remote local (exemple) :
   ```bash
   mkdir ../dvc_storage
   dvc remote add -d localremote ../dvc_storage
   git add .dvc/config
   git commit -m "Configure local DVC remote"
   ```

5. Créer le dataset prétraité :
   ```bash
   python scripts/preprocess.py
   ```

6. Versionner le dataset prétraité :
   ```bash
   dvc add data/iris_preprocessed.csv
   git add data/iris_preprocessed.csv.dvc
   git commit -m "Add preprocessed Iris dataset"
   ```

7. Tester `dvc push` / `dvc pull` :
   ```bash
   dvc push
   rm data/iris_preprocessed.csv
   dvc pull
   ```

Le projet est ainsi prêt pour servir de base aux exercices suivants (pipeline, métriques, MLOps).
