# GitHub Actions CI/CD Pipeline

## Configuration du Pipeline

Un pipeline CI/CD automatisé a été mis en place pour exécuter les tests API à chaque push et pull request.

### Fichier Workflow

📍 `.github/workflows/api-tests.yml`

## Déclencheurs

Le pipeline s'exécute automatiquement dans les cas suivants:

- ✅ **Push** sur les branches `main` ou `develop`
- ✅ **Pull Request** vers les branches `main` ou `develop`
- ✅ **Planifié** quotidiennement à 09:00 UTC

## Ce que fait le Pipeline

1. **Checkout** du code
2. **Installation** de Node.js (versions 18.x et 20.x)
3. **Installation** de Newman et ses reporters
4. **Exécution** des tests API avec les fichiers:
   - `AutomationExercise_API_Testing.postman_collection.json`
   - `AutomationExercise.postman_environment.json`
5. **Génération** des rapports de test (JSON, HTML, JUnit XML)
6. **Upload** des artefacts (rapports de test)
7. **Publication** des résultats des tests
8. **Commentaire** automatique sur les PRs avec un résumé

## Résultats et Rapports

### Accès aux Résultats

- 📊 Allez à l'onglet **Actions** de votre dépôt GitHub
- 📈 Sélectionnez le workflow **"API Tests CI/CD"**
- 📋 Consultez les détails de chaque exécution

### Artefacts Générés

Pour chaque exécution, les artefacts suivants sont disponibles (30 jours):

| Type | Description |
|------|-------------|
| `newman-results.json` | Résultats bruts en JSON |
| `newman-results.xml` | Format JUnit pour l'intégration |
| `newman-report.html` | Rapport HTML visuel |

### Rapport HTML

Le rapport HTML peut être consulté:
1. Via l'onglet **Artifacts** dans l'exécution du workflow
2. Télécharger et ouvrir localement dans votre navigateur

## Configuration Locale

Pour exécuter les tests localement comme le fait le pipeline:

```bash
# Installation unique
npm install -g newman newman-reporter-html newman-reporter-junitxml

# Exécution des tests
newman run AutomationExercise_API_Testing.postman_collection.json \
  -e AutomationExercise.postman_environment.json \
  --reporters cli,json,junit,html
```

## Personnalisation

### Modifier les Branches

Editez `.github/workflows/api-tests.yml` pour ajouter/modifier les branches:

```yaml
on:
  push:
    branches: [ main, develop, staging ]
  pull_request:
    branches: [ main, develop, staging ]
```

### Modifier l'Horaire

Changez la fréquence des exécutions planifiées (syntaxe cron):

```yaml
schedule:
  - cron: '0 9 * * *'  # Tous les jours à 09:00 UTC
```

Exemples:
- `0 9 * * 1-5` → Jours de semaine à 09:00
- `0 */6 * * *` → Toutes les 6 heures
- `0 0 * * 0` → Chaque dimanche à minuit

### Ajouter des Versions Node.js

```yaml
strategy:
  matrix:
    node-version: [16.x, 18.x, 20.x]
```

## Status Badge

Ajoutez ce badge à votre README.md pour afficher le statut du pipeline:

```markdown
[![API Tests](https://github.com/YOUR_USERNAME/YOUR_REPO/actions/workflows/api-tests.yml/badge.svg)](https://github.com/YOUR_USERNAME/YOUR_REPO/actions/workflows/api-tests.yml)
```

Remplacez `YOUR_USERNAME` et `YOUR_REPO` par vos valeurs.

## Dépannage

### Les tests ne s'exécutent pas

1. Vérifiez que le fichier `.github/workflows/api-tests.yml` existe
2. Vérifiez les permissions du dépôt (Settings → Actions)
3. Consultez l'onglet **Actions** pour voir les logs d'erreur

### Les rapports ne s'affichent pas

- Vérifiez que les fichiers JSON et XML sont bien générés
- Assurez-vous que Newman est correctement installé

### Échec des tests

- Vérifiez que l'environnement Postman est correctement configuré
- Vérifiez que l'API est accessible
- Consultez les logs détaillés dans GitHub Actions

## Support

Pour plus d'informations:
- [Documentation Newman](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)
- [Documentation GitHub Actions](https://docs.github.com/en/actions)
