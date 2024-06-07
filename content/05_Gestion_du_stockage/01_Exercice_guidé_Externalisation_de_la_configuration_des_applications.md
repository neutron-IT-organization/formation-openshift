Bien sûr ! Voici la partie "Exercice Guidé : Externalisation de la Configuration des Applications" avec les lignes de commande à utiliser :

---

# Exercice Guidé : Externalisation de la Configuration des Applications

Dans cet exercice, nous allons pratiquer l'externalisation de la configuration des applications dans Kubernetes en utilisant des ConfigMaps et des Secrets. Nous allons créer et utiliser des ConfigMaps pour stocker la configuration de l'application et des Secrets pour gérer des informations sensibles, puis les utiliser dans les déploiements de nos applications.

## Objectifs de l'Exercice

- Apprendre à créer et à utiliser des ConfigMaps pour externaliser la configuration des applications.
- Comprendre comment créer et utiliser des Secrets pour gérer des informations sensibles.
- Pratiquer l'utilisation de ConfigMaps et de Secrets dans les déploiements d'applications Kubernetes.

## Instructions

### 1. Création d'un ConfigMap

1. **Créez un ConfigMap** contenant la configuration de base de votre application :
   
   ```bash
   kubectl create configmap my-config --from-file=config.yaml
   ```

   Remplacez `config.yaml` par le chemin de votre fichier de configuration.

2. **Vérifiez que le ConfigMap a été créé** :
   
   ```bash
   kubectl get configmap
   ```

### 2. Utilisation d'un ConfigMap dans un Déploiement

1. **Modifiez votre déploiement** pour utiliser le ConfigMap :
   
   ```yaml
   ...
   spec:
     containers:
     - name: my-app
       image: my-image:latest
       volumeMounts:
       - name: config-volume
         mountPath: /config
   volumes:
   - name: config-volume
     configMap:
       name: my-config
   ...
   ```

2. **Redéployez votre application** :
   
   ```bash
   kubectl apply -f deployment.yaml
   ```

### 3. Création d'un Secret

1. **Créez un Secret** contenant des informations sensibles :
   
   ```bash
   kubectl create secret generic my-secret --from-literal=username=myuser --from-literal=password=mypassword
   ```

2. **Vérifiez que le Secret a été créé** :
   
   ```bash
   kubectl get secret
   ```

### 4. Utilisation d'un Secret dans un Déploiement

1. **Modifiez votre déploiement** pour utiliser le Secret :
   
   ```yaml
   ...
   spec:
     containers:
     - name: my-app
       image: my-image:latest
       volumeMounts:
       - name: secret-volume
         mountPath: /secrets
   volumes:
   - name: secret-volume
     secret:
       secretName: my-secret
   ...
   ```

2. **Redéployez votre application** :
   
   ```bash
   kubectl apply -f deployment.yaml
   ```

## Conclusion

Cet exercice vous a permis de pratiquer l'externalisation de la configuration des applications dans Kubernetes en utilisant des ConfigMaps et des Secrets. En séparant la configuration de l'application et les informations sensibles de leurs images de conteneurs, vous pouvez rendre vos applications plus flexibles, modulaires et sécurisées dans un environnement Kubernetes.

---

Cet exercice devrait vous donner une bonne expérience pratique dans l'externalisation de la configuration des applications avec ConfigMaps et Secrets dans Kubernetes. Si vous avez des questions supplémentaires ou si vous rencontrez des difficultés lors de cet exercice, n'hésitez pas à demander de l'aide !