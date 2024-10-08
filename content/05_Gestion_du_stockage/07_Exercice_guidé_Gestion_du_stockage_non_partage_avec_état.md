# Exercice Guidée : Gestion du Stockage Non-Partagé avec État

Dans cet exercice, nous allons pratiquer la gestion du stockage non-partagé avec états dans OpenShift. Nous allons créer un PersistentVolumeClaim (PVC) pour attacher un volume de stockage persistant à un pod spécifique, puis configurer une application pour utiliser ce stockage pour stocker des données spécifiques à cet instance de l'application.

## Objectifs de l'Exercice

- Apprendre à créer un PersistentVolumeClaim (PVC) dans OpenShift pour le stockage non-partagé avec états.
- Comprendre comment configurer une application pour utiliser le stockage persistant attaché à un pod spécifique.
- Pratiquer la gestion du stockage non-partagé avec états dans un environnement OpenShift.

## Instructions

### 1. Création d'un PersistentVolumeClaim (PVC)

1. **Créez un PersistentVolumeClaim (PVC)** pour demander du stockage persistant :
   
   ```bash
   oc create -f pvc.yaml
   ```

   Assurez-vous que le fichier `pvc.yaml` spécifie les caractéristiques du stockage souhaité, telles que la taille et le mode d'accès.

2. **Vérifiez que le PVC a été créé avec succès** :
   
   ```bash
   oc get pvc
   ```

### 2. Configuration de l'Application pour Utiliser le Stockage Persistant

1. **Modifiez votre configuration d'application pour utiliser le PVC** :
   
   ```yaml
   ...
   spec:
     volumeMounts:
     - name: data-volume
       mountPath: /data
   volumes:
   - name: data-volume
     persistentVolumeClaim:
       claimName: my-pvc
   ...
   ```

   Assurez-vous que le nom du PVC (`claimName`) correspond à celui que vous avez créé précédemment.

2. **Redéployez votre application** :
   
   ```bash
   oc apply -f deployment.yaml
   ```

### 3. Vérification de la Configuration du Stockage Non-Partagé avec États

1. **Vérifiez que l'application est correctement configurée avec le stockage persistant** :
   
   ```bash
   oc describe pod <nom-du-pod>
   ```

   Assurez-vous que le volume monté dans le pod utilise le PVC spécifié.

2. **Vérifiez que les données sont stockées dans le stockage persistant** :
   
   Utilisez les outils de gestion du stockage OpenShift pour vérifier que les données sont stockées dans le PVC associé à l'application.

## Conclusion

Cet exercice vous a permis de pratiquer la gestion du stockage non-partagé avec états dans OpenShift. En utilisant des PersistentVolumeClaims, vous pouvez attacher dynamiquement des volumes de stockage persistant à des pods spécifiques, ce qui permet aux applications d'accéder à des données persistantes tout en garantissant l'isolement des données entre les instances de l'application.