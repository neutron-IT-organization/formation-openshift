# Exercice guidé : Interagir avec la Ligne de Commande

Dans cet exercice guidé, vous allez mettre en pratique les connaissances acquises sur l'utilisation de la ligne de commande pour interagir avec un cluster OpenShift. Vous allez effectuer plusieurs tâches courantes, telles que la création, la mise à jour et la suppression de ressources, ainsi que l'inspection de l'état du cluster.

## Objectifs de l'exercice

- Utiliser les commandes de base de `oc` pour effectuer des opérations sur les ressources du cluster.
- Créer, mettre à jour et supprimer des ressources telles que des déploiements et des services.
- Vérifier l'état des pods et des services pour assurer le bon fonctionnement du cluster.

## Instructions

### 1. Connexion au Cluster

Commencez par vous connecter à votre cluster OpenShift en utilisant la commande `oc login` avec les informations d'identification appropriées.

```bash
oc login <cluster_url> -u <username> -p <password>
```

Assurez-vous d'être connecté au bon projet (namespace) où vous souhaitez effectuer les opérations.

### 2. Création d'une Nouvelle Application

Utilisez la commande `oc new-app` pour créer une nouvelle application à partir d'une image Docker. Remplacez `<image_name>` par le nom de l'image Docker que vous souhaitez utiliser.

```bash
oc new-app --docker-image=<image_name>
```

Vérifiez que l'application a été déployée avec succès en vérifiant l'état des pods.

### 3. Mise à Jour de l'Application Déployée

Mettez à jour l'application déployée avec une nouvelle version de l'image en utilisant la commande `oc set image`. Remplacez `<deployment_name>` par le nom du déploiement à mettre à jour et `<new_image_name>` par le nom de la nouvelle image Docker.

```bash
oc set image deployment/<deployment_name> <container_name>=<new_image_name>
```

Assurez-vous que la mise à jour a été appliquée avec succès en vérifiant l'état des pods.

### 4. Suppression de l'Application

Supprimez l'application et ses ressources associées en utilisant la commande `oc delete`. Remplacez `<app_name>` par le nom de l'application que vous souhaitez supprimer.

```bash
oc delete all -l app=<app_name>
```

Vérifiez que toutes les ressources de l'application ont été supprimées avec succès en vérifiant l'état des déploiements, des services, et des pods.

## Conclusion

Dans cet exercice guidé, vous avez utilisé la ligne de commande `oc` pour interagir avec un cluster OpenShift. Vous avez appris à créer, mettre à jour et supprimer des ressources, ainsi qu'à vérifier l'état du cluster. Cette expérience pratique vous a permis de consolider vos connaissances et de devenir plus à l'aise avec l'utilisation de la ligne de commande dans un environnement OpenShift.

---

Cet exercice devrait vous aider à renforcer vos compétences pratiques dans l'utilisation de la ligne de commande pour gérer un cluster OpenShift. Si vous avez des questions ou si vous rencontrez des problèmes lors de l'exécution de cet exercice, n'hésitez pas à demander de l'aide !