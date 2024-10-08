Voici la partie "Exercice Guidé : Approvisionnement des Bases de Données Persistantes" en markdown :

---

# Exercice Guidé : Approvisionnement des Bases de Données Persistantes

Dans cet exercice, nous allons pratiquer l'approvisionnement de bases de données persistantes dans Kubernetes en utilisant des PersistentVolumes (PV) et des PersistentVolumeClaims (PVC). Nous allons créer un PVC pour demander un volume de stockage persistant, puis le monter dans un déploiement de base de données. 

## Objectifs de l'Exercice

- Apprendre à créer un PersistentVolumeClaim (PVC) pour demander du stockage persistant dans Kubernetes.
- Comprendre comment monter un PVC dans un déploiement pour stocker les données de la base de données.
- Pratiquer l'approvisionnement de bases de données persistantes dans un cluster Kubernetes.

## Instructions

### 1. Création d'un PersistentVolumeClaim (PVC)

1. **Créez un PersistentVolumeClaim** pour demander du stockage persistant :
   
   ```bash
   kubectl apply -f pvc.yaml
   ```

   Assurez-vous que le fichier `pvc.yaml` spécifie les caractéristiques du stockage souhaité, telles que la taille et le mode d'accès.

2. **Vérifiez que le PVC a été créé avec succès** :
   
   ```bash
   kubectl get pvc
   ```

### 2. Utilisation du PVC dans un Déploiement

1. **Modifiez votre déploiement** pour utiliser le PVC :
   
   ```yaml
   ...
   spec:
     containers:
     - name: my-database
       image: database-image:latest
       volumeMounts:
       - name: data-volume
         mountPath: /var/lib/database
   volumes:
   - name: data-volume
     persistentVolumeClaim:
       claimName: my-pvc
   ...
   ```

   Assurez-vous que le nom du PVC (`claimName`) correspond à celui que vous avez créé précédemment.

2. **Redéployez votre application de base de données** :
   
   ```bash
   kubectl apply -f deployment.yaml
   ```

### 3. Vérification du Stockage Persistant

1. **Vérifiez que le déploiement est en cours d'exécution** :
   
   ```bash
   kubectl get pods
   ```

   Attendez que le pod de la base de données soit en état "Running".

2. **Accédez au pod de la base de données** :
   
   ```bash
   kubectl exec -it <nom-du-pod> -- /bin/bash
   ```

   Remplacez `<nom-du-pod>` par le nom réel du pod de la base de données.

3. **Vérifiez que le volume est monté** :
   
   ```bash
   ls /var/lib/database
   ```

   Vous devriez voir les fichiers de données de la base de données montés dans ce répertoire.

## Conclusion

Cet exercice vous a permis de pratiquer l'approvisionnement de bases de données persistantes dans Kubernetes en utilisant des PersistentVolumes et des PersistentVolumeClaims. En utilisant cette approche, vous pouvez garantir que les données de votre base de données sont conservées de manière fiable même en cas de redémarrage ou de mise à jour des pods.

---

Cet exercice devrait vous donner une bonne expérience pratique dans l'approvisionnement de bases de données persistantes dans Kubernetes. Si vous avez des questions supplémentaires ou si vous rencontrez des difficultés lors de cet exercice, n'hésitez pas à demander de l'aide !