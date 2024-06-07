# Exercice Guidé : Exploration de la console OpenShift

Dans cet exercice, vous allez apprendre à naviguer dans la console web d'OpenShift et à effectuer des tâches courantes. Suivez les étapes ci-dessous pour vous familiariser avec l'interface utilisateur et ses fonctionnalités.

## Objectifs de l'exercice

- Accéder à la console web d'OpenShift
- Créer un projet
- Déployer une application à partir d'un template
- Surveiller les ressources du projet
- Configurer et visualiser des alertes

## Prérequis

- Accès à un cluster OpenShift avec des identifiants valides
- Connexion Internet et un navigateur web compatible

## Étape 1 : Accéder à la console web

1. Ouvrez votre navigateur web.
2. Entrez l'URL de la console web d'OpenShift fournie par votre administrateur.
3. Connectez-vous avec vos identifiants OpenShift.

## Étape 2 : Créer un projet

1. **Naviguer vers les Projets** :
   - Cliquez sur **Projets** dans la barre de navigation en haut de la page.
   - Cliquez sur **Créer un projet**.

2. **Remplir le formulaire de création de projet** :
   - Nom du projet : `exercice-exploration`
   - Afficher le nom : `Exploration de la Console`
   - Description : `Projet pour l'exercice guidé d'exploration de la console OpenShift`
   - Cliquez sur **Créer**.

## Étape 3 : Déployer une application

1. **Accéder au Catalogue** :
   - Cliquez sur **Catalogues** dans la barre de navigation.

2. **Sélectionner une application** :
   - Recherchez et sélectionnez un template d'application, par exemple `Node.js + MongoDB (Ephemeral)`.

3. **Configurer le déploiement** :
   - Cliquez sur **Suivant** et remplissez les paramètres nécessaires pour l'application.
   - Utilisez les valeurs par défaut pour cet exercice ou personnalisez-les selon vos besoins.
   - Cliquez sur **Créer** pour lancer le déploiement.

4. **Vérifier le déploiement** :
   - Accédez à l'onglet **Applications** dans le projet `exercice-exploration`.
   - Vérifiez que les pods de l'application sont en cours d'exécution.

## Étape 4 : Surveiller les ressources du projet

1. **Accéder à l'onglet Monitoring** :
   - Dans le projet `exercice-exploration`, cliquez sur l'onglet **Monitoring**.

2. **Visualiser les métriques** :
   - Observez les graphiques montrant l'utilisation de la CPU, de la mémoire, et d'autres métriques.
   - Prenez note de l'activité de votre application déployée.

## Étape 5 : Configurer des alertes

1. **Accéder aux Alertes** :
   - Dans l'onglet **Monitoring**, cliquez sur **Configurer des alertes**.

2. **Créer une nouvelle alerte** :
   - Cliquez sur **Créer une alerte**.
   - Configurez une alerte pour surveiller l'utilisation de la CPU :
     - Nom de l'alerte : `Alerte Utilisation CPU`
     - Expression : `sum(rate(container_cpu_usage_seconds_total{namespace="exercice-exploration"}[5m])) by (pod)`
     - Conditions : Déclenchez une alerte si l'utilisation de la CPU dépasse 80%.
     - Actions : Configurez les notifications par email ou autre méthode disponible.

3. **Sauvegarder et activer l'alerte** :
   - Cliquez sur **Sauvegarder**.
   - Vérifiez que l'alerte est activée et surveillez son déclenchement en fonction de l'activité de votre application.

## Conclusion

Vous avez maintenant une bonne compréhension de la console web d'OpenShift. Vous savez comment créer des projets, déployer des applications, surveiller les ressources et configurer des alertes. Continuez à explorer les autres fonctionnalités de la console pour renforcer vos compétences. Si vous avez des questions ou des difficultés, consultez la documentation officielle d'OpenShift ou demandez de l'aide à votre administrateur.

---

Dans la prochaine section, nous aborderons l'architecture d'OpenShift et Kubernetes, en explorant leurs composants clés et leur interaction.