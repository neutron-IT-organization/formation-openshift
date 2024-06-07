# Interagir avec la Ligne de Commande

L'interface en ligne de commande (CLI) est un outil fondamental pour interagir avec un cluster OpenShift. En utilisant les commandes `oc` (pour OpenShift) et `kubectl` (pour Kubernetes), vous pouvez gérer efficacement les ressources du cluster, effectuer des opérations courantes et automatiser des tâches administratives.

## Objectifs de la Section

Cette section vise à vous familiariser avec les fonctionnalités de base de la CLI OpenShift et Kubernetes et à vous apprendre à les utiliser pour interagir avec votre cluster. Les principaux objectifs sont :

- Comprendre les commandes essentielles de `oc` et `kubectl`.
- Apprendre à manipuler les ressources du cluster via la ligne de commande.
- Effectuer des opérations telles que la création, la mise à jour et la suppression de ressources.

## Prérequis

Avant de commencer, assurez-vous d'avoir les éléments suivants :

- Accès à un terminal avec les outils de ligne de commande `oc` et `kubectl` installés et configurés pour se connecter à votre cluster OpenShift.
- Connaissances de base sur la structure des ressources Kubernetes/OpenShift, telles que les pods, les déploiements et les services.

## Principales Commandes

### 1. `oc`

La CLI OpenShift (`oc`) offre une interface intuitive pour interagir avec un cluster OpenShift. Voici quelques-unes des commandes les plus couramment utilisées :

- `oc login`: Cette commande permet de se connecter à un cluster OpenShift en spécifiant l'URL du cluster, le nom d'utilisateur et le mot de passe.
- `oc project`: Elle permet de changer de projet (namespace) actif dans lequel vous travaillez.
- `oc get <resource>`: Affiche une liste des ressources du cluster, telles que les pods, les services et les déploiements.
- `oc describe <resource> <name>`: Affiche des détails spécifiques sur une ressource donnée, tels que son état, ses propriétés et ses annotations.
- `oc create -f <file>`: Crée une ressource en utilisant une définition de ressource YAML fournie dans un fichier.
- `oc apply -f <file>`: Applique les changements définis dans un fichier YAML à une ressource existante.
- `oc edit <resource> <name>`: Ouvre un éditeur de texte pour modifier la définition d'une ressource donnée directement dans le fichier YAML.
- `oc delete <resource> <name>`: Supprime une ressource spécifique du cluster.

### 2. `kubectl`

`kubectl` est l'outil de ligne de commande standard pour interagir avec les clusters Kubernetes. Bien qu'il soit principalement utilisé pour les clusters Kubernetes, il peut également être utilisé avec OpenShift. Voici quelques commandes couramment utilisées :

- `kubectl get <resource>`: Similaire à `oc get`, cette commande affiche une liste des ressources du cluster Kubernetes.
- `kubectl describe <resource> <name>`: Affiche des informations détaillées sur une ressource spécifique dans le cluster Kubernetes.
- `kubectl create -f <file>`: Crée une ressource en utilisant une définition YAML fournie dans un fichier.
- `kubectl apply -f <file>`: Applique les changements définis dans un fichier YAML à une ressource existante.
- `kubectl edit <resource> <name>`: Ouvre un éditeur de texte pour modifier la définition d'une ressource donnée directement dans le fichier YAML.
- `kubectl delete <resource> <name>`: Supprime une ressource spécifique du cluster Kubernetes.

## Exemples d'Utilisation

### Création d'une Nouvelle Application

Pour créer une nouvelle application sur OpenShift, vous pouvez utiliser la commande suivante :

```bash
oc new-app --docker-image=<image_name>
```

Cette commande crée automatiquement tous les objets nécessaires, y compris les déploiements, les services et les routes, pour déployer l'application.

### Vérification de l'État des Pods

Pour vérifier l'état des pods dans un namespace spécifique, vous pouvez utiliser la commande suivante :

```bash
oc get pods -n <namespace>
```

Cela affichera une liste des pods en cours d'exécution dans le namespace spécifié, ainsi que leur état actuel.

### Mise à Jour d'une Application Déployée

Pour mettre à jour une application déployée avec une nouvelle version de l'image, utilisez la commande suivante :

```bash
oc set image deployment/<deployment_name> <container_name>=<new_image_name>
```

Cela mettra à jour le déploiement spécifié avec la nouvelle image Docker.

### Suppression d'une Application

Pour supprimer une application et ses ressources associées, utilisez la commande suivante :

```bash
oc delete all -l app=<app_name>
```

Cela supprimera tous les objets Kubernetes associés à l'application spécifiée, y compris les déploiements, les services et les routes.

## Conclusion

La ligne de commande est un outil puissant pour gérer et manipuler des ressources sur un cluster OpenShift. En apprenant les commandes de base et en pratiquant régulièrement, vous serez en mesure de travailler de manière efficace avec OpenShift et Kubernetes. Dans les prochaines sections, nous explorerons des scénarios plus avancés et des techniques avancées pour tirer le meilleur parti de votre cluster OpenShift.

---

N'hésitez pas à pratiquer ces commandes dans votre propre environnement pour renforcer votre compréhension et votre familiarité avec l'outil en ligne de commande. Si vous avez des questions ou rencontrez des problèmes, n'hésitez pas à demander de l'aide !