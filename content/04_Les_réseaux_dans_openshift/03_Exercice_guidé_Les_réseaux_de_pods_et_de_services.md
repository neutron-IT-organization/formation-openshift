# Exercice Guidé : Les Services et les Routes dans OpenShift

Dans cet exercice, vous allez créer différents types de services pour exposer vos applications et configurer des routes pour permettre un accès externe. Suivez les étapes ci-dessous pour mettre en pratique les concepts théoriques abordés dans le cours.

### Objectifs de l'Exercice

- Créer des services `ClusterIP`, `NodePort`, et `LoadBalancer`.
- Configurer une route pour exposer une application via HTTP.
- Mettre en place une route TLS en mode `edge`.
- Tester les différentes configurations de service et de route.

## Prérequis

Vous allez, au cours de cet exercice, une application qui nous affichera les resultats des jeux olympiques de paris 2024.

Pour cela créez un fichier nommé `olympic-medals-app.yaml` avec le contenu suivant :

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: olympic-medals-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: olympic-medals-app
  template:
    metadata:
      labels:
        app: olympic-medals-app
    spec:
      containers:
        - name: olympic-medals-app
          image: quay.io/neutron-it/olympic-medals-app:latest
          ports:
            - containerPort: 5000
```

**Appliquez ce service avec la commande suivante :**

```bash
oc apply -f olympic-medals-app.yaml
```

## Étape 1 : Créer un Service ClusterIP

Créez un fichier nommé `my-clusterip-service.yaml` avec le contenu suivant :

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-clusterip-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
  type: ClusterIP
```

Ce fichier YAML définit un service `ClusterIP` qui expose les pods ayant le label `app: my-app` sur le port 80.

**Appliquez ce service avec la commande suivante :**

```bash
oc apply -f my-clusterip-service.yaml
```

**Vérifiez que le service a été créé et qu'il est accessible depuis d'autres pods dans le cluster :**

```bash
oc get svc
oc describe svc my-clusterip-service
```

## Étape 2 : Créer un Service NodePort

Créez un fichier nommé `my-nodeport-service.yaml` avec le contenu suivant :

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
    nodePort: 30007
  type: NodePort
```

Ce fichier YAML définit un service `NodePort` qui expose le service sur le port 30007 de chaque nœud du cluster.

**Appliquez ce service :**

```bash
oc apply -f my-nodeport-service.yaml
```

**Vérifiez que le service est accessible en utilisant l'adresse IP de l'un des nœuds du cluster :**

```bash
oc get svc
curl http://<NODE_IP>:30007
```

Remplacez `<NODE_IP>` par l'adresse IP d'un nœud de votre cluster.


## Étape 3 : Créer un Service LoadBalancer (avec MetalLB si en environnement On-Premise)

NOTE: TODO not configured yet on the cluster

Créez un fichier nommé `my-loadbalancer-service.yaml` :

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
  type: LoadBalancer
```

**Appliquez le service :**

```bash
oc apply -f my-loadbalancer-service.yaml
```

**Vérifiez que le service est exposé avec une adresse IP externe :**

```bash
oc get svc
```

## Étape 4 : Créer une Route pour Exposer le Service

Créez un fichier nommé `my-route.yaml` pour exposer votre application via HTTP :

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: my-http-route
spec:
  host: my-app.example.com
  to:
    kind: Service
    name: my-clusterip-service
```

**Appliquez cette route :**

```bash
oc apply -f my-route.yaml
```

**Vérifiez que la route est créée et accessible :**

```bash
oc get routes
curl http://my-app.example.com
```

Assurez-vous que le DNS `my-app.example.com` pointe vers votre cluster OpenShift.

## Étape 5 : Configurer une Route TLS (Mode Edge)

Créez un fichier nommé `my-edge-route.yaml` :

```yaml
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  name: my-edge-route
spec:
  host: my-app-secure.example.com
  to:
    kind: Service
    name: my-clusterip-service
  tls:
    termination: edge
```

**Appliquez la route TLS :**

```bash
oc apply -f my-edge-route.yaml
```

**Testez l'accès HTTPS à l'application :**

```bash
curl -k https://my-app-secure.example.com
```

## Étape 6 : Nettoyage

Après avoir terminé les tests, nettoyez les ressources créées pour éviter les coûts inutiles :

```bash
oc delete svc my-clusterip-service my-nodeport-service my-loadbalancer-service
oc delete route my-http-route my-edge-route
```

## Conclusion

En suivant cet exercice guidé, vous avez mis en pratique la création de différents types de services et de routes dans OpenShift. Vous avez appris à exposer des applications à l'intérieur et à l'extérieur du cluster et à sécuriser les connexions à l'aide des routes TLS.
