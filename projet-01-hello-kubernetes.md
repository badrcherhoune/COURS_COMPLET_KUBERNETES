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

## 1️⃣ Déployer un **Pod simple**

**But** : voir comment Kubernetes exécute un conteneur.

```bash
kubectl run hello-pod --image=nginx --restart=Never
kubectl get pods
kubectl describe pod hello-pod
kubectl logs hello-pod
```

* `kubectl run` → crée un pod unique.
* `kubectl describe` → montre tous les détails et événements du pod.
* `kubectl logs` → affiche la sortie du conteneur.

---

## 2️⃣ Créer un **Deployment**

**But** : gérer plusieurs copies et la montée en charge.

```bash
kubectl create deployment hello-deploy --image=nginx
kubectl get deployments
kubectl get pods
kubectl describe deployment hello-deploy
```

* Kubernetes crée automatiquement un **ReplicaSet**.
* Pour tester plusieurs pods :

```bash
kubectl scale deployment hello-deploy --replicas=3
kubectl get pods -o wide
```

💡 Vérifie la colonne `NODE` pour voir sur quel nœud les pods sont créés.

---

## 3️⃣ Exposer l’application via un **Service**

**But** : rendre ton pod/deployment accessible.

* **ClusterIP** (interne au cluster) :

```bash
kubectl expose deployment hello-deploy --port=80 --target-port=80 --type=ClusterIP
kubectl get services
```

* **NodePort** (externe, via le navigateur) :

```bash
kubectl expose deployment hello-deploy --port=80 --target-port=80 --type=NodePort
kubectl get services
```

* Note le port NodePort (ex : 30080) et teste :

```bash
curl <NODE_IP>:<NODE_PORT>
```

---

## 4️⃣ Nettoyage

```bash
kubectl delete pod hello-pod
kubectl delete deployment hello-deploy
kubectl delete service hello-deploy
```
### Remarque importante : 
Les pods gérés par un Deployment/ReplicaSet se recréent automatiquement si tu les supprimes. Les pods “simples” (kubectl run --restart=Never) ne se recréent pas.
---

### ✅ À retenir

1. **Pod** = instance de conteneur.
2. **Deployment** = gère les pods et la montée en charge.
3. **ReplicaSet** = assure le nombre souhaité de pods.
4. **Service** = abstraction réseau pour exposer les pods.
5. **ClusterIP vs NodePort** = interne vs externe.

---

Si tu veux, je peux te faire **un tableau prêt à copier-coller**, avec toutes les commandes dans l’ordre exact pour Killer Coda, pour que tu puisses suivre ton TP sans te tromper.



