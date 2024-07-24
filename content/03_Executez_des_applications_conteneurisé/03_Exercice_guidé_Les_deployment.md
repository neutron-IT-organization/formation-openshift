# Exercice Guidé : Les déploiements dans OpenShift

Dans cet exercice, vous allez créer un déploiement dans OpenShift et tester une stratégie de déploiement en Rolling Updates. Suivez les étapes ci-dessous pour mettre en pratique les concepts théoriques que nous avons abordés.

#### Objectifs de l'Exercice

- Créer un déploiement dans OpenShift.
- Appliquer une stratégie de déploiement en Rolling Updates.
- Mettre à jour l'application et observer le processus de déploiement.
- Déclencher un rollback en cas de problème.

#### Prérequis

Assurez-vous d'avoir accès à un cluster OpenShift et les permissions nécessaires pour créer des déploiements. Vous devez également avoir la CLI `oc` installée sur votre machine.

### Étape 1 : Créer un Déploiement

Créez un fichier nommé `my-deployment.yaml` avec le contenu suivant :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
  labels:
    app: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: registry.access.redhat.com/ubi9/httpd-24:latest
        ports:
        - containerPort: 80
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
        env:
        - name: ENV_VAR
          value: "value"
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
```

Ce fichier YAML définit un déploiement nommé `my-deployment` avec 3 réplicas d'un conteneur Nginx. La stratégie de déploiement est configurée pour utiliser Rolling Updates.

Appliquez ce déploiement avec la commande suivante :

```bash
oc apply -f my-deployment.yaml
```

### Étape 2 : Vérifier le Déploiement

Vérifiez que le déploiement a été créé et que les pods sont en cours d'exécution :

```bash
oc get deployments
oc get pods
```

Vous devriez voir le déploiement `my-deployment` et trois pods en cours d'exécution.

### Étape 3 : Mettre à Jour l'Application

Pour simuler une mise à jour de l'application, nous allons changer l'image utilisée par le conteneur. Exécutez la commande suivante pour mettre à jour l'image du conteneur :

```bash
oc set image deployment/my-deployment my-container=registry.access.redhat.com/ubi9/httpd-24:1-325
```

### Étape 4 : Observer le Rolling Update

Observez le processus de mise à jour en utilisant la commande suivante :

```bash
oc rollout status deployment/my-deployment
```

Cette commande vous montrera l'état du déploiement en cours. Les pods devraient être mis à jour progressivement, avec un pod supplémentaire créé et un pod ancien supprimé à chaque étape, conformément aux paramètres `maxSurge` et `maxUnavailable`.

### Étape 5 : Déclencher un Rollback

Si quelque chose ne va pas avec la mise à jour, vous pouvez revenir à la version précédente du déploiement :

```bash
oc rollout undo deployment/my-deployment
```

Cette commande déclenchera un rollback, et les pods seront remplacés par ceux définis dans la configuration précédente.

### Étape 6 : Vérifier la Disponibilité de l'Application

Pendant et après la mise à jour, vérifiez que l'application reste disponible. Vous pouvez obtenir l'adresse IP des pods et vérifier l'accès au serveur Nginx avec la commande suivante :

```bash
oc get pods -o wide
```

Utilisez l'adresse IP d'un pod pour tester l'accès via un navigateur ou un outil de ligne de commande comme `curl`.

### Conclusion

Félicitations ! Vous avez créé un déploiement dans OpenShift, appliqué une stratégie de déploiement en Rolling Updates, mis à jour l'application, et observé le processus de déploiement. Vous avez également appris à déclencher un rollback en cas de problème. Ces compétences sont essentielles pour gérer efficacement des applications conteneurisées en production.
