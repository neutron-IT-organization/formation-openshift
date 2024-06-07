# Exercice Guidé : Exposition d'Application avec un Accès Externe

Dans cet exercice, nous allons explorer différentes méthodes pour exposer une application dans Kubernetes pour un accès externe. Nous allons pratiquer la création et la configuration de services pour utiliser les types NodePort, LoadBalancer et Ingress, et examiner comment chaque méthode permet d'accéder à une application depuis l'extérieur du cluster Kubernetes.

## Objectifs de l'Exercice

- Apprendre à exposer une application dans Kubernetes pour un accès externe en utilisant les types de service NodePort, LoadBalancer et Ingress.
- Comprendre les avantages et les limitations de chaque méthode d'exposition.
- Explorer les meilleures pratiques pour la gestion de l'accès externe aux applications dans Kubernetes.

## Instructions

### 1. Exposition avec NodePort

1. Créez un service de type NodePort pour exposer une application dans Kubernetes. Utilisez la commande `kubectl expose` avec l'option `--type=NodePort` pour créer le service.

2. Vérifiez que le service NodePort a été créé avec succès en utilisant la commande `kubectl get svc`.

3. Obtenez l'adresse IP d'un nœud dans le cluster et le port NodePort assigné au service. Essayez de vous connecter à l'application en utilisant cette adresse IP et le port NodePort.

### 2. Exposition avec LoadBalancer

1. Créez un service de type LoadBalancer pour exposer une application dans Kubernetes à l'aide d'un équilibreur de charge externe. Utilisez la commande `kubectl expose` avec l'option `--type=LoadBalancer` pour créer le service.

2. Vérifiez que le service LoadBalancer a été créé avec succès en utilisant la commande `kubectl get svc`.

3. Obtenez l'adresse IP externe attribuée par l'équilibreur de charge et essayez de vous connecter à l'application en utilisant cette adresse IP.

### 3. Exposition avec Ingress

1. Déployez un contrôleur Ingress dans le cluster Kubernetes, par exemple, Nginx Ingress Controller.

2. Créez une ressource Ingress pour router le trafic vers l'application. Utilisez les règles de routage pour spécifier les hôtes et les chemins d'URL.

3. Vérifiez que l'Ingress a été créé avec succès en utilisant la commande `kubectl get ingress`.

4. Ajoutez une entrée dans votre fichier hosts local ou configurez un DNS pour mapper le nom d'hôte spécifié dans l'Ingress à l'adresse IP du cluster Kubernetes.

5. Essayez de vous connecter à l'application en utilisant le nom d'hôte spécifié dans l'Ingress.

## Conclusion

Cet exercice vous a permis de pratiquer l'exposition d'une application dans Kubernetes pour un accès externe en utilisant les types de service NodePort, LoadBalancer et Ingress. En explorant les différentes méthodes d'exposition et en testant l'accès à l'application depuis l'extérieur du cluster, vous avez acquis une expérience pratique dans la gestion de l'accès externe aux applications dans Kubernetes.