# Exercice Guidé : Les Déploiements et les DaemonSets dans OpenShift

Dans cet exercice, vous allez créer un déploiement et un DaemonSet dans OpenShift, tester une stratégie de déploiement en Rolling Updates, et observer le fonctionnement des DaemonSets. Suivez les étapes ci-dessous pour mettre en pratique les concepts théoriques que nous avons abordés.

#### Objectifs de l'Exercice

- Créer un déploiement dans OpenShift.
- Appliquer une stratégie de déploiement en Rolling Updates.
- Mettre à jour l'application et observer le processus de déploiement.
- Déclencher un rollback en cas de problème.
- Créer un DaemonSet et comprendre ses spécificités.
- Observer le fonctionnement des DaemonSets sur les nœuds du cluster.

#### Prérequis

Assurez-vous d'avoir accès à un cluster OpenShift et les permissions nécessaires pour créer des déploiements et des DaemonSets. Vous devez également avoir la CLI `oc` installée sur votre machine.

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
        image: registry.access.redhat.com/ubi9/httpd-24:1-3
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

Ce fichier YAML définit un déploiement nommé `my-deployment` avec 3 réplicas d'un conteneur Httpd. La stratégie de déploiement est configurée pour utiliser Rolling Updates.

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

### Étape 3 : Mettre à Jour l'Application et Observer le Rolling Update

Pour simuler une mise à jour de l'application, nous allons changer l'image utilisée par le conteneur.
Avant cela, rendez-vous dans la console dans la section Deployment et cliquez sur `my-deployment`.

![My-deployment section](./images/my-deployment.png)

Exécutez la commande suivante pour mettre à jour l'image du conteneur :

```bash
oc set image deployment/my-deployment my-container=registry.access.redhat.com/ubi9/httpd-24:1-325
```

Vous devriez alors pouvoir observer le rollout dans la console.

### Étape 4 : Déclencher un Rollback

Si quelque chose ne va pas avec la mise à jour, vous pouvez revenir à la version précédente du déploiement :

```bash
oc rollout undo deployment/my-deployment
```

Cette commande déclenchera un rollback, et les pods seront remplacés par ceux définis dans la configuration précédente.

### Étape 5 : Vérifier le Rollback

Pour vérifier que le rollback a bien fonctionné, nous allons récupérer l'image actuellement utilisée par les pods et vérifier qu'elle correspond bien à l'ancienne version. Utilisez les commandes suivantes :

1. **Vérifiez le statut du déploiement :**

   ```bash
   oc rollout status deployment/my-deployment
   ```

2. **Listez les pods pour vérifier qu'ils sont tous en cours d'exécution :**

   ```bash
   oc get pods
   ```

3. **Récupérez l'image actuellement utilisée par le déploiement :**

   ```bash
   oc get deployment my-deployment -o jsonpath='{.spec.template.spec.containers[0].image}'
   ```

Cette commande affichera l'image actuellement utilisée par le déploiement. Vérifiez que cette image correspond à l'ancienne version, qui est `registry.access.redhat.com/ubi9/httpd-24:1-3`.

### Étape 6 : Créer un DaemonSet

Un DaemonSet garantit que chaque nœud du cluster exécute une instance d'un pod spécifique. C'est idéal pour les tâches de maintenance ou de surveillance qui doivent être présentes sur chaque nœud, comme les collecteurs de logs ou les agents de monitoring. Dans cet exemple, nous allons créer un DaemonSet pour déployer Fluentd, un collecteur de logs populaire.

Créez un fichier nommé `my-daemonset.yaml` avec le contenu suivant :

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
  labels:
    app: fluentd
spec:
  selector:
    matchLabels:
      app: fluentd
  template:
    metadata:
      labels:
        app: fluentd
    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd:v1.12.3
        resources:
          requests:
            memory: "64Mi"
            cpu: "250m"
          limits:
            memory: "128Mi"
            cpu: "500m"
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibdockercontainers
          mountPath: /var/lib/docker/containers
          readOnly: true
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibdockercontainers
        hostPath:
          path: /var/lib/docker/containers
```

Ce fichier YAML définit un DaemonSet nommé `fluentd` qui déploie un pod Fluentd sur chaque nœud du cluster.

Appliquez ce DaemonSet avec la commande suivante :

```bash
oc apply -f my-daemonset.yaml
```

### Étape 7 : Vérifier le DaemonSet

Vérifiez que le DaemonSet a été créé et que les pods sont en cours d'exécution sur chaque nœud :

```bash
oc get daemonsets
oc get pods -l app=fluentd -o wide
```

Vous devriez voir le DaemonSet `fluentd` et un pod en cours d'exécution sur chaque nœud du cluster. Pour confirmer dans la console OpenShift :

1. **Allez dans la section Workloads et cliquez sur DaemonSets.**
2. **Vérifiez que le DaemonSet `fluentd` est listé.**
3. **Cliquez sur `fluentd` pour voir les détails et vérifier que des pods sont en cours d'exécution sur chaque nœud.**

### Conclusion

En suivant ces étapes, vous avez appris à créer et gérer des déploiements et des DaemonSets dans OpenShift. Vous avez également observé comment mettre à jour une application avec une stratégie de Rolling Updates, déclencher un rollback en cas de problème, et déployer des tâches critiques sur chaque nœud à l'aide de DaemonSets. Les DaemonSets sont particulièrement utiles pour les services nécessitant une présence sur tous les nœuds, comme les collecteurs de logs, les agents de monitoring, ou les configurations réseau. Ces compétences sont essentielles pour gérer efficacement vos applications et maintenir la stabilité et la continuité des services dans un environnement OpenShift.
