# Exercice Guidé : Monitoring de Cluster

Dans cet exercice, vous allez explorer le processus de monitoring d'un cluster OpenShift en utilisant les outils Prometheus, Grafana et Alertmanager. Vous apprendrez à collecter des métriques, à créer des tableaux de bord personnalisés, et à configurer des alertes pour surveiller la santé et les performances du cluster.

## Objectifs de l'exercice

- Accéder à l'interface de monitoring de Prometheus et Grafana.
- Explorer les métriques disponibles et créer des requêtes personnalisées.
- Créer un tableau de bord Grafana pour surveiller les ressources du cluster.
- Configurer une règle d'alerte dans Alertmanager et vérifier son déclenchement.

## Prérequis

- Accès à un cluster OpenShift avec des identifiants valides.
- Connexion Internet et un navigateur web compatible avec l'interface de Prometheus et Grafana.

## Étape 1 : Accès à l'interface de monitoring

1. **Ouvrir la console web OpenShift**.
2. **Naviguer vers le Monitoring** :
   - Cliquez sur **Monitoring** dans la barre de navigation.

### Accès à Prometheus

1. **Accéder à Prometheus** :
   - Sélectionnez **Metrics** pour ouvrir l'interface de Prometheus.

2. **Explorer les Métriques** :
   - Utilisez l'interface pour rechercher et explorer les métriques disponibles.
   - Créez des requêtes pour afficher des métriques spécifiques.

### Accès à Grafana

1. **Accéder à Grafana** :
   - Sélectionnez **Dashboards** pour ouvrir l'interface de Grafana.

2. **Créer un Tableau de Bord** :
   - Utilisez l'interface pour créer un nouveau tableau de bord.
   - Ajoutez des panneaux pour afficher les métriques pertinentes du cluster.

## Étape 2 : Configuration d'une Règle d'Alerte

1. **Accéder à Alertmanager** :
   - Depuis la console Prometheus, cliquez sur **Alerting**.

2. **Créer une Nouvelle Règle** :
   - Définissez une règle d'alerte basée sur une condition spécifique, par exemple, une utilisation élevée de la CPU ou de la mémoire.

3. **Configurer les Destinataires** :
   - Ajoutez des destinataires pour recevoir les alertes, par exemple, une adresse e-mail ou un canal Slack.

4. **Tester la Règle d'Alerte** :
   - Simulez une condition de déclenchement de l'alerte en modifiant temporairement une métrique dans le cluster.

## Étape 3 : Vérification de l'Alerte

1. **Surveiller les Alertes** :
   - Retournez à l'interface de Prometheus et vérifiez que l'alerte est déclenchée.

2. **Vérifier les Notifications** :
   - Vérifiez que les destinataires configurés reçoivent les notifications d'alerte, par exemple, en vérifiant votre boîte e-mail ou le canal Slack.

## Conclusion

Vous avez maintenant une compréhension pratique du processus de monitoring d'un cluster OpenShift. En utilisant les outils Prometheus, Grafana et Alertmanager, vous pouvez collecter des métriques, créer des tableaux de bord personnalisés et configurer des alertes pour surveiller la santé et les performances de votre cluster. Continuez à explorer et à affiner votre configuration de monitoring pour répondre aux besoins spécifiques de vos applications et de votre infrastructure.

---

Dans la prochaine section, nous aborderons l'interaction avec la ligne de commande, y compris l'utilisation des outils `oc` et `kubectl` pour gérer vos ressources OpenShift.