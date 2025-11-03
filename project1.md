

## 🚀 **Niveau 1 — Les bases (Pods, Deployments, Services)**

### 🎯 Objectif :

Comprendre le cœur de Kubernetes : comment il gère les conteneurs, le réseau, et la montée en charge.

### 🧩 Projet 1 : “Hello Kubernetes”

**Concepts couverts :**

* Pod
* Deployment
* ReplicaSet
* Service (ClusterIP, NodePort)

**Description :**
Déploie une simple application Nginx ou une API Java Spring Boot sur un cluster K8s local (Minikube ou K3s).
Expose-la via un `Service NodePort` et accède à ton app via le navigateur.

---

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

## 🧠 **Niveau 3 — Stockage persistant**

### 🎯 Objectif :

Gérer les données persistantes (bases de données, fichiers…).

### 🧩 Projet 3 : “Todo App avec base PostgreSQL”

**Concepts couverts :**

* PersistentVolume (PV)
* PersistentVolumeClaim (PVC)
* StatefulSet
* Service type ClusterIP

**Description :**
Déploie PostgreSQL dans Kubernetes avec un volume persistant.
Déploie une app (Java ou Node.js) connectée à cette base.
Teste la persistance après suppression du Pod.

---

## 🧩 **Niveau 4 — Architecture microservices**

### 🎯 Objectif :

Faire communiquer plusieurs services dans le cluster.

### 🧩 Projet 4 : “E-commerce simplifié”

**Concepts couverts :**

* Multi Deployments (service-produit, service-client, service-commande)
* Services internes (ClusterIP)
* Communication inter-pods
* Health probes (liveness, readiness)

**Description :**
Chaque microservice a son propre déploiement.
Ils communiquent via leurs services internes (ex : `http://product-service:8080`).
Ajoute des `readinessProbe` et `livenessProbe` pour surveiller leur état.

---

## 🌐 **Niveau 5 — Ingress et Load Balancer**

### 🎯 Objectif :

Apprendre à exposer plusieurs services via un seul point d’entrée.

### 🧩 Projet 5 : “Application front + API + DB”

**Concepts couverts :**

* Ingress Controller (NGINX Ingress)
* Service type LoadBalancer
* TLS (certificat auto-signé)

**Description :**
Déploie :

* un front Angular ou React (Nginx)
* une API backend
* une base PostgreSQL

Configure un **Ingress** pour router :

* `/api` → backend
* `/` → frontend

---

## 🛠️ **Niveau 6 — CI/CD & déploiement automatique**

### 🎯 Objectif :

Automatiser le build, le push et le déploiement.

### 🧩 Projet 6 : “Pipeline GitHub Actions + K8s”

**Concepts couverts :**

* GitHub Actions ou GitLab CI
* kubectl + kubeconfig
* Image Docker build & push
* Déploiement automatisé

**Description :**
Crée un pipeline qui :

1. Build ton image Docker
2. Push sur Docker Hub
3. Déploie automatiquement sur ton cluster (kubectl apply)

---

## 🧩 **Niveau 7 — Observabilité et logs**

### 🎯 Objectif :

Surveiller ton cluster et tes apps.

### 🧩 Projet 7 : “Monitoring complet”

**Concepts couverts :**

* Metrics Server
* Prometheus
* Grafana
* Logs (kubectl logs, EFK Stack)

**Description :**
Installe Prometheus et Grafana via Helm.
Ajoute un dashboard pour suivre CPU/mémoire de ton app.
Visualise les logs applicatifs.

---

## ☸️ **Niveau 8 — Helm & production-ready**

### 🎯 Objectif :

Gérer les déploiements complexes et réutilisables.

### 🧩 Projet 8 : “Helm chart complet d’une app microservice”

**Concepts couverts :**

* Helm chart
* Values.yaml
* Templates
* Versioning et release upgrade

**Description :**
Crée un **chart Helm** qui déploie ton app e-commerce complète (front + backend + DB).
Teste le `helm upgrade` et le rollback.

---

## 🔥 **Niveau 9 — Avancé (Autoscaling, NetworkPolicy, Secrets Manager)**

### 🎯 Objectif :

Faire du Kubernetes professionnel.

### 🧩 Projet 9 : “Scalable app sécurisée”

**Concepts couverts :**

* HorizontalPodAutoscaler (HPA)
* Resource limits
* NetworkPolicy
* RBAC
* ServiceAccount

**Description :**
Ajoute l’autoscaling selon la charge CPU.
Limite les ressources de tes pods.
Définis une `NetworkPolicy` qui restreint les flux réseau entre services.
Ajoute une sécurité RBAC.

---

## 💡 **Bonus :**

* Utilise **Lens** ou **K9s** pour visualiser ton cluster.
* Essaie **K3s** pour un cluster léger en local.
* Quand tu seras à l’aise, teste le **déploiement sur un vrai Cloud** (GKE, EKS, AKS, ou DigitalOcean K8s).

---

Souhaites-tu que je te crée un **plan de progression sur 4 à 6 semaines** avec ces projets (par jour/semaine) pour te guider étape par étape jusqu’à la maîtrise complète de K8s ?