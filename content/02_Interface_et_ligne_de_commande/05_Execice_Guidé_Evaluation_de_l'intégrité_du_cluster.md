# Exercice guidé : Évaluation de l'intégrité du Cluster

Dans cet exercice, nous allons pratiquer l'évaluation de l'intégrité d'un cluster Kubernetes ou OpenShift à l'aide de la commande `kubectl` et d'autres outils de surveillance. Vous allez apprendre à vérifier l'état des ressources clés telles que les pods, les services et les nœuds, ainsi qu'à identifier les problèmes potentiels et à prendre des mesures correctives.

## Objectifs de l'exercice

- Utiliser la commande `kubectl` pour obtenir des informations sur l'état des ressources du cluster.
- Surveiller les événements récents du cluster pour détecter les problèmes potentiels.
- Identifier les ressources en échec et prendre des mesures correctives pour restaurer l'intégrité du cluster.

## Instructions

### 1. Affichage de l'état des Pods

Utilisez la commande `kubectl get pods --all-namespaces` pour afficher l'état des pods dans tous les namespaces du cluster.

```bash
kubectl get pods --all-namespaces
```

Notez les pods en état "Running", "Pending" ou "Error" et examinez les raisons des éventuelles erreurs.

### 2. Affichage de l'état des Nœuds

Utilisez la commande `kubectl get nodes` pour afficher l'état des nœuds du cluster.

```bash
kubectl get nodes
```

Vérifiez que tous les nœuds sont en ligne et prêts à recevoir des charges de travail.

### 3. Surveillance des Événements du Cluster

Utilisez la commande `kubectl get events --sort-by='.metadata.creationTimestamp'` pour afficher les événements récents du cluster.

```bash
kubectl get events --sort-by='.metadata.creationTimestamp'
```

Recherchez les événements liés à des échecs de pods, des erreurs de déploiement ou d'autres problèmes potentiels.

### 4. Identification et Résolution des Problèmes

Si vous identifiez des problèmes potentiels lors de l'examen de l'état du cluster et des événements, prenez des mesures correctives pour restaurer l'intégrité du cluster. Cela peut inclure la redémarrage de pods en échec, la modification de la configuration des déploiements ou d'autres actions nécessaires pour résoudre les problèmes rencontrés.

## Conclusion

Cet exercice vous a permis de pratiquer l'évaluation de l'intégrité d'un cluster Kubernetes ou OpenShift en utilisant la commande `kubectl` et d'autres outils de surveillance. En surveillant régulièrement l'état des ressources du cluster et en identifiant les problèmes potentiels, vous pouvez prendre des mesures proactives pour maintenir un environnement stable et opérationnel.