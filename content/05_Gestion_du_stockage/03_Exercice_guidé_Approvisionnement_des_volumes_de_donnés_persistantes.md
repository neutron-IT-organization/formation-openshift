# Exercice : Créer et Consommer un Volume Persistant dans OpenShift

**Objectif** : À travers cet exercice, vous allez :

1. Créer un **Persistent Volume Claim (PVC)** utilisant une **Storage Class**.
2. Déployer un **pod** qui consomme le PVC pour stocker des données persistantes.
3. Vérifier le bon fonctionnement du volume persistant.

---

### Prérequis

- Accès à un cluster OpenShift.
- Une Storage Class nommée `lvms-vg1` configurée comme par défaut :

  ```
  NAME                 PROVISIONER   RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
  lvms-vg1 (default)   topolvm.io    Delete          WaitForFirstConsumer   true                   13d
  ```

---

### Étape 1 : Créer un Persistent Volume Claim (PVC)

1. Créez un fichier `pvc.yaml` avec le contenu suivant :

   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: my-pvc
   spec:
     accessModes:
       - ReadWriteOnce
     resources:
       requests:
         storage: 5Gi
     storageClassName: lvms-vg1
   ```

   **Explications** :
   - `accessModes: ReadWriteOnce` : Seul un pod peut écrire sur le volume à la fois.
   - `storage: 5Gi` : Demande un volume de 5 GiB.
   - `storageClassName: lvms-vg1` : Utilise la Storage Class `lvms-vg1` pour l’approvisionnement dynamique du PV.

2. Déployez le PVC en exécutant la commande suivante :

   ```bash
   oc apply -f pvc.yaml
   ```

3. Vérifiez que le PVC a bien été créé et qu'il est en attente de liaison avec un volume :

   ```bash
   oc get pvc my-pvc
   ```

   La colonne `STATUS` devrait afficher `Pending`, ce qui indique que le PVC attend qu'un pod soit créé pour consommer le volume.

---

### Étape 2 : Déployer un Pod utilisant le PVC

1. Créez un fichier `pod.yaml` pour déployer un pod qui montera le PVC :

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: my-pod
   spec:
     containers:
       - name: my-container
         image: nginx
         volumeMounts:
           - mountPath: /usr/share/nginx/html
             name: my-storage
     volumes:
       - name: my-storage
         persistentVolumeClaim:
           claimName: my-pvc
   ```

   **Explications** :
   - `image: nginx` : Utilise l'image de conteneur **nginx**.
   - `volumeMounts` : Monte le PVC `my-pvc` dans le conteneur sous le chemin `/usr/share/nginx/html`.
   - `volumes` : Associe le PVC `my-pvc` comme source de stockage pour le volume `my-storage`.

2. Déployez le pod en exécutant la commande suivante :

   ```bash
   oc apply -f pod.yaml
   ```

3. Vérifiez que le pod est bien créé et en cours d'exécution :

   ```bash
   oc get pod my-pod
   ```

   Attendez que le statut du pod soit `Running`.

---

### Étape 3 : Vérifier le Montage et Tester le Stockage Persistant

1. Accédez au conteneur pour vérifier que le volume est bien monté :

   ```bash
   oc exec -it my-pod -- /bin/bash
   ```

2. À l'intérieur du conteneur, créez un fichier pour vérifier la persistance des données :

   ```bash
   echo "Bonjour, OpenShift!" > /usr/share/nginx/html/index.html
   ```

3. Sortez du conteneur et redémarrez le pod pour simuler un redéploiement :

   ```bash
   oc delete pod my-pod
   oc apply -f pod.yaml
   ```

4. Après le redémarrage du pod, accédez à nouveau au conteneur :

   ```bash
   oc exec -it my-pod -- /bin/bash
   ```

5. Vérifiez que le fichier `index.html` existe toujours :

   ```bash
   cat /usr/share/nginx/html/index.html
   ```

   Si le fichier contient le message `Bonjour, OpenShift!`, cela signifie que le stockage persistant est fonctionnel, et les données ont été conservées malgré le redémarrage du pod.

---

### Étape 4 : Nettoyer les Ressources

Pour terminer cet exercice, supprimez les ressources créées pour libérer le stockage :

```bash
oc delete pod my-pod
oc delete pvc my-pvc
```

---

### Prochaine Section

Dans cet exercice, vous avez appris à créer et consommer un **Persistent Volume Claim (PVC)** en utilisant une **Storage Class**. Vous avez également vu comment un PVC reste lié à un PV et conserve les données après le redémarrage d'un pod. Dans la prochaine section, nous détaillerons les **Storage Classes**, leurs paramètres, et les différentes options pour configurer un stockage optimisé selon les besoins de vos applications. Vous découvrirez également comment ajuster les stratégies de provisionnement et de recyclage pour une meilleure gestion des ressources.
