# Documentation Technique Complète du Projet Minikube

## Description du Projet

Ce projet est un site web de gestion des tâches utilisant Node.js pour le backend, React pour le frontend, et PostgreSQL pour la base de données. Les composants sont conteneurisés avec Docker et déployés sur un cluster Minikube utilisant Kubernetes.

## Pré-requis

- Docker : Pour créer les images de conteneurs.
- Minikube : Pour créer un cluster Kubernetes local.
- kubectl : Pour interagir avec le cluster Kubernetes.
- Nginx Ingress Controller : Pour gérer les accès HTTP externes.

## Étapes de Déploiement

### 1. Démarrer Minikube

```bash
minikube start
```
Initialise et démarre le cluster Minikube local.

### 2. Activer Nginx Ingress Controller

```bash
minikube addons enable ingress
```
Active l'addon Ingress dans Minikube pour gérer le routage HTTP externe.

### 3. Configurer le Fichier Hosts

```bash
echo "$(minikube ip) myapp.local" | sudo tee -a /etc/hosts
```
Ajoute une entrée dans le fichier hosts pour mapper l'IP de Minikube à un nom de domaine local.

### 4. Créer les PersistentVolumes et PersistentVolumeClaims

```bash
kubectl apply -f backend-pv-pvc.yaml
kubectl apply -f db-pv-pvc.yaml
```
Crée les volumes persistants pour stocker les données de la base de données et les logs du backend.

### 5. Déployer les Jobs et CronJobs

```bash
kubectl apply -f volume-backup-job.yaml
kubectl apply -f volume-cleanup-cronjob.yaml
```
Déploie un job pour sauvegarder les volumes et un CronJob pour nettoyer périodiquement les volumes.

### 6. Déployer la Base de Données PostgreSQL

```bash
kubectl apply -f db-deployment.yaml
kubectl apply -f db-service.yaml
```
Déploie la base de données PostgreSQL et crée un service Kubernetes pour y accéder.

### 7. Déployer le Backend

```bash
kubectl apply -f backend-configmap.yaml
kubectl apply -f back-deployment.yaml
kubectl apply -f back-service.yaml
kubectl apply -f backend-hpa.yaml
```
Déploie l'application backend, crée un service pour l'exposer, et configure l'autoscaling horizontal.

### 8. Déployer le Frontend

```bash
kubectl apply -f frontend-configmap.yaml
kubectl apply -f front-deployment.yaml
kubectl apply -f front-service.yaml
kubectl apply -f frontend-hpa.yaml
```
Déploie l'application frontend, crée un service pour l'exposer, et configure l'autoscaling horizontal.

### 9. Configurer l'Ingress

```bash
kubectl apply -f ingress.yaml
```
Configure les règles Ingress pour diriger le trafic externe vers les services backend et frontend.

## Résumé des Composants Déployés

### PersistentVolumes et PersistentVolumeClaims
- backend-pv-pvc.yaml : Définit le volume persistant pour les logs du backend.
- db-pv-pvc.yaml : Définit le volume persistant pour les données PostgreSQL.

### Jobs et CronJobs
- volume-backup-job.yaml : Job pour sauvegarder les volumes de la base de données et des logs backend.
- volume-cleanup-cronjob.yaml : CronJob pour nettoyer périodiquement les anciens logs et sauvegardes.

### Base de Données PostgreSQL
- db-deployment.yaml : Déploie l'instance PostgreSQL.
- db-service.yaml : Expose PostgreSQL via un service Kubernetes.

### Backend
- backend-configmap.yaml : Contient les variables d'environnement pour le backend.
- back-deployment.yaml : Déploie l'application backend.
- back-service.yaml : Expose l'application backend via un service Kubernetes.
- backend-hpa.yaml : Définit l'autoscaler horizontal pour le backend.

### Frontend
- frontend-configmap.yaml : Contient les variables d'environnement pour le frontend.
- front-deployment.yaml : Déploie l'application frontend.
- front-service.yaml : Expose l'application frontend via un service Kubernetes.
- frontend-hpa.yaml : Définit l'autoscaler horizontal pour le frontend.

### Ingress
- ingress.yaml : Configure les règles Ingress pour diriger le trafic vers les services backend et frontend.

## Commandes de Gestion

### Vérifier les Pods
```bash
kubectl get pods
```
Affiche la liste et le statut de tous les pods en cours d'exécution.

### Vérifier les Services
```bash
kubectl get services
```
Affiche la liste de tous les services Kubernetes et leurs détails.

### Vérifier les Ingress
```bash
kubectl get ingress
```
Affiche les règles Ingress configurées.

### Vérifier les HPA (Horizontal Pod Autoscalers)
```bash
kubectl get hpa
```
Affiche les détails des autoscalers horizontaux configurés.

### Journaux d'un Pod
```bash
kubectl logs <pod-name>
```
Affiche les logs d'un pod spécifique.

### Accéder à un Pod
```bash
kubectl exec -it <pod-name> -- /bin/bash
```
Ouvre un shell interactif dans un pod spécifique.

### Vérifier les Jobs
```bash
kubectl get jobs
```
Affiche la liste et le statut de tous les jobs.

### Vérifier les CronJobs
```bash
kubectl get cronjobs
```
Affiche la liste et le statut de tous les CronJobs.

### Décrire un Ressource
```bash
kubectl describe <resource-type> <resource-name>
```
Fournit des informations détaillées sur une ressource spécifique (pod, service, deployment, etc.).

### Supprimer une Ressource
```bash
kubectl delete <resource-type> <resource-name>
```
Supprime une ressource spécifique du cluster.

### Mettre à Jour une Ressource
```bash
kubectl apply -f <updated-resource-file.yaml>
```
Met à jour une ressource existante avec de nouvelles configurations.

### Scaling Manuel d'un Déploiement
```bash
kubectl scale deployment <deployment-name> --replicas=<number>
```
Ajuste manuellement le nombre de réplicas pour un déploiement spécifique.

## Maintenance et Dépannage

### Vérifier l'État du Cluster Minikube
```bash
minikube status
```
Affiche l'état actuel du cluster Minikube.

### Redémarrer Minikube
```bash
minikube stop
minikube start
```
Arrête puis redémarre le cluster Minikube en cas de problèmes.

### Vérifier les Ressources du Cluster
```bash
kubectl top nodes
kubectl top pods
```
Affiche l'utilisation des ressources (CPU, mémoire) pour les nœuds et les pods.

### Vérifier les Événements du Cluster
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```
Affiche les événements récents du cluster, utile pour le dépannage.

### Nettoyer les Ressources
```bash
kubectl delete all --all
```
Supprime toutes les ressources du cluster (à utiliser avec précaution).

