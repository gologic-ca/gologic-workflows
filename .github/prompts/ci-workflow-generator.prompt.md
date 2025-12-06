---
mode: "agent"
description: 'Generate CI pipeline based on reusable workflows'
---

# Objective
Analyser le type de langage et framework d'une application et générer un fichier de workflow GitHub Actions `ci.yml` statique qui utilise le bon workflow réutilisable disponible dans `.github/workflows`.

# As a [Role]
**DevOps Engineer** expert en CI/CD, GitHub Actions, et automation de pipelines avec une connaissance approfondie des écosystèmes de développement multi-langages (Java, Python, Node.js, Go, etc.) et capable d'analyser la structure des projets.

# Context
Le repository `https://github.com/gologic-ca/gologic-workflows` contient plusieurs workflows réutilisables spécialisés. 
Les workflows sont tous décrits dans le [README](https://github.com/gologic-ca/gologic-workflows/README.md)

L'objectif est d'analyser les workflows GitHub présents dans le repository pour déterminer le type d'application et générer un `ci.yml` statique qui appelle directement le bon workflow réutilisable.

# Identified Problems
- Configuration manuelle requise pour chaque nouveau projet
- Sélection incorrecte du workflow approprié selon le langage/framework
- Temps de setup initial élevé pour nouveaux repositories
- Incohérence dans l'utilisation des workflows réutilisables
- Risque d'erreurs dans la sélection du bon pipeline CI/CD

# Refactoring Objective
- Automatiser l'analyse du type d'application basée sur les fichiers présents
- Générer le bon workflow CI/CD statique selon le langage détecté
- Simplifier l'onboarding de nouveaux projets avec le bon pipeline
- Assurer l'utilisation cohérente des workflows réutilisables
- Éliminer les erreurs de configuration manuelle

# Technical Constraints
- Utiliser GitHub Actions uniquement
- Réutiliser les workflows existants dans `https://github.com/gologic-ca/gologic-workflows/.github/workflows`
- Générer un workflow statique (pas de détection runtime)
- Analyse des fichiers de projet : pom.xml, build.gradle, pyproject.toml, package.json, go.mod
- Support des langages : Java (Maven/Gradle), Python (Poetry), Node.js, Go
- Le workflow généré doit appeler directement le bon workflow réutilisable
- Gestion des secrets et variables d'environnement selon le type détecté
- Générer seulement un workflow, pas de documentation ou autre fichier
- **UNIQUEMENT utiliser les workflows réutilisables disponibles** - ne pas créer de jobs personnalisés supplémentaires
- **Se limiter strictement** aux workflows réutilisables existants
- **Aucun job custom** ne doit être ajouté

# Expected Output
Analyse d'abord les fichiers présents dans le repository pour identifier le type d'application, puis génère un fichier `ci.yml` statique qui :
- Appelle directement le workflow réutilisable approprié (ex: `uses: gologic-ca/gologic-workflows/.github/workflows/maven-build.yml@main`)
- Configure les déclencheurs appropriés (push, PR, release)
- Passe les bons paramètres au workflow réutilisable
- Inclut les jobs de test si applicable (ex: appel de `maven-test.yml` ou `gradle-test.yml`)
- Configure les permissions nécessaires
- **Se contente uniquement** des workflows réutilisables existants sans ajouter d'autres jobs

Logique de détection :
- Si `pom.xml` présent → utiliser `maven-build.yml` et `maven-test.yml`
- Si `build.gradle` présent → utiliser `gradle-build.yml` et `gradle-test.yml`
- Si `pyproject.toml` présent → utiliser `poetry-build.yml`
- Si `package.json` présent → créer workflow Node.js (à développer)
- Si `go.mod` présent → créer workflow Go (à développer)

# Style and Best Practices
- Suivre les **GitHub Actions best practices**
- Utiliser des **workflow réutilisables uniquement**
- Implémenter une logique simple et directe (pas de conditions complexes)
- Passer les **paramètres** appropriés aux workflows réutilisables
- Gérer les **permissions** de manière sécurisée
- Nommer les jobs de manière explicite selon le type détecté
- Utiliser des **environments** pour la production si nécessaire
- Documenter le type d'application détecté en commentaire
- **Éviter tout job personnalisé** en dehors des workflows réutilisables

# Expected Response Format
- **Première étape** : Analyser les fichiers présents et identifier le type d'application
- **Deuxième étape** : Fournir le fichier `ci.yml` statique et commenté adapté au type détecté
- Expliquer pourquoi ce workflow réutilisable a été choisi
- Lister les paramètres passés au workflow réutilisable
- Donner des exemples de customisation possible
- Inclure les prérequis (secrets, variables) selon le type détecté
- **Confirmer que seuls les workflows réutilisables sont utilisés**
