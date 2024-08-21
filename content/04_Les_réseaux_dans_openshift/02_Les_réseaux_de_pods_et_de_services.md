# Services et Route dans OpenShift

## Introduction

Dans OpenShift, l'exposition des applications à un accès externe est essentielle pour les utilisateurs finaux, et les services d'équilibrage de charge ainsi que les routes jouent un rôle clé dans cette tâche. Cette section explore comment configurer ces services et routes pour assurer la disponibilité et la performance des applications.

## Objectifs de la section

1. Comprendre le rôle des services d'équilibrage de charge et des routes dans OpenShift.
2. Apprendre à configurer et à utiliser des services d'équilibrage de charge pour exposer des services non HTTP.
3. Découvrir les alternatives d'exposition de services comme NodePort et leur utilisation dans différents environnements.
4. Explorer des solutions comme MetalLB pour les environnements sans fournisseurs de cloud.
5. Comprendre le fonctionnement et la configuration des routes dans OpenShift pour l'exposition des applications HTTP.

---

## Les services d'équilibrage de charge dans OpenShift

Dans un environnement Kubernetes, les services d'équilibrage de charge (LoadBalancer) répartissent le trafic réseau vers les pods qui composent une application. Cela permet d'assurer une haute disponibilité et une meilleure évolutivité des services. Lorsque plusieurs pods exécutent la même application, l'équilibrage de charge permet de répartir le trafic entre eux, assurant ainsi que la charge est distribuée équitablement et que l'application reste disponible même en cas de défaillance d'un ou plusieurs pods.

Les services d'équilibrage de charge sont particulièrement utilisés dans des environnements de cloud public, où le fournisseur de cloud gère l'infrastructure réseau nécessaire. Par exemple, dans un cluster OpenShift hébergé sur AWS ou Google Cloud, les API du fournisseur de cloud sont utilisées pour configurer automatiquement les composants d'équilibrage de charge externes. Cela simplifie la gestion pour les développeurs et les administrateurs, qui n'ont pas besoin de se soucier des détails d'infrastructure sous-jacents.

Cependant, dans des environnements on-premise ou sur des infrastructures sans fournisseur de cloud, l'utilisation d'un équilibreur de charge nécessite une configuration manuelle. Dans ces scénarios, des solutions comme MetalLB peuvent être utilisées pour simuler le comportement des équilibreurs de charge en cloud.

### Exposition de Services Non HTTP

Tous les services ne fonctionnent pas avec des protocoles HTTP/HTTPS. Par exemple, les services SSH, FTP ou les bases de données peuvent nécessiter une exposition externe qui ne passe pas par un serveur web. Pour ces cas d'utilisation, les services d'équilibrage de charge offrent une méthode pour exposer ces services au monde extérieur.

Lorsque vous configurez un service d'équilibrage de charge pour un protocole non HTTP, vous devez spécifier les ports et les adresses IP sur lesquels le service sera accessible. Ce type de configuration assure que les utilisateurs externes peuvent se connecter directement au service, sans avoir besoin de passer par un intermédiaire comme un proxy HTTP.

### NodePort

Les services NodePort sont une autre méthode d'exposition de services en dehors du cluster. Contrairement aux services LoadBalancer, NodePort expose un service sur un port spécifique sur chaque nœud du cluster. Cela signifie que le service est accessible via l'adresse IP de n'importe quel nœud du cluster, ce qui offre une certaine flexibilité dans les environnements où les services d'équilibrage de charge gérés ne sont pas disponibles.

NodePort est souvent utilisé dans des environnements de développement ou de test, où l'infrastructure réseau est limitée. Cependant, il nécessite une gestion manuelle des adresses IP et des ports, ce qui peut devenir complexe dans des environnements de production à grande échelle.

### MetalLB : Une Solution pour les Environnements Non Cloud

MetalLB est un composant d'équilibrage de charge conçu pour les environnements où les équilibreurs de charge en cloud ne sont pas disponibles. Il s'agit d'un projet open-source qui permet à Kubernetes d'assigner des adresses IP publiques à des services d'équilibrage de charge, même sur des infrastructures nues (bare metal) ou virtualisées.

