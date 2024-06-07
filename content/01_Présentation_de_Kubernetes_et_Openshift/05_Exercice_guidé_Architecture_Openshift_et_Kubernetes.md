# Exercice Guidé : Architecture OpenShift et Kubernetes

Dans cet exercice, nous allons explorer l'architecture d'OpenShift et Kubernetes en détails. Vous apprendrez à identifier les principaux composants et comprendre leur rôle dans le fonctionnement d'un cluster.

## Objectifs de l'exercice

- Comprendre les composants principaux d'OpenShift et Kubernetes
- Explorer la configuration des masters et des nodes
- Visualiser les interactions entre les composants
- Utiliser les commandes CLI pour obtenir des informations sur les composants

## Prérequis

- Accès à un cluster OpenShift avec des identifiants valides
- Connexion Internet et un terminal avec l'outil de ligne de commande `oc` configuré

## Étape 1 : Comprendre les composants principaux

### 1.1 Master Node

Le Master Node est responsable de la gestion du cluster. Les composants clés du Master Node incluent :
- **API Server** : Point d'entrée pour toutes les commandes REST, gère les authentifications et les autorisations.
- **Etcd** : Stockage clé-valeur distribué pour toutes les données de configuration du cluster.
- **Scheduler** : Assigne des pods aux nodes en fonction des besoins de ressources et des contraintes.
- **Controller Manager** : Exécute les contrôleurs qui régulent l'état du cluster (réplication, endpoints, etc.).

### 1.2 Worker Nodes

Les Worker Nodes exécutent les applications conteneurisées. Les composants clés des Worker Nodes incluent :
- **Kubelet** : Agent qui assure le bon fonctionnement des pods sur le node.
- **Kube-proxy** : Gère le réseau de services et la distribution du trafic.
- **Container Runtime** : Exécute les conteneurs (par exemple, Docker, CRI-O).

### 1.3 Composants OpenShift supplémentaires

En plus des composants Kubernetes, OpenShift inclut :
- **Router** : Gère le routage du trafic entrant vers les services exposés.
- **Registry** : Stocke et distribue les images de conteneurs.

## Étape 2 : Explorer la configuration des masters et des nodes

### 2.1 Inspecter les Masters

1. **Lister les nodes** :
   ```sh
   oc get nodes
   ```

2. **Détailler un Master Node** :
   ```sh
   oc describe node <nom-du-master-node>
   ```

3. **Examiner les composants du Master** :
   - Accédez aux logs de l'API Server :
     ```sh
     oc logs -n openshift-kube-apiserver <nom-du-pod-apiserver>
     ```
   - Affichez la configuration du Scheduler :
     ```sh
     oc get pod -n openshift-kube-scheduler -o yaml
     ```

### 2.2 Inspecter les Worker Nodes

1. **Lister les pods sur un Worker Node** :
   ```sh
   oc get pods --all-namespaces -o wide | grep <nom-du-worker-node>
   ```

2. **Détailler un Worker Node** :
   ```sh
   oc describe node <nom-du-worker-node>
   ```

3. **Vérifier le fonctionnement de Kubelet** :
   - Accédez aux logs de Kubelet :
     ```sh
     journalctl -u kubelet
     ```

## Étape 3 : Visualiser les interactions entre les composants

### 3.1 Observer les pods dans le namespace kube-system

1. **Lister les pods du namespace kube-system** :
   ```sh
   oc get pods -n kube-system
   ```

2. **Détailler un pod spécifique** :
   ```sh
   oc describe pod <nom-du-pod> -n kube-system
   ```

3. **Visualiser les logs d'un pod** :
   ```sh
   oc logs <nom-du-pod> -n kube-system
   ```

### 3.2 Interactions réseau

1. **Lister les services et endpoints** :
   ```sh
   oc get svc -A
   oc get endpoints -A
   ```

2. **Détailler un service spécifique** :
   ```sh
   oc describe svc <nom-du-service> -n <namespace>
   ```

3. **Vérifier les routes exposées par le Router** :
   ```sh
   oc get routes -A
   ```

## Étape 4 : Utiliser les commandes CLI pour obtenir des informations sur les composants

### 4.1 Utiliser `oc` pour interagir avec les ressources

1. **Obtenir des informations sur les nodes** :
   ```sh
   oc get nodes
   oc describe node <nom-du-node>
   ```

2. **Lister les pods dans un namespace spécifique** :
   ```sh
   oc get pods -n <namespace>
   ```

3. **Afficher les détails d'un pod** :
   ```sh
   oc describe pod <nom-du-pod> -n <namespace>
   ```

4. **Visualiser les logs d'un pod** :
   ```sh
   oc logs <nom-du-pod> -n <namespace>
   ```

### 4.2 Explorer les ressources spécifiques d'OpenShift

1. **Lister les routes** :
   ```sh
   oc get routes -A
   ```

2. **Afficher les builds et build configs** :
   ```sh
   oc get builds -A
   oc get bc -A
   ```

3. **Détailler un build spécifique** :
   ```sh
   oc describe build <nom-du-build> -n <namespace>
   ```

## Conclusion

Vous avez maintenant une compréhension plus approfondie de l'architecture d'OpenShift et Kubernetes. Vous savez comment identifier et interagir avec les principaux composants du Master Node et des Worker Nodes, ainsi que comment utiliser les commandes CLI pour obtenir des informations détaillées. Continuez à explorer et à pratiquer pour renforcer vos compétences.

---

Dans la prochaine section, nous aborderons la surveillance du cluster OpenShift et comment utiliser les outils intégrés pour monitorer les performances et la santé des ressources.