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