Parfait Badr 😎, je vais te donner **toutes les commandes Kubernetes essentielles**, organisées par thème, avec des explications concises. Ces commandes couvrent **tous les aspects d’un cluster K8s**, du déploiement des applications à l’administration complète.

---

# **1️⃣ Gestion des clusters**

```bash
kubectl cluster-info                 # Informations sur le cluster actuel
kubectl get nodes                    # Liste des nœuds du cluster
kubectl describe node <nom-node>     # Détails sur un nœud
kubectl top node                     # Utilisation CPU/mémoire des nœuds
kubectl get namespaces               # Liste des namespaces
kubectl create namespace <nom>       # Créer un namespace
kubectl delete namespace <nom>       # Supprimer un namespace
```

---

# **2️⃣ Gestion des Pods**

```bash
kubectl get pods                     # Liste des pods dans le namespace courant
kubectl get pods -n <namespace>      # Liste des pods dans un namespace spécifique
kubectl describe pod <nom-pod>       # Détails d’un pod
kubectl logs <nom-pod>               # Afficher les logs d’un pod
kubectl logs -f <nom-pod>            # Suivre les logs en temps réel
kubectl exec -it <nom-pod> -- bash   # Accéder au shell d’un pod
kubectl delete pod <nom-pod>         # Supprimer un pod
kubectl apply -f pod.yaml             # Créer ou mettre à jour un pod à partir d’un fichier YAML
```

---

# **3️⃣ Gestion des Deployments**

```bash
kubectl get deployments               # Liste des déploiements
kubectl describe deployment <nom>     # Détails d’un déploiement
kubectl apply -f deployment.yaml      # Créer ou mettre à jour un déploiement
kubectl scale deployment <nom> --replicas=3  # Changer le nombre de pods
kubectl rollout status deployment/<nom>      # Voir l’état du déploiement
kubectl rollout undo deployment/<nom>        # Revenir à la version précédente
```

---

# **4️⃣ Gestion des ReplicaSets**

```bash
kubectl get rs                        # Liste des ReplicaSets
kubectl describe rs <nom>             # Détails d’un ReplicaSet
kubectl delete rs <nom>               # Supprimer un ReplicaSet
```

---

# **5️⃣ Gestion des Services**

```bash
kubectl get svc                       # Liste des services
kubectl describe svc <nom>            # Détails d’un service
kubectl apply -f service.yaml         # Créer ou mettre à jour un service
kubectl delete svc <nom>              # Supprimer un service
```

**Types de services :** ClusterIP (interne), NodePort (externe via port), LoadBalancer (Cloud).

---

# **6️⃣ Gestion des ConfigMaps et Secrets**

```bash
kubectl get configmap                 # Liste des ConfigMaps
kubectl describe configmap <nom>      # Détails d’un ConfigMap
kubectl apply -f configmap.yaml       # Créer/mettre à jour un ConfigMap

kubectl get secret                     # Liste des secrets
kubectl describe secret <nom>          # Détails d’un secret
kubectl apply -f secret.yaml           # Créer/mettre à jour un secret
```

---

# **7️⃣ Gestion du stockage**

```bash
kubectl get pv                         # Liste des volumes persistants
kubectl get pvc                        # Liste des claims de volume
kubectl describe pvc <nom>             # Détails d’un PVC
kubectl apply -f pvc.yaml              # Créer/mettre à jour un PVC
kubectl delete pvc <nom>               # Supprimer un PVC
```

---

# **8️⃣ Monitoring et scaling**

```bash
kubectl top pod                        # Utilisation CPU/mémoire des pods
kubectl top pod <nom-pod>              # Pod spécifique
kubectl get hpa                         # Liste des HorizontalPodAutoscalers
kubectl apply -f hpa.yaml               # Créer/mettre à jour un HPA
kubectl delete hpa <nom>                # Supprimer un HPA
```

---

# **9️⃣ Gestion des Ingress**

```bash
kubectl get ingress                    # Liste des Ingress
kubectl describe ingress <nom>         # Détails d’un Ingress
kubectl apply -f ingress.yaml          # Créer ou mettre à jour un Ingress
kubectl delete ingress <nom>           # Supprimer un Ingress
```

---

# **🔟 Commandes avancées**

```bash
kubectl get all                        # Liste tous les objets (pods, svc, deployments...)
kubectl apply -f .                      # Appliquer tous les fichiers YAML du dossier courant
kubectl delete -f .                     # Supprimer tous les objets du dossier
kubectl explain <ressource>             # Explications sur une ressource K8s (ex: pod, deployment)
kubectl get events                       # Voir les événements récents du cluster
kubectl get secrets --show-labels        # Voir les secrets avec labels
kubectl auth can-i <action> <resource>  # Vérifier les permissions RBAC
kubectl port-forward <pod> 8080:80      # Forwarder un port local vers un pod
kubectl cp <pod>:/path/file ./localfile # Copier un fichier depuis un pod
kubectl apply -k <dir>                   # Appliquer un Kustomize directory
kubectl diff -f <file>                   # Voir les changements avant de les appliquer
```

---

# **1️⃣1️⃣ Helm (optionnel mais essentiel pour projets avancés)**

```bash
helm repo add stable https://charts.helm.sh/stable
helm repo update
helm install <nom-release> <chart>       # Installer un chart
helm upgrade <nom-release> <chart>       # Mettre à jour un chart
helm rollback <nom-release> <revision>   # Revenir à une version précédente
helm uninstall <nom-release>             # Supprimer une release
helm list                                # Lister les releases
```

---

💡 **Astuce pratique :**
Pour ne jamais oublier une commande, tu peux créer un **fichier cheat-sheet Markdown** pour ton apprentissage, avec **commandes + description + exemples d’usage** pour chaque projet.
