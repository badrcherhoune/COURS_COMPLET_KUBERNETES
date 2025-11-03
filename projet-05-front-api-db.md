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