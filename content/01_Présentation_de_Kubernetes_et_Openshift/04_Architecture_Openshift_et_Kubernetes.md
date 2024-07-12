# Concepts Architecturaux de Kubernetes

TOCOMPLETE

## Objectif

Dans cette section, nous allons explorer l'architecture d'OpenShift.

### Concepts

Kubernetes repose sur plusieurs serveurs, ou nodes, pour garantir la résilience et l’évolutivité des applications qu’il gère. Ces nodes, qu’ils soient physiques ou virtuels, fournissent les ressources nécessaires au cluster. Il y a deux types de nodes, chacun ayant un rôle distinct dans le fonctionnement du cluster. Les nodes du plan de contrôle gèrent la coordination globale du cluster, notamment la planification des charges de travail et la gestion de l’état de configuration du cluster. Les nodes du plan de calcul exécutent les applications, en communiquant avec les nodes du plan de contrôle pour recevoir les demandes d’exécution des applications.

![Generic architecture](./images/architecture.png)

La communication entre le plan de contrôle et les nodes du cluster s'effectue via le service kubelet qui fonctionne sur chaque node. Bien qu'un serveur puisse servir à la fois de node de plan de contrôle et de calcul, ces rôles sont souvent séparés pour une meilleure stabilité, sécurité et gérabilité.

#### Composants du Plan de Contrôle

- **etcd** : Une base de données distribuée clé-valeur qui stocke les configurations du cluster.
- **kube-apiserver** : Le service frontal qui expose l’API Kubernetes.
- **kube-scheduler** : Un service qui détermine les nodes de calcul disponibles pour les nouvelles demandes de pods.
- **kubelet** : L'agent principal sur chaque node de calcul, chargé de l'exécution des pods demandés via l'API et le planificateur.
- **CRI (Container Runtime Interface)** : Une interface de plug-in pour la communication entre kubelet et les configurations de pods.
- **cri-o** : Un moteur d’exécution compatible OCI qui facilite la communication entre kubelet et les demandes de configuration de pods.

### Concepts Architecturaux de Red Hat OpenShift Container Platform

Red Hat OpenShift Container Platform (RHOCP) utilise Red Hat Enterprise Linux CoreOS pour ses nodes. Grâce à cette orchestration, les administrateurs n’ont pas besoin de configurer manuellement les machines hôtes. Le Machine Configuration Operator (MCO) de RHOCP gère le système d’exploitation sous-jacent. OpenShift utilise le MCO pour configurer les systèmes CoreOS, et les administrateurs peuvent l’utiliser pour des configurations supplémentaires des nodes.

Un autre élément clé de RHOCP est l’Operator Lifecycle Manager (OLM), qui simplifie l’installation, les mises à jour et la gestion des opérateurs Kubernetes et des services au sein du cluster. L’OLM utilise des manifestes d’opérateur pour déployer des opérateurs à partir d’un catalogue de cluster, pour chaque espace de noms.

### Présentation des Configurations de Cluster RHOCP

RHOCP peut être déployé via deux méthodes principales, permettant chacune de distribuer un cluster complet sur les nodes fournis.

- **Infrastructure IPI (Installer-Provisioned Infrastructure)** : Cette méthode repose sur la création d’un node d’amorçage qui automatise la plupart des tâches de déploiement du cluster. Elle est disponible pour les machines virtuelles ou le matériel nu sur site, ainsi que via divers fournisseurs de cloud public tels que IBM Cloud, Amazon Web Services et Google Cloud Platform.

- **Infrastructure UPI (User-Provisioned Infrastructure)** : Plus personnalisable, cette méthode permet à l’administrateur de configurer chaque aspect du déploiement du cluster. Bien que moins automatisée, elle est idéale pour les déploiements nécessitant une intégration à une infrastructure d’entreprise existante, comme les services DHCP ou DNS.

Les deux méthodes visent à fournir un cluster RHOCP opérationnel pour le déploiement des charges de travail et des applications métiers. Il est essentiel de choisir la méthode la plus adaptée à votre environnement d’entreprise pour débuter avec RHOCP.
