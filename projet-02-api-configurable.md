## ⚙️ **Niveau 2 — Gestion de la configuration**

### 🎯 Objectif :

Séparer la configuration du code, comprendre comment Kubernetes injecte les variables.

### 🧩 Projet 2 : “API configurable”

**Concepts couverts :**

* ConfigMap
* Secret
* Environment variables
* Volume mount

**Description :**
Déploie une application Spring Boot qui lit une variable d’environnement (ex: message de bienvenue).
Stocke cette variable dans un `ConfigMap`.
Ajoute un mot de passe en `Secret`.
Monte-les dans le conteneur.