# TP2 : Simulation d'un pipeline CI/CD avec GitHub Actions

**Université Sidi Mohamed Ben Abdellah**  
**École Nationale des Sciences Appliquées de Fès (ENSA Fès)**  
**Filière ILIA / Semestre 5 — DevOps**

---

## 📌 Présentation du Projet
Ce projet implémente et simule un pipeline CI/CD complet à l'aide de **GitHub Actions** pour une application Python de gestion des notes d'étudiants (calcul de moyenne, attribution de mention et validation d'admission).

À chaque modification envoyée sur la branche `main` de GitHub, le pipeline est automatiquement déclenché afin d'exécuter l'ensemble des étapes de vérification, de test et de simulation de déploiement.

---

## 📂 Structure du Répertoire
```
TP-Simulation-CICD/
├── .github/
│   └── workflows/
│       └── cicd.yml           # Configuration du pipeline GitHub Actions
├── app.py                     # Code source de l'application
├── test_app.py                # Tests unitaires avec Pytest
├── requirements.txt           # Dépendances du projet (pytest)
├── .gitignore                 # Fichiers à ignorer par Git
└── README.md                  # Documentation du projet
```

---

## ⚙️ Détail des Fichiers

### 1. `app.py`
Contient la logique métier :
- `calculer_moyenne(notes)` : calcule la moyenne arithmétique d'une liste de notes. Lève une `ValueError` si la liste est vide.
- `mention(moyenne)` : renvoie `"Très bien"` (≥ 16), `"Bien"` (≥ 14), `"Assez bien"` (≥ 12), `"Passable"` (≥ 10) ou `"Ajourné"` (< 10).
- `est_admis(moyenne)` : renvoie un booléen indiquant si la moyenne est supérieure ou égale à 10.

### 2. `test_app.py`
Tests unitaires automatisés avec Pytest :
- `test_calculer_moyenne()` : vérifie le calcul standard.
- `test_liste_notes_vide()` : vérifie la levée de l'exception pour liste vide.
- `test_mention()` : vérifie les seuils de chaque mention.
- `test_est_admis()` : vérifie l'admission et le refus.

### 3. `.github/workflows/cicd.yml`
Définit les 3 jobs ordonnancés avec la directive `needs` :
1. **`build-test`** :
   - Récupération du code source (`actions/checkout@v4`).
   - Configuration de Python 3.12 (`actions/setup-python@v5`).
   - Installation des dépendances via `pip install -r requirements.txt`.
   - Exécution des tests unitaires (`pytest -v`).
2. **`deploy-staging`** (`needs: build-test`) :
   - Simulation du déploiement en préproduction.
   - Génération de l'artefact `application-staging` (`staging/app.txt`).
3. **`deploy-production`** (`needs: deploy-staging`) :
   - Simulation du déploiement en production si staging réussit.
   - Génération de l'artefact `application-production` (`production/app.txt`).

---

## 🚀 Exécution Locale

```bash
# 1. Créer un environnement virtuel (optionnel)
python -m venv venv
venv\Scripts\activate   # Windows

# 2. Installer les dépendances
pip install -r requirements.txt

# 3. Exécuter les tests unitaires
pytest -v
```

---

## 🔄 Commandes Git pour GitHub

```bash
# Lier à votre dépôt distant GitHub
git remote add origin https://github.com/VOTRE_NOM/TP-Simulation-CICD.git

# Envoyer vers GitHub
git branch -M main
git push -u origin main
```
