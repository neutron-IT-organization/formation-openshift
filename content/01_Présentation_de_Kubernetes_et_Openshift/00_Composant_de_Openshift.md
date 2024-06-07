# Composants de OpenShift

Dans cette section, nous allons explorer en détail les différents composants d'OpenShift et comprendre leur rôle dans le fonctionnement global du cluster. OpenShift, construit sur Kubernetes, ajoute plusieurs fonctionnalités pour simplifier le déploiement, la gestion et la mise à l'échelle des applications conteneurisées.

## Aperçu des composants principaux

### 1. **Master Node**
Le Master Node est le cerveau du cluster OpenShift. Il gère les API, planifie les workloads, et assure la communication entre les différents composants. Voici les principaux services exécutés sur le Master Node :

- **API Server** : Gère les demandes RESTful pour configurer l'état du cluster. C'est le point d'entrée principal pour l'ensemble des commandes administratives.
  - Expose l'API Kubernetes.
  - Authentifie les utilisateurs et les applications.
  - Valide et persiste l'état des objets API.

- **Controller Manager** : Un daemon qui régule les contrôleurs intégrés à Kubernetes. Chaque contrôleur veille sur le cluster pour s'assurer qu'il se rapproche toujours de l'état désiré (par exemple, un ReplicaSet s'assure qu'un nombre spécifié de pods sont exécutés).
  - Node Controller : Gère l'état des nodes (ajout/suppression).
  - Replication Controller : Maintient le nombre souhaité de copies de pods.
  - Endpoints Controller : Gère les objets endpoints.

- **Scheduler** : Assigne les pods aux nodes en fonction des ressources disponibles et des contraintes spécifiées. Le scheduler analyse les besoins de chaque pod et trouve le meilleur emplacement pour son exécution.
  - Considère les ressources CPU et mémoire.
  - Applique des politiques d'affinité et d'anti-affinité.

### 2. **Nodes**
Les Nodes sont les machines (physiques ou virtuelles) qui exécutent les conteneurs via Kubernetes. Chaque Node contient plusieurs composants importants :

- **Kubelet** : Assure que les conteneurs sont lancés et opérationnels sur le node. Il surveille les pods assignés à son node et signale au Master leur état.
  - Interagit avec le runtime de conteneur pour démarrer et arrêter les conteneurs.
  - Lit les manifestes de pod pour s'assurer que les pods sont en état désiré.

- **Kube-proxy** : Gère les règles de réseau sur chaque node. Il permet la communication entre les services et les pods.
  - Maintient les règles de réseau pour rediriger le trafic réseau aux pods appropriés.
  - Gère l'équilibrage de charge pour les services.

- **CRI-O (ou Docker)** : Un runtime de conteneur pour exécuter les conteneurs. OpenShift utilise CRI-O par défaut pour une compatibilité et une performance optimales, bien que Docker puisse aussi être utilisé.

### 3. **Etcd**
Etcd est une base de données clé-valeur distribuée qui stocke toutes les données de configuration du cluster Kubernetes. Il joue un rôle crucial car il conserve l'état souhaité du cluster.
- Réplication distribuée pour tolérance aux pannes.
- Assure la cohérence forte des données.

### 4. **Registry**
Le registre intégré d'OpenShift stocke les images de conteneurs nécessaires pour déployer les applications. Il peut être configuré pour utiliser des registres externes (comme Docker Hub) ou internes pour le stockage des images.
- Supporte l'authentification et l'autorisation.
- Intégration avec les builds S2I (Source-to-Image).

### 5. **Router**
Les routers gèrent le trafic entrant vers les applications exécutées sur OpenShift. Ils fournissent des fonctionnalités de load balancing et d'exposition des services via des routes HTTP(S).
- Support pour les certificats SSL/TLS.
- Capacité à gérer des règles de routage basées sur des noms de domaine.

### 6. **Web Console**
La console web est une interface utilisateur graphique qui permet aux administrateurs et aux développeurs d'interagir avec le cluster. Elle offre une vue d'ensemble des projets, des applications, des ressources et des métriques.
- Interface intuitive pour déployer et gérer des applications.
- Vue en temps réel des métriques et des logs.

### 7. **OpenShift CLI (`oc`)**
Le client en ligne de commande `oc` permet d'interagir avec OpenShift de manière scriptée. Il est utilisé pour créer, modifier et supprimer des ressources, ainsi que pour déployer des applications et gérer les configurations.
- Automatisation des tâches via des scripts.
- Gestion des ressources et des configurations.

## Fonctionnalités supplémentaires d'OpenShift

### 1. **Builds**
OpenShift fournit des capacités de build intégrées pour automatiser la création d'images de conteneurs à partir du code source. Les types de builds incluent :
- **Source-to-Image (S2I)** : Convertit le code source en une image de conteneur exécutable.
  - Intègre les dépendances et le code source.
  - Génère une image prête à être déployée.

- **Dockerfile** : Utilise des Dockerfiles pour créer des images personnalisées.
  - Offre une flexibilité totale pour définir le processus de build.
  - Permet l'utilisation de Dockerfiles existants.

- **Pipeline** : Utilise Jenkins pour orchestrer des builds CI/CD.
  - Intégration avec des systèmes de contrôle de version comme Git.
  - Définition de pipelines complexes avec plusieurs étapes de build, test et déploiement.

### 2. **Deployment Configs**
OpenShift utilise des Deployment Configs pour gérer les déploiements des applications. Cela inclut les stratégies de déploiement telles que les rolling updates et les recreates.
- **Rolling Updates** : Déploiement progressif des nouvelles versions sans interruption de service.
- **Recreate** : Arrêt des anciennes versions avant de lancer les nouvelles.

### 3. **Projects et Quotas**
Les projets sont des espaces de noms (namespaces) qui regroupent des ressources liées. OpenShift permet de définir des quotas pour contrôler l'utilisation des ressources par projet.
- Isolation des ressources et des permissions.
- Gestion des quotas pour CPU, mémoire et nombre de pods.

### 4. **Templates**
Les templates sont des objets réutilisables qui définissent un ensemble de ressources Kubernetes. Ils simplifient le déploiement d'applications complexes en permettant de créer plusieurs objets à partir d'un seul fichier template.
- Personnalisation via des paramètres.
- Réutilisation et partage de templates pour standardiser les déploiements.

## Conclusion

La compréhension des composants d'OpenShift est cruciale pour gérer efficacement un cluster et déployer des applications. Chaque composant joue un rôle spécifique et interagit avec les autres pour offrir une plateforme robuste et scalable pour les conteneurs.

Dans la prochaine section, nous approfondirons ces composants et apprendrons à les manipuler via des exercices pratiques.
