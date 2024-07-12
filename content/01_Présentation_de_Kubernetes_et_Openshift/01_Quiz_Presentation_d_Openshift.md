# Quiz : Composants de OpenShift

Testez vos connaissances sur les composants d'OpenShift avec ce quiz. Répondez aux questions ci-dessous pour évaluer votre compréhension des concepts clés et des rôles des différents composants.

## Questions

### 1. Quel est le rôle principal du Master Node dans un cluster OpenShift ?
- A. Exécuter les conteneurs
- B. Gérer les API et planifier les workloads
- C. Stocker les images de conteneurs
- D. Gérer le réseau des conteneurs

### 2. Quel composant du Master Node s'occupe de l'assignation des pods aux nodes ?
- A. API Server
- B. Controller Manager
- C. Scheduler
- D. Kubelet

### 3. Quel composant du Node assure que les conteneurs sont lancés et opérationnels ?
- A. Kube-proxy
- B. Kubelet
- C. Etcd
- D. Router

### 4. Quelle est la fonction principale d'Etcd dans un cluster OpenShift ?
- A. Exécuter les conteneurs
- B. Gérer les règles de réseau
- C. Stocker les données de configuration du cluster
- D. Balancer la charge du trafic entrant

### 5. Quel composant est responsable de stocker les images de conteneurs dans OpenShift ?
- A. Registry
- B. Router
- C. Controller Manager
- D. API Server

### 6. Quel composant d'OpenShift gère le trafic entrant vers les applications ?
- A. Kube-proxy
- B. Etcd
- C. Router
- D. Kubelet

### 7. Quelle interface d'OpenShift permet aux utilisateurs d'interagir graphiquement avec le cluster ?
- A. CLI OpenShift (`oc`)
- B. Kube-proxy
- C. Web Console
- D. Etcd

### 8. Lequel des éléments suivants n'est pas un type de build intégré dans OpenShift ?
- A. Source-to-Image (S2I)
- B. Dockerfile
- C. Maven Build
- D. Pipeline

### 9. Qu'est-ce qu'un Project dans OpenShift ?
- A. Un ensemble de conteneurs
- B. Un espace de noms (namespace) regroupant des ressources liées
- C. Un composant de routage du trafic
- D. Un fichier de configuration des déploiements

### 10. Quel composant d'OpenShift permet d'appliquer des quotas de ressources par projet ?
- A. Etcd
- B. Registry
- C. Controller Manager
- D. Quota Manager

## Réponses

1. B. Gérer les API et planifier les workloads
2. C. Scheduler
3. B. Kubelet
4. C. Stocker les données de configuration du cluster
5. A. Registry
6. C. Router
7. C. Web Console
8. C. Maven Build
9. B. Un espace de noms (namespace) regroupant des ressources liées
10. D. Quota Manager

---

Bravo d'avoir complété ce quiz ! Si vous avez rencontré des difficultés, n'hésitez pas à revoir la section sur les composants d'OpenShift pour renforcer votre compréhension.
