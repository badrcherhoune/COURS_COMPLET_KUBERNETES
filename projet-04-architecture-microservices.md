Voici ton **TP complet pour le Niveau 4 — Architecture microservices** 👇

---

## 🧩 **Niveau 4 — Architecture microservices**

### 🎯 **Objectif :**

Faire communiquer plusieurs services dans un cluster Kubernetes.

---

## 🚀 **Projet 4 : “E-commerce simplifié”**

### 🧠 **Concepts couverts :**

* Multi Deployments (service-produit, service-client, service-commande)
* Services internes (ClusterIP)
* Communication inter-pods
* Health probes (`livenessProbe`, `readinessProbe`)

---

## 🧩 **Étape 1 — Structure du projet**

Crée un dossier :

```bash
mkdir k8s-ecommerce
cd k8s-ecommerce
```

Tu auras à l’intérieur :

```
k8s-ecommerce/
├── product-deployment.yaml
├── client-deployment.yaml
├── order-deployment.yaml
├── product-service.yaml
├── client-service.yaml
├── order-service.yaml
```

---

## 🧩 **Étape 2 — Exemple de microservice “produit”**

### 🧱 `product-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: product-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: product
  template:
    metadata:
      labels:
        app: product
    spec:
      containers:
        - name: product
          image: badrcherhoune/product-service:latest
          ports:
            - containerPort: 8080
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 15
```

### ⚙️ `product-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: product-service
spec:
  selector:
    app: product
  ports:
    - protocol: TCP
      port: 8080
      targetPort: 8080
  type: ClusterIP
```

---

## 🧩 **Étape 3 — Microservice “client”**

### 🧱 `client-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: client-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: client
  template:
    metadata:
      labels:
        app: client
    spec:
      containers:
        - name: client
          image: badrcherhoune/client-service:latest
          ports:
            - containerPort: 8081
          env:
            - name: PRODUCT_API_URL
              value: "http://product-service:8080/products"
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: 8081
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: 8081
            initialDelaySeconds: 10
            periodSeconds: 15
```

### ⚙️ `client-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: client-service
spec:
  selector:
    app: client
  ports:
    - protocol: TCP
      port: 8081
      targetPort: 8081
  type: ClusterIP
```

---

## 🧩 **Étape 4 — Microservice “commande”**

### 🧱 `order-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: order
  template:
    metadata:
      labels:
        app: order
    spec:
      containers:
        - name: order
          image: badrcherhoune/order-service:latest
          ports:
            - containerPort: 8082
          env:
            - name: CLIENT_API_URL
              value: "http://client-service:8081/clients"
            - name: PRODUCT_API_URL
              value: "http://product-service:8080/products"
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: 8082
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: 8082
            initialDelaySeconds: 10
            periodSeconds: 15
```

### ⚙️ `order-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: order-service
spec:
  selector:
    app: order
  ports:
    - protocol: TCP
      port: 8082
      targetPort: 8082
  type: ClusterIP
```

---

## 🧩 **Étape 5 — Déploiement dans le cluster**

Applique les fichiers dans ton cluster :

```bash
kubectl apply -f product-deployment.yaml
kubectl apply -f product-service.yaml

kubectl apply -f client-deployment.yaml
kubectl apply -f client-service.yaml

kubectl apply -f order-deployment.yaml
kubectl apply -f order-service.yaml
```

---

## 🧾 **Étape 6 — Vérification**

Vérifie les ressources :

```bash
kubectl get pods
kubectl get services
kubectl get deployments
```

Teste la communication entre services :

```bash
kubectl exec -it <nom-du-pod-client> -- curl http://product-service:8080/products
```

---

## 🧠 **Remarques importantes**

* Chaque service communique via **son nom DNS interne**, ex : `product-service:8080`.
* Les probes permettent à Kubernetes de redémarrer les pods non sains.
* Tu peux ajouter un **Ingress** (niveau 5) pour exposer `order-service` à l’extérieur.

