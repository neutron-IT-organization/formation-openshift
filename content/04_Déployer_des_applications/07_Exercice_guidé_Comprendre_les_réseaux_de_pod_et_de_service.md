# Exercice Guidé : Comprendre le Réseau de Pod et de Service

Dans cet exercice, nous allons explorer le réseau de pod et de service dans Kubernetes. Nous allons pratiquer la création et la configuration de services pour exposer des ensembles de pods et examiner comment les pods communiquent entre eux à l'intérieur d'un cluster Kubernetes.

## Objectifs de l'Exercice

- Apprendre à créer et à configurer des services Kubernetes pour exposer des ensembles de pods.
- Comprendre comment les services facilitent la communication entre les différents composants d'une application dans un cluster Kubernetes.
- Explorer les différents types de services et leurs cas d'utilisation.

## Instructions

### 1. Création d'un Service ClusterIP

1. Utilisez la commande `kubectl create deployment` pour créer un déploiement avec quelques pods d'une application de test, par exemple, nginx.
   
2. Créez un service de type ClusterIP pour exposer les pods du déploiement. Utilisez la commande `kubectl expose` pour créer le service.

3. Vérifiez que le service a été créé avec succès en utilisant la commande `kubectl get svc`.

4. Notez l'adresse IP interne attribuée au service et essayez de vous connecter aux pods à l'aide de cette adresse IP.

### 2. Création d'un Service NodePort

1. Créez un service de type NodePort pour exposer les pods du déploiement sur un port statique sur chaque nœud du cluster. Utilisez la commande `kubectl expose` pour créer le service avec l'option `--type=NodePort`.

2. Vérifiez que le service NodePort a été créé avec succès en utilisant la commande `kubectl get svc`.

3. Obtenez l'adresse IP d'un nœud dans le cluster et le port NodePort assigné au service. Essayez de vous connecter aux pods à l'aide de cette adresse IP et du port NodePort.

### 3. Communication entre Pods

1. Utilisez la commande `kubectl get pods -o wide` pour afficher les adresses IP des pods dans le cluster.

2. Choisissez deux pods différents et utilisez la commande `kubectl exec` pour ouvrir un terminal à l'intérieur de chaque pod.

3. À l'intérieur de chaque pod, essayez de vous connecter à l'autre pod en utilisant son adresse IP interne. Vérifiez que la communication entre les pods fonctionne correctement.

## Conclusion

Cet exercice vous a permis de pratiquer la création et la configuration de services dans Kubernetes pour exposer des ensembles de pods et de comprendre comment les pods communiquent entre eux à l'intérieur d'un cluster Kubernetes. En utilisant les différents types de services et en explorant la communication entre les pods, vous avez acquis une expérience pratique dans la gestion du réseau de pod et de service dans Kubernetes.