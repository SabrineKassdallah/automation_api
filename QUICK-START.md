# 🚀 Démarrage Rapide - CI/CD GitHub Actions

## ✅ Configuration Complète en 3 Étapes

### Étape 1: Préparation du Dépôt Git

```bash
# Assurez-vous que vous êtes dans le répertoire du projet
cd /home/sabrine/Videos/automation_api

# Vérifiez que git est initialisé
git status
```

### Étape 2: Ajout des Fichiers de Configuration

Les fichiers suivants ont été créés automatiquement:

```
├── .github/
│   ├── workflows/
│   │   └── api-tests.yml              # Workflow principal
│   └── CI-CD-SETUP.md                 # Documentation détaillée
├── package.json                        # Scripts et dépendances
├── .gitignore                          # Fichiers à ignorer
└── QUICK-START.md                      # Ce fichier
```

### Étape 3: Push vers GitHub

```bash
# Ajoutez tous les fichiers
git add .

# Committez les changements
git commit -m "chore: Add GitHub Actions CI/CD pipeline"

# Poussez vers votre dépôt
git push origin main
```

---

## 📊 Vérifier le Pipeline

### Dans GitHub

1. Allez sur votre dépôt GitHub
2. Cliquez sur l'onglet **Actions**
3. Vous devriez voir le workflow **"API Tests CI/CD"** en cours d'exécution
4. Attendez la fin et consultez les résultats

### Localement

Testez les commandes avant de pusher:

```bash
# Installation des dépendances
npm install

# Exécuter les tests (rapport minimal)
npm test

# Générer un rapport HTML
npm run test:html

# Générer tous les rapports (comme le pipeline)
npm run test:all

# Exécuter avec mode verbose (utile pour le débogage)
npm run test:verbose
```

---

## 📈 Résultats et Rapports

### Après chaque Exécution

- 📋 **Rapport HTML** : Consultable via l'onglet Artifacts
- 📊 **Résultats JSON** : Format brut pour l'analyse
- ✅ **Status Check** : Affichée sur les PRs (✔️ ou ❌)
- 💬 **Commentaire PR** : Résumé automatique des résultats

### Ajouter un Badge de Statut

Modifiez votre [README.md](README.md) et ajoutez:

```markdown
[![API Tests](https://github.com/YOUR_USERNAME/automation_api/actions/workflows/api-tests.yml/badge.svg?branch=main)](https://github.com/YOUR_USERNAME/automation_api/actions/workflows/api-tests.yml)
```

---

## 🔄 Exécutions Planifiées

Le pipeline s'exécute automatiquement:

| Événement | Quand |
|-----------|-------|
| **Push** | À chaque commit sur `main` ou `develop` |
| **Pull Request** | À chaque PR vers `main` ou `develop` |
| **Quotidien** | Chaque jour à 09:00 UTC |

---

## 🛠️ Personnalisation

### Ajouter des Branches

Éditez [.github/workflows/api-tests.yml](.github/workflows/api-tests.yml):

```yaml
on:
  push:
    branches: [ main, develop, staging ]
  pull_request:
    branches: [ main, develop, staging ]
```

### Changer l'Horaire Quotidien

Modifiez la section `schedule` dans le workflow (format cron):

```yaml
schedule:
  - cron: '0 9 * * *'  # Actuellement: tous les jours à 09:00 UTC
```

---

## 🐛 Dépannage

### "Le workflow n'apparaît pas dans Actions"

- Vérifiez que le fichier `.github/workflows/api-tests.yml` est pushé
- Attendez quelques secondes et rafraîchissez la page

### "Les tests échouent dans le pipeline mais fonctionnent localement"

- Vérifiez que l'API `https://automationexercise.com` est accessible depuis GitHub Actions
- Consultez les logs détaillés dans GitHub (onglet Actions → Workflow)

### "Les rapports ne s'affichent pas"

- Vérifiez que Newman a généré les fichiers sans erreur
- Consultez les logs de l'étape "Run API Tests"

---

## 📚 Ressources Supplémentaires

- [Documentation Newman](https://learning.postman.com/docs/running-collections/using-newman-cli/)
- [Documentation GitHub Actions](https://docs.github.com/en/actions)
- [Syntaxe YAML Workflow](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)

---

## ✨ Prochaines Étapes

1. ✅ Testez localement: `npm test`
2. ✅ Poussez vers GitHub: `git push`
3. ✅ Vérifiez l'onglet Actions
4. ✅ Consultez les rapports
5. ✅ Itérez et améliorez vos tests

Bon courage! 🎉
