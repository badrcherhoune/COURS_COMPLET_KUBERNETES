
## 1️⃣ Structure du Helm Chart

```
ecommerce-chart/
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── _helpers.tpl
│   ├── product-deployment.yaml
│   ├── product-service.yaml
│   ├── client-deployment.yaml
│   ├── client-service.yaml
│   ├── order-deployment.yaml
│   └── order-service.yaml
```

---

## 2️⃣ `Chart.yaml`

```yaml
apiVersion: v2
name: ecommerce-chart
description: Helm chart pour un e-commerce microservices
type: application
version: 0.1.0
appVersion: "1.0"
```

---

## 3️⃣ `values.yaml`

```yaml
replicaCount: 1

productService:
  image: "badrcherhoune/product-service:latest"
  port: 8080

clientService:
  image: "badrcherhoune/client-service:latest"
  port: 8081

orderService:
  image: "badrcherhoune/order-service:latest"
  port: 8082
```

---

## 4️⃣ `templates/_helpers.tpl`

```yaml
{{/* Nom complet pour les ressources */}}
{{- define "ecommerce.fullname" -}}
{{ .Release.Name }}-{{ .Chart.Name }}
{{- end -}}
```

---

## 5️⃣ Déploiements et services

### 🔹 `templates/product-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "ecommerce.fullname" . }}-product
spec:
  replicas: {{ .Values.replicaCount }}
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
          image: {{ .Values.productService.image }}
          ports:
            - containerPort: {{ .Values.productService.port }}
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: {{ .Values.productService.port }}
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: {{ .Values.productService.port }}
            initialDelaySeconds: 10
            periodSeconds: 15
```

### 🔹 `templates/product-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ include "ecommerce.fullname" . }}-product
spec:
  selector:
    app: product
  ports:
    - protocol: TCP
      port: {{ .Values.productService.port }}
      targetPort: {{ .Values.productService.port }}
  type: ClusterIP
```

---

### 🔹 `templates/client-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "ecommerce.fullname" . }}-client
spec:
  replicas: {{ .Values.replicaCount }}
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
          image: {{ .Values.clientService.image }}
          ports:
            - containerPort: {{ .Values.clientService.port }}
          env:
            - name: PRODUCT_API_URL
              value: "http://{{ include "ecommerce.fullname" . }}-product:{{ .Values.productService.port }}/products"
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: {{ .Values.clientService.port }}
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: {{ .Values.clientService.port }}
            initialDelaySeconds: 10
            periodSeconds: 15
```

### 🔹 `templates/client-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ include "ecommerce.fullname" . }}-client
spec:
  selector:
    app: client
  ports:
    - protocol: TCP
      port: {{ .Values.clientService.port }}
      targetPort: {{ .Values.clientService.port }}
  type: ClusterIP
```

---

### 🔹 `templates/order-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "ecommerce.fullname" . }}-order
spec:
  replicas: {{ .Values.replicaCount }}
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
          image: {{ .Values.orderService.image }}
          ports:
            - containerPort: {{ .Values.orderService.port }}
          env:
            - name: CLIENT_API_URL
              value: "http://{{ include "ecommerce.fullname" . }}-client:{{ .Values.clientService.port }}/clients"
            - name: PRODUCT_API_URL
              value: "http://{{ include "ecommerce.fullname" . }}-product:{{ .Values.productService.port }}/products"
          readinessProbe:
            httpGet:
              path: /actuator/health
              port: {{ .Values.orderService.port }}
            initialDelaySeconds: 5
            periodSeconds: 10
          livenessProbe:
            httpGet:
              path: /actuator/health
              port: {{ .Values.orderService.port }}
            initialDelaySeconds: 10
            periodSeconds: 15
```

### 🔹 `templates/order-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ include "ecommerce.fullname" . }}-order
spec:
  selector:
    app: order
  ports:
    - protocol: TCP
      port: {{ .Values.orderService.port }}
      targetPort: {{ .Values.orderService.port }}
  type: ClusterIP
```

---

## 6️⃣ **Installation du Helm Chart**

```bash
helm install ecommerce ./ecommerce-chart
```

Vérifie les pods et services :

```bash
kubectl get pods
kubectl get svc
```

---

💡 Avec ce chart, tu peux facilement :

* Modifier le nombre de replicas dans `values.yaml`
* Changer les images ou ports des services
* Déployer et mettre à jour tous les microservices en une seule commande `helm upgrade`.

