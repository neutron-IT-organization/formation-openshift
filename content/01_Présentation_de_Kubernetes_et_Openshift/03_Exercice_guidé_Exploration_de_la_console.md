# Exercice Guidé : Exploration de la console OpenShift

Dans cet exercice, vous allez apprendre à naviguer dans la console web d'OpenShift et à effectuer des tâches courantes. Suivez les étapes ci-dessous pour vous familiariser avec l'interface utilisateur et ses fonctionnalités.

## Objectifs de l'exercice

- Accéder à la console web d'OpenShift
- Créer un projet
- Déployer une application à partir d'un template
- Surveiller les ressources du projet
- Configurer et visualiser des alertes

## Étape 1 : Accéder à la console web

1. Ouvrez votre navigateur web.
2. Entrez l'URL de la console web d'OpenShift ci-dessous :
```shell
https://console-openshift-console.apps.neutron-sno-office.intraneutron.fr/
```
3. Cliquez sur `Neutron Guest Identity Management`
4. Connectez-vous avec vos identifiants OpenShift.

## Étape 2 : Créer un projet et déployer une application

Pour utiliser la perspective Developer de la console Web et créer votre premier projet :

1. Dans la vue developer, cliquez sur votre Project en haut à gauche puis sur  "Create a new project" pour ouvrir l'assistant Create Project.

![Create Project](./images/create_project.png){: style="height:300px"}

Créez un projet nommé "console-exploration-YOURCITY" à l'aide de cet assistant et ajoutez une brève description du projet.

2. Cliquez sur "Create" pour finaliser la création du projet.

![Create Project](./images/assistant_create_project.png){: style="height:300px"}


3. Ensuite, cliquez sur "+Add" pour créer une application.

4. Pour déployer un exemple d'application dans le projet :

   - Cliquez dans "Create applications using samples" sur le lien "Basic Quarkus".

   ![Basic quarkus](./images/basic_quarkus.png){: style="height:300px"}

   - Examinez les valeurs par défaut de l'exemple d'application, puis sélectionnez "Create" en bas de la page.

   ![Create application](./images/create_application.png){: style="height:300px"}


5. Une fois le déploiement effectué, rendez vous dans à la page "Topology" qui affiche maintenant le déploiement de l'application "code-with-quarkus".

6. Pour afficher les détails de ce déploiement :

   - Sélectionnez l'icône correspondant à "code-with-quarkus" dans le panneau "Topology" pour ouvrir les détails du déploiement.

   ![Topology view](./images/topology_view.png)

   - Dans la partie "Route" cliquez sur la location pour accéder au deploiement de "code-with-quarkus".

   ![Get route](./images/get_route.png)

   ![Result](./images/result_quarkus.png)

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
