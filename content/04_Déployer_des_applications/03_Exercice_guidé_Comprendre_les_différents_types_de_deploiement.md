Voici quelques exercices pratiques avec des lignes de commande pour vous familiariser avec Kubernetes :

---

## Exercice 1: Création d'un Pod

1. Utilisez la commande `kubectl run` pour créer un pod nommé "mon-pod" à partir de l'image "nginx:latest".

2. Vérifiez que le pod a été créé en utilisant la commande `kubectl get pods`.

3. Affichez les détails du pod en utilisant la commande `kubectl describe pod mon-pod`.

## Exercice 2: Déploiement d'une Application

1. Créez un fichier YAML nommé "deployment.yaml" décrivant un déploiement avec 3 répliques d'une application basée sur l'image "mon_application:latest".

2. Utilisez la commande `kubectl apply -f deployment.yaml` pour déployer l'application sur votre cluster Kubernetes.

3. Vérifiez que le déploiement a été créé en utilisant la commande `kubectl get deployment`.

4. Affichez les détails du déploiement en utilisant la commande `kubectl describe deployment mon-deploiement`.

## Exercice 3: Mise à l'échelle d'un Déploiement

1. Utilisez la commande `kubectl scale` pour mettre à l'échelle le déploiement "mon-deploiement" à 5 répliques.

2. Vérifiez que le nombre de répliques a été mis à jour en utilisant la commande `kubectl get deployment mon-deploiement`.

## Exercice 4: Exposition d'un Service

1. Créez un fichier YAML nommé "service.yaml" décrivant un service de type NodePort pour exposer le déploiement "mon-deploiement" sur le port 8080.

2. Utilisez la commande `kubectl apply -f service.yaml` pour créer le service.

3. Vérifiez que le service a été créé en utilisant la commande `kubectl get svc`.

4. Affichez les détails du service en utilisant la commande `kubectl describe svc mon-service`.

## Exercice 5: Suppression d'un Pod

1. Utilisez la commande `kubectl delete pod` pour supprimer le pod "mon-pod".

2. Vérifiez que le pod a été supprimé en utilisant la commande `kubectl get pods`.

---

Ces exercices vous permettront de pratiquer différentes opérations courantes avec Kubernetes en utilisant des lignes de commande. Si vous avez des questions ou si vous rencontrez des difficultés avec l'un des exercices, n'hésitez pas à demander de l'aide !