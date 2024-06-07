# Exploration de la console OpenShift

Dans cette section, nous allons explorer la console web d'OpenShift. La console web offre une interface graphique intuitive pour gérer les ressources de votre cluster, déployer des applications, surveiller les performances et configurer les paramètres.

## Accès à la console web

Pour accéder à la console web d'OpenShift, ouvrez un navigateur web et entrez l'URL fournie par votre administrateur système. Vous devrez vous authentifier avec vos identifiants OpenShift. Une fois connecté, vous verrez le tableau de bord principal.

## Tableau de bord principal

Le tableau de bord principal vous offre une vue d'ensemble de votre cluster, incluant les projets, les applications, les statistiques de performance et les événements récents. Voici les principaux éléments que vous y trouverez :

### 1. **Barre de navigation**

La barre de navigation en haut de la page permet d'accéder rapidement aux différentes sections de la console :
- **Accueil** : Retour au tableau de bord principal.
- **Projets** : Liste des projets disponibles.
- **Catalogues** : Accès aux catalogues de services et d'applications.
- **Monitorage** : Surveillance des ressources et des métriques.
- **Administration** : Gestion des utilisateurs, des rôles et des paramètres globaux.

### 2. **Vue d'ensemble du cluster**

La vue d'ensemble du cluster fournit des informations générales sur l'état du cluster, telles que :
- **Utilisation des ressources** : CPU, mémoire, stockage.
- **État des nodes** : Nombre de nodes disponibles, en ligne, hors ligne.
- **Pods** : Nombre total de pods, répartis par état (Running, Pending, Failed).

### 3. **Liste des projets**

La liste des projets affiche tous les projets auxquels vous avez accès. Chaque projet regroupe un ensemble de ressources liées (pods, services, routes, etc.). En sélectionnant un projet, vous accédez à ses détails spécifiques.

## Détails d'un projet

En cliquant sur un projet dans la liste des projets, vous accédez à sa vue détaillée. Cette vue fournit des informations spécifiques sur les ressources et les configurations du projet.

### 1. **Vue d'ensemble du projet**

La vue d'ensemble du projet inclut :
- **Résumé des ressources** : Nombre de pods, services, routes, builds, etc.
- **Dernières activités** : Journal des événements récents dans le projet.
- **Utilisation des ressources** : Graphiques d'utilisation de la CPU, de la mémoire et du stockage.

### 2. **Applications**

Sous l'onglet Applications, vous trouverez une liste des applications déployées dans le projet. Chaque application peut inclure plusieurs composants, tels que des déploiements, des services et des routes.

- **Déploiements** : Liste des déploiements et de leurs états actuels.
- **Services** : Points d'accès réseau pour les applications.
- **Routes** : Expositions des applications au trafic externe.

### 3. **Workloads**

L'onglet Workloads affiche les ressources de calcul dans le projet :
- **Pods** : Liste des pods en cours d'exécution et leurs détails (logs, métriques, événements).
- **ReplicaSets** : Groupes de pods identiques pour la scalabilité.
- **Jobs** : Exécutions de tâches ponctuelles ou périodiques.

### 4. **Builds**

L'onglet Builds montre l'état des processus de construction des images de conteneurs :
- **BuildConfigs** : Définitions des processus de build.
- **Builds** : Instances de builds en cours ou terminées.

### 5. **Networking**

L'onglet Networking permet de gérer les ressources réseau du projet :
- **Services** : Liste des services réseau.
- **Routes** : Gestion des routes HTTP(S).
- **Ingress** : Points d'entrée pour le trafic externe.

### 6. **Storage**

L'onglet Storage affiche les volumes de stockage persistants utilisés par le projet :
- **Persistent Volume Claims (PVC)** : Demandes de volumes de stockage.
- **Persistent Volumes (PV)** : Volumes de stockage alloués.

### 7. **Monitoring**

L'onglet Monitoring fournit des graphiques et des alertes sur les performances et l'état des ressources du projet :
- **Métriques** : Surveillance en temps réel de la CPU, de la mémoire, des requêtes réseau, etc.
- **Alertes** : Notifications sur les événements importants ou les problèmes détectés.

## Utilisation de la console web

### 1. **Créer un projet**

Pour créer un nouveau projet :
1. Cliquez sur **Projets** dans la barre de navigation.
2. Cliquez sur **Créer un projet**.
3. Remplissez le formulaire avec le nom et la description du projet.
4. Cliquez sur **Créer**.

### 2. **Déployer une application**

Pour déployer une nouvelle application :
1. Cliquez sur **Catalogues** dans la barre de navigation.
2. Sélectionnez un template ou un opérateur de la liste.
3. Suivez les instructions pour configurer et déployer l'application.

### 3. **Surveiller les ressources**

Pour surveiller les ressources de votre projet :
1. Cliquez sur le projet souhaité dans la liste des projets.
2. Naviguez vers l'onglet **Monitoring**.
3. Visualisez les graphiques et configurez des alertes si nécessaire.

## Conclusion

La console web d'OpenShift est un outil puissant et intuitif pour gérer vos projets, déployer des applications et surveiller l'état de votre cluster. Familiarisez-vous avec ses fonctionnalités pour tirer le meilleur parti de votre environnement OpenShift. Dans la prochaine section, nous réaliserons un exercice guidé pour explorer la console en détail et effectuer des tâches courantes.
