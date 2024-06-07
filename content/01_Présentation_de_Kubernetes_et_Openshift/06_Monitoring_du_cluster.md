# Monitoring du Cluster OpenShift

La surveillance (monitoring) est un aspect essentiel pour garantir la disponibilité, la performance et la santé des applications déployées sur un cluster OpenShift. Cette section couvre les concepts et outils de monitoring fournis par OpenShift et Kubernetes, ainsi que les pratiques recommandées pour surveiller un cluster.

## Objectifs

- Comprendre les concepts de base du monitoring dans Kubernetes et OpenShift.
- Explorer les outils de monitoring intégrés dans OpenShift.
- Apprendre à configurer et utiliser Prometheus et Grafana pour la surveillance.
- Savoir comment interpréter les métriques et les alertes pour maintenir la santé du cluster.

## Concepts de Base

### Monitoring dans Kubernetes

- **Métriques** : Les données collectées sur les performances et la santé des composants du cluster, comme l'utilisation de la CPU, de la mémoire, et le temps de réponse des services.
- **Logs** : Les enregistrements des événements et des erreurs générés par les composants et les applications du cluster.
- **Alertes** : Les notifications automatiques déclenchées par des conditions spécifiques détectées dans les métriques ou les logs.

### Monitoring dans OpenShift

OpenShift utilise les mêmes concepts de base que Kubernetes, mais ajoute des outils et des intégrations pour faciliter la surveillance du cluster. Les principaux outils incluent Prometheus, Grafana, et Alertmanager.

## Outils de Monitoring

### Prometheus

Prometheus est un système de surveillance et d'alerte open source, conçu pour collecter et stocker des métriques, interroger les données en temps réel, et déclencher des alertes.

### Grafana

Grafana est une plateforme de visualisation et de surveillance open source, utilisée pour créer des tableaux de bord interactifs et informatifs basés sur les données collectées par Prometheus.

### Alertmanager

Alertmanager gère les alertes envoyées par Prometheus, les déduplique, les groupe, et les achemine vers les récepteurs appropriés comme les e-mails, les messages Slack, ou les systèmes de ticketing.

## Explorer les Outils de Monitoring Intégrés

### Accéder à Prometheus

1. **Ouvrir la console web OpenShift**.
2. **Naviguer vers le Monitoring** :
   - Cliquez sur **Monitoring** dans la barre de navigation.
   - Sélectionnez **Metrics** pour accéder à l'interface de Prometheus.

3. **Requêtes Prometheus** :
   - Utilisez l'interface pour effectuer des requêtes Prometheus et visualiser les métriques du cluster.
   - Exemple de requête : `sum(rate(container_cpu_usage_seconds_total[1m])) by (namespace)`

### Accéder à Grafana

1. **Ouvrir la console web OpenShift**.
2. **Naviguer vers le Monitoring** :
   - Cliquez sur **Monitoring** dans la barre de navigation.
   - Sélectionnez **Dashboards** pour accéder à l'interface de Grafana.

3. **Visualisation des Métriques** :
   - Parcourez les tableaux de bord par défaut fournis par OpenShift.
   - Créez des tableaux de bord personnalisés pour surveiller des métriques spécifiques.

### Configurer les Alertes

1. **Accéder à Alertmanager** :
   - Depuis la console Prometheus, cliquez sur **Alerting**.
   - Configurez les règles d'alerte basées sur les requêtes Prometheus.

2. **Exemple de Règle d'Alerte** :
   ```yaml
   groups:
     - name: example
       rules:
         - alert: HighPodCPUUsage
           expr: sum(rate(container_cpu_usage_seconds_total[5m])) by (pod) > 0.8
           for: 5m
           labels:
             severity: warning
           annotations:
             summary: "High CPU usage detected for pod {{ $labels.pod }}"
             description: "Pod {{ $labels.pod }} is using more than 80% of CPU for the last 5 minutes."
   ```

3. **Configurer les Récepteurs d'Alertes** :
   - Accédez à l'interface d'Alertmanager pour définir les récepteurs (e-mail, Slack, etc.).
   - Exemple de configuration pour les notifications par e-mail :
     ```yaml
     route:
       receiver: team-email

     receivers:
       - name: 'team-email'
         email_configs:
           - to: 'team@example.com'
             from: 'alertmanager@example.com'
             smarthost: 'smtp.example.com:587'
             auth_username: 'alertmanager'
             auth_identity: 'alertmanager'
             auth_password: 'password'
     ```

## Interpréter les Métriques et les Alertes

### Métriques Clés

- **Utilisation de la CPU** : Indique la charge sur les processeurs du cluster.
- **Utilisation de la Mémoire** : Surveille la consommation de mémoire.
- **Latence des Réponses** : Mesure le temps de réponse des services.
- **Taux d'Erreur** : Suivi des erreurs pour détecter les anomalies et les problèmes de performance.

### Analyser les Alertes

- **High CPU Usage** : Investiguer les pods ou les nodes utilisant une quantité excessive de CPU.
- **Memory Pressure** : Identifier les applications consommant trop de mémoire et optimiser leur utilisation.
- **Service Latency** : Déterminer les causes de la latence élevée et ajuster la configuration ou les ressources allouées.

## Conclusion

Le monitoring est essentiel pour assurer la stabilité et la performance de votre cluster OpenShift. En utilisant les outils intégrés comme Prometheus, Grafana, et Alertmanager, vous pouvez collecter et analyser des métriques, visualiser des données en temps réel, et configurer des alertes pour détecter et résoudre rapidement les problèmes. Continuez à explorer et à affiner votre configuration de monitoring pour répondre aux besoins spécifiques de vos applications et de votre infrastructure.
