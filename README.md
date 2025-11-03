# 🧩 COURS COMPLET KUBERNETES POUR DEVOPS

---

## 🧱 1. INTRODUCTION À KUBERNETES

### 🔹 Qu’est-ce que Kubernetes ?

Kubernetes (K8s) est une **plateforme d’orchestration de conteneurs** open source développée par Google, aujourd’hui maintenue par la **Cloud Native Computing Foundation (CNCF)**.
Son objectif : **déployer, gérer et faire évoluer automatiquement** des applications conteneurisées (ex. Docker).

### 🔹 Pourquoi l’utiliser ?

* Déploiement automatisé des conteneurs
* Scalabilité automatique (auto-scaling)
* Reprise après panne (self-healing)
* Rolling updates (mises à jour progressives)
* Load balancing intégré
* Déploiements reproductibles

---

## ⚙️ 2. ARCHITECTURE KUBERNETES

### 📦 Composants principaux
<img src="./images/kubernetes-cluster-architecture.svg" alt="My App"/>

#### 🧠 **Control Plane**

1. **kube-apiserver** — point d’entrée (API REST) de K8s
2. **etcd** — base de données clé/valeur pour l’état du cluster
3. **kube-scheduler** — décide où placer les pods
4. **kube-controller-manager** — gère les boucles de contrôle (repliques, nœuds, etc.)

#### 🖥️ **Node (Worker)**

1. **kubelet** — agent qui exécute les conteneurs sur le nœud
2. **kube-proxy** — gère le réseau et le load-balancing
3. **Container runtime** — Docker, containerd, CRI-O...

---

## 🚀 3. CONCEPTS CLÉS

### 🔸 **Pod**

L’unité de base dans K8s.
Un pod = 1 ou plusieurs conteneurs partageant le même réseau et stockage.

### 🔸 **ReplicaSet**

Assure qu’un nombre fixe de pods identiques sont toujours en exécution.

### 🔸 **Deployment**

Objet qui gère les ReplicaSets et permet des **mises à jour continues (rolling updates)**.

### 🔸 **Service**

Expose un ensemble de pods via une **adresse IP stable**.
Types :

* ClusterIP (interne)
* NodePort (externe via un port)
* LoadBalancer (via un load balancer cloud)
* ExternalName (DNS externe)

### 🔸 **Namespace**

Permet d’isoler les ressources (environnements dev, test, prod).

### 🔸 **ConfigMap & Secret**

* **ConfigMap** : variables non sensibles
* **Secret** : données sensibles (mots de passe, clés API…)

### 🔸 **Volume & PersistentVolume**

* Volume = stockage rattaché à un pod
* PersistentVolume = stockage indépendant du cycle de vie du pod
* PersistentVolumeClaim (PVC) = requête de stockage faite par le pod

---

## 🌐 4. RÉSEAU KUBERNETES

### 🔹 Concepts

* Chaque pod a sa propre IP.
* Tous les pods peuvent communiquer entre eux (par défaut).
* Les Services assurent la **découverte DNS interne**.

### 🔹 Ingress

Objet K8s pour **gérer le trafic HTTP/HTTPS** vers les services internes (avec NGINX Ingress Controller par exemple).

---

## 🧰 5. MANIFESTES YAML

Les objets K8s sont décrits en YAML.
Exemple : **Deployment**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

## 🧪 6. COMMANDES `kubectl` ESSENTIELLES

| Action                  | Commande                                               |
| ----------------------- | ------------------------------------------------------ |
| Voir les pods           | `kubectl get pods`                                     |
| Voir les services       | `kubectl get svc`                                      |
| Déployer un YAML        | `kubectl apply -f fichier.yaml`                        |
| Supprimer une ressource | `kubectl delete -f fichier.yaml`                       |
| Voir les logs           | `kubectl logs pod-name`                                |
| Entrer dans un pod      | `kubectl exec -it pod-name -- bash`                    |
| Changer de namespace    | `kubectl config set-context --current --namespace=dev` |

---

## 🧩 7. CONCEPTS AVANCÉS

### 🌀 **DaemonSet**

