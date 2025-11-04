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

---

# pratique:

## 🧩 **Étape 1 — Déploiement**

Applique les fichiers dans ton cluster :

```bash
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

## 🧾 **Étape 2 — Vérification**

🔹 Vérifie les ressources :

```bash
kubectl get configmaps
kubectl get secrets
kubectl get pods
kubectl get services
```

🔹 Ouvre un shell dans le pod :

```bash
kubectl exec -it <nom-du-pod> -- sh
```

🔹 Vérifie que les variables sont bien injectées :

```bash
echo $WELCOME_MESSAGE
echo $DB_PASSWORD
```

---

## 🧠 **Étape 4 — Option bonus (volume mount visible)**

Dans le conteneur, regarde le contenu monté depuis le ConfigMap :

```bash
cat /config/WELCOME_MESSAGE
```