MetalLB fonctionne en mode couche 2 ou en utilisant le protocole BGP (Border Gateway Protocol). Le mode couche 2 est plus simple à configurer, tandis que le mode BGP offre une meilleure intégration avec les routeurs réseau existants.

L'installation de MetalLB est gérée par l'Operator Lifecycle Manager d'OpenShift. Une fois installé, vous devez configurer des plages d'adresses IP que MetalLB pourra attribuer aux services. Cela permet de simuler un comportement de cloud public dans un environnement on-premise.

---

## Routes dans OpenShift

Les routes sont un autre composant essentiel pour exposer des applications dans OpenShift, en particulier pour les applications HTTP/HTTPS. Contrairement aux services d'équilibrage de charge qui gèrent le trafic réseau au niveau de l'infrastructure, les routes se concentrent sur l'exposition des applications web.

### Fonctionnement des Routes

Les routes dans OpenShift agissent comme un point d'entrée pour les applications HTTP/HTTPS. Elles définissent un nom de domaine (par exemple, www.example.com) qui est accessible depuis l'extérieur du cluster et qui est mappé à un service Kubernetes interne. Lorsque des requêtes arrivent sur l'adresse définie par la route, elles sont redirigées vers le service correspondant à l'intérieur du cluster.

Cette approche permet une gestion centralisée des accès HTTP/HTTPS et offre une grande flexibilité pour les applications web. Par exemple, une seule route peut diriger le trafic vers différents services en fonction du sous-domaine ou du chemin d'URL utilisé.

### Types de Routes

OpenShift supporte plusieurs types de routes, chacune offrant différents niveaux de contrôle sur la gestion du trafic et de la sécurité.

- **Edge Termination** : Dans ce mode, le TLS (Transport Layer Security) est terminé à l'edge, c'est-à-dire au niveau du routeur OpenShift. Le trafic vers l'application interne est ensuite envoyé en clair (HTTP).
- **Passthrough** : Ici, le TLS passe directement au service interne, où il est terminé. Ce mode est utilisé lorsque l'application interne doit gérer elle-même la sécurité TLS.
- **Reencrypt** : Dans ce mode, le TLS est terminé à l'edge, puis réencrypté avant d'être envoyé au service interne. Cela offre une couche supplémentaire de sécurité, en assurant que le trafic reste chiffré tout au long de son parcours.

### Avantages des Routes

Les routes dans OpenShift ne se contentent pas de mapper des noms de domaine à des services. Elles offrent également des fonctionnalités avancées comme la gestion des certificats TLS, l'équilibrage de charge au niveau applicatif, et des stratégies de routage basées sur des règles spécifiques. Cela permet une grande flexibilité dans la manière dont les applications sont exposées aux utilisateurs finaux.

Les routes sont particulièrement utiles pour les applications nécessitant des noms de domaine spécifiques et des configurations de sécurité complexes. Elles permettent également de gérer le trafic de manière plus granulaire qu'avec des services d'équilibrage de charge seuls, en offrant des options pour rediriger, réécrire ou diviser le trafic en fonction de divers critères.

### Exemple de Configuration de Route

Voici un exemple de configuration de route dans OpenShift :

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: example-route
  namespace: example
spec:
  host: www.example.com
  to:
    kind: Service
    name: example-service
  port:
    targetPort: 8080
  tls:
    termination: edge
```

Dans cet exemple, la route www.example.com redirige le trafic vers le service example-service sur le port 8080, en terminant le TLS au niveau du routeur OpenShift.

### Utilisation des Routes

Les routes sont particulièrement adaptées aux environnements où les applications doivent être exposées sur des noms de domaine spécifiques avec une gestion fine de la sécurité. Elles complètent les services d'équilibrage de charge en offrant des fonctionnalités supplémentaires pour le routage et la gestion du trafic HTTP/HTTPS.
