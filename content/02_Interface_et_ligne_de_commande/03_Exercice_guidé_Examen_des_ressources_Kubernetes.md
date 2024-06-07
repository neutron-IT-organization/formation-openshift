# Exercice guidé : Examen des Ressources Kubernetes

Dans cet exercice, nous allons pratiquer l'examen des ressources Kubernetes à l'aide de la commande `kubectl`. Vous allez apprendre à afficher des informations détaillées sur différentes ressources, telles que les pods, les services et les déploiements, et à interpréter ces informations pour mieux comprendre l'état et la configuration de votre cluster.

## Objectifs de l'exercice

- Utiliser la commande `kubectl` pour afficher des informations sur les différentes ressources Kubernetes.
- Pratiquer l'examen des ressources telles que les pods, les services et les déploiements.
- Interpréter les informations affichées pour comprendre l'état et la configuration du cluster.

## Instructions

### 1. Affichage des Pods

Utilisez la commande `kubectl get pods` pour afficher une liste des pods dans le cluster.

```bash
kubectl get pods
```

Observez les noms des pods, leur état actuel (Running, Pending, etc.) et d'autres détails pertinents.

### 2. Affichage des Services

Utilisez la commande `kubectl get services` pour afficher une liste des services disponibles dans le cluster.

```bash
kubectl get services
```

Notez les adresses IP et les ports des services, ainsi que leur type (ClusterIP, NodePort, etc.).

### 3. Affichage des Déploiements

Utilisez la commande `kubectl get deployments` pour afficher une liste des déploiements actifs dans le cluster.

```bash
kubectl get deployments
```

Observez le nombre de répliques, l'état du déploiement et d'autres détails pertinents.

### 4. Examen d'un Pod Spécifique

Choisissez un des pods affichés à l'étape 1 et utilisez la commande `kubectl describe pod <pod_name>` pour afficher des informations détaillées sur ce pod.

```bash
kubectl describe pod <pod_name>
```

Examinez les sections telles que les événements, les volumes montés, les conteneurs, etc., pour comprendre l'état et la configuration du pod.

### 5. Examen d'un Service Spécifique

Choisissez un des services affichés à l'étape 2 et utilisez la commande `kubectl describe service <service_name>` pour afficher des informations détaillées sur ce service.

```bash
kubectl describe service <service_name>
```

Observez les adresses IP, les ports, les endpoints et d'autres détails liés au service.

### 6. Examen d'un Déploiement Spécifique

Choisissez un des déploiements affichés à l'étape 3 et utilisez la commande `kubectl describe deployment <deployment_name>` pour afficher des informations détaillées sur ce déploiement.

```bash
kubectl describe deployment <deployment_name>
```

Examinez les sections telles que la stratégie de déploiement, les répliques, les événements, etc., pour comprendre l'état et la configuration du déploiement.

## Conclusion

Cet exercice vous a permis de pratiquer l'examen des ressources Kubernetes à l'aide de la commande `kubectl`. En affichant des informations détaillées sur les pods, les services et les déploiements, vous avez pu mieux comprendre l'état et la configuration de votre cluster. Cette compétence est essentielle pour gérer efficacement un environnement Kubernetes et OpenShift.

---