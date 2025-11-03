

## **Problème du Projet 2 – Gestion de la configuration**

Ton application a des paramètres (mode, message, mot de passe…) **codés en dur**.

**Objectif :**

* Déplacer ces paramètres dans Kubernetes.
* Utiliser **ConfigMap** pour les données normales et **Secret** pour les mots de passe.
* Faire en sorte que l’application prenne les changements **sans reconstruire l’image**.