Déploie un pod sur **chaque nœud** (ex: monitoring, log agent).

### ⚖️ **StatefulSet**

Gère des applications **avec état** (bases de données, Kafka…).

### 🧭 **Job & CronJob**

* **Job** : exécute une tâche unique
* **CronJob** : exécute une tâche planifiée (comme un cron Linux)

### 🧬 **Labels, Selectors, Annotations**

* **Labels** : tags pour identifier des objets
* **Selectors** : filtres basés sur les labels
* **Annotations** : métadonnées non utilisées pour la sélection

---

## 🧠 8. HAUTE DISPONIBILITÉ ET SCALING

### 🔹 Horizontal Pod Autoscaler (HPA)

Ajuste le nombre de pods selon la charge CPU/mémoire.

```bash
kubectl autoscale deployment my-app --min=2 --max=5 --cpu-percent=80
```

### 🔹 Vertical Pod Autoscaler (VPA)

Ajuste les ressources CPU/mémoire assignées aux pods.

### 🔹 Cluster Autoscaler

Ajoute ou supprime des **nœuds** selon la charge globale.

---

## 🛡️ 9. SÉCURITÉ DANS KUBERNETES

* **RBAC (Role-Based Access Control)** : contrôle des permissions
* **Service Account** : compte utilisé par des pods pour accéder à l’API
* **Network Policies** : contrôle du trafic entre pods
* **Pod Security Policies (PSP)** : définit les règles de sécurité des pods
* **Secrets chiffrés** via etcd

---

## 🧩 10. OBSERVABILITÉ ET MONITORING

### 🔹 Logs

* `kubectl logs pod-name`
* Intégration avec **ELK Stack** (Elastic, Logstash, Kibana)

### 🔹 Metrics

* **Metrics Server** (CPU/RAM)
* **Prometheus + Grafana** (dashboard complet)

### 🔹 Tracing

* **Jaeger / OpenTelemetry** pour tracer les requêtes inter-services

---

## 🧩 11. CI/CD AVEC KUBERNETES

Intégration avec :

* **Jenkins / GitLab CI / GitHub Actions**
* Déploiement automatisé avec `kubectl` ou **Helm**
* Stratégies de déploiement :

  * Rolling Update
  * Blue/Green Deployment
  * Canary Deployment

---

## ⚓ 12. HELM

### 🔹 Définition

Helm est le **gestionnaire de packages pour Kubernetes**.

### 🔹 Concepts

* **Chart** : modèle de configuration (application)
* **Values.yaml** : fichier de variables
* **Release** : instance déployée d’un chart

### 🔹 Commandes

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-app bitnami/nginx
helm upgrade my-app bitnami/nginx
helm uninstall my-app
```

---

## 🌥️ 13. DÉPLOIEMENT CLOUD

Kubernetes est disponible sur :

* **GKE** (Google)
* **EKS** (AWS)
* **AKS** (Azure)
* **K3s** (léger pour dev local)
* **Minikube / Kind** (pour pratiquer en local)

---

## 🧩 14. TROUBLESHOOTING

| Problème             | Commande utile                                    |
| -------------------- | ------------------------------------------------- |
| Pod bloqué           | `kubectl describe pod <name>`                     |
| CrashLoopBackOff     | `kubectl logs <pod>`                              |
| Service inaccessible | `kubectl get endpoints`                           |
| DNS interne          | `kubectl exec -it <pod> -- nslookup service-name` |

---

## 🧭 15. PROJETS POUR PRATIQUER

1. **Déployer une appli Nginx + backend Node.js + base MongoDB**
2. Ajouter un **Ingress NGINX**
3. Gérer les configs avec **ConfigMap / Secret**
4. Mettre en place **HPA** (autoscaling)
5. Intégrer **Prometheus + Grafana**
6. Déployer via **Helm Chart**
7. Automatiser avec **GitHub Actions**

---

Souhaites-tu que je te crée un **plan de formation pratique (jour par jour)** avec exercices et mini-projets pour maîtriser Kubernetes en **2 à 3 semaines** ?
Cela te permettra de passer du niveau “je comprends” à **“je maîtrise en entreprise”**.
