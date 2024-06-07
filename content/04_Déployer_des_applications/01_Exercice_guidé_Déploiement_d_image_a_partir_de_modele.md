# Exercice Guidé : Déploiement d'Image à Partir d'un Modèle

Dans cet exercice, nous allons pratiquer le déploiement d'une application à partir d'un modèle dans Kubernetes. Vous apprendrez à créer un déploiement en utilisant un fichier YAML décrivant les spécifications de l'application, puis à déployer cette application sur votre cluster Kubernetes en utilisant la commande `kubectl apply`.

## Objectifs de l'Exercice

- Apprendre à créer un fichier YAML décrivant les spécifications d'une application dans Kubernetes.
- Pratiquer le déploiement de l'application en utilisant le fichier YAML créé.
- Vérifier que l'application a été déployée avec succès sur le cluster Kubernetes.

## Instructions

### 1. Création du Fichier YAML

Commencez par créer un fichier YAML décrivant les spécifications de votre application. Assurez-vous d'inclure des informations telles que le nom de l'application, l'image du conteneur, les ports exposés, etc. Voici un exemple de structure de fichier YAML pour un déploiement :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mon-application
spec:
  replicas: 3
  selector:
    matchLabels:
      app: mon-application
  template:
    metadata:
      labels:
        app: mon-application
    spec:
      containers:
      - name: mon-conteneur
        image: mon_image:latest
        ports:
        - containerPort: 8080
```

### 2. Déploiement de l'Application

Une fois que vous avez créé votre fichier YAML, utilisez la commande `kubectl apply` pour déployer l'application sur votre cluster Kubernetes :

```bash
kubectl apply -f nom_du_fichier.yaml
```

Vérifiez que le déploiement a été créé avec succès en utilisant la commande `kubectl get deployment` :

```bash
kubectl get deployment
```

### 3. Vérification du Déploiement

Vérifiez que les pods de votre déploiement sont en cours d'exécution en utilisant la commande `kubectl get pods` :

```bash
kubectl get pods
```

Assurez-vous que les pods sont en état "Running" et qu'ils sont prêts à recevoir du trafic.

## Conclusion

Cet exercice vous a permis de pratiquer le déploiement d'une application à partir d'un modèle dans Kubernetes. En créant un fichier YAML décrivant les spécifications de l'application et en utilisant la commande `kubectl apply`, vous avez pu déployer l'application sur votre cluster Kubernetes avec succès. Le déploiement d'applications à partir de modèles est une pratique courante dans Kubernetes qui permet de standardiser et d'automatiser le processus de déploiement d'applications conteneurisées.