# Exercice Guidé : Mise à l'Échelle dans Kubernetes

Dans cet exercice, nous allons pratiquer la mise à l'échelle des applications dans Kubernetes en utilisant à la fois des méthodes manuelles et automatiques.

## Objectifs de l'Exercice

- Apprendre à mettre à l'échelle manuellement un déploiement dans Kubernetes.
- Explorer la mise à l'échelle automatique basée sur les ressources et les métriques personnalisées.
- Comprendre comment définir des seuils pour déclencher la mise à l'échelle automatique.

## Instructions

### 1. Mise à l'Échelle Manuelle

1. Utilisez la commande `kubectl get deployments` pour lister les déploiements disponibles sur votre cluster Kubernetes.

2. Choisissez un déploiement existant et utilisez la commande `kubectl scale` pour mettre à l'échelle le nombre de répliques. Par exemple, pour mettre à l'échelle un déploiement nommé "mon-deploiement" à 5 répliques, utilisez la commande suivante :

```bash
kubectl scale deployment mon-deploiement --replicas=5
```

3. Vérifiez que le déploiement a été mis à l'échelle avec succès en utilisant la commande `kubectl get deployment mon-deploiement`.

### 2. Mise à l'Échelle Automatique

#### Mise à l'Échelle Basée sur les Ressources

1. Examinez les spécifications de ressources d'un déploiement existant en utilisant la commande `kubectl describe deployment mon-deploiement`.

2. Modifiez les spécifications de ressources pour inclure des seuils d'utilisation CPU et/ou mémoire dans le fichier YAML du déploiement.

3. Observez le comportement du déploiement lorsque l'utilisation des ressources atteint ou dépasse les seuils définis.

#### Mise à l'Échelle Basée sur les Métriques Personnalisées

1. Définissez une métrique personnalisée pour surveiller une caractéristique spécifique de votre application, telle que le nombre de requêtes par seconde.

2. Utilisez un outil de surveillance tel que Prometheus pour collecter et visualiser les métriques personnalisées de votre application.

3. Configurez un système d'alerte pour déclencher automatiquement la mise à l'échelle lorsque la métrique personnalisée dépasse un seuil défini.

## Conclusion

Cet exercice vous a permis de pratiquer la mise à l'échelle des applications dans Kubernetes en utilisant à la fois des méthodes manuelles et automatiques. En mettant à l'échelle les déploiements manuellement et en explorant la mise à l'échelle automatique basée sur les ressources et les métriques personnalisées, vous avez acquis une expérience pratique dans la gestion de la capacité des applications dans un environnement Kubernetes.