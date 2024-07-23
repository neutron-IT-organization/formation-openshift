# Exercice Guidé : Conteneur Linux sur Kubernetes

Dans cet exercice, nous allons pratiquer le déploiement et la gestion d'un conteneur Linux sur un cluster Kubernetes. Vous apprendrez à créer un pod Kubernetes pour exécuter un conteneur Linux, à surveiller son état et à effectuer des opérations de dépannage en cas de problème.

## Objectifs de l'Exercice

- Créer un pod Kubernetes pour exécuter un conteneur Linux.
- Vérifier l'état du pod pour s'assurer qu'il s'exécute correctement.
- Effectuer des opérations de dépannage en cas de problème avec le pod ou le conteneur.

## Instructions

### 1. Création du Pod Kubernetes

Utilisez un manifeste YAML pour définir un pod Kubernetes qui exécute un conteneur Linux. Voici un exemple de manifeste :

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mon-pod
spec:
  containers:
  - name: conteneur-linux
    image: <votre_image_conteneur_linux>
```

Remplacez `<votre_image_conteneur_linux>` par le nom de l'image de votre conteneur Linux.

### 2. Déploiement du Pod

Utilisez la commande `kubectl apply` pour déployer le pod sur votre cluster Kubernetes :

```bash
kubectl apply -f nom-du-fichier-manifeste.yaml
```

### 3. Vérification de l'État du Pod

Utilisez la commande `kubectl get pods` pour vérifier l'état du pod et vous assurer qu'il est en cours d'exécution :

```bash
kubectl get pods
```

Assurez-vous que l'état du pod est "Running" et qu'il n'y a pas d'erreurs signalées.

### 4. Exécution de Commandes dans le Conteneur

Utilisez la commande `kubectl exec` pour exécuter des commandes à l'intérieur du conteneur Linux :

```bash
kubectl exec -it mon-pod -- commande-a-executer
```

Remplacez `commande-a-executer` par la commande que vous souhaitez exécuter à l'intérieur du conteneur.

### 5. Dépannage en Cas de Problème

Si vous rencontrez des problèmes avec le pod ou le conteneur, utilisez les commandes `kubectl describe` et `kubectl logs` pour obtenir des informations détaillées sur l'état du pod et les éventuelles erreurs rencontrées :

```bash
kubectl describe pod mon-pod
kubectl logs mon-pod
```

## Conclusion

Cet exercice vous a permis de pratiquer le déploiement et la gestion d'un conteneur Linux sur un cluster Kubernetes. En créant un pod Kubernetes, en vérifiant son état et en effectuant des opérations de dépannage, vous avez acquis une expérience pratique précieuse dans l'exécution d'applications conteneurisées dans un environnement Kubernetes.

---

Cet exercice devrait vous fournir une expérience pratique dans le déploiement et la gestion de conteneurs Linux sur Kubernetes. Si vous avez des questions supplémentaires ou si vous rencontrez des difficultés lors de cet exercice, n'hésitez pas à demander de l'aide !