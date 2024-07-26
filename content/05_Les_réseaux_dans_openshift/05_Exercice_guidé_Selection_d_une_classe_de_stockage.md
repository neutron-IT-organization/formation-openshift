# Exercice Guidé : Zones de Stockage

Dans cet exercice, nous allons explorer l'utilisation des zones de stockage dans OpenShift. Les zones de stockage permettent de spécifier des emplacements physiques ou logiques spécifiques pour le stockage persistant, ce qui peut être utile pour la résilience des données et la conformité aux réglementations.

## Objectifs de l'Exercice

- Apprendre à définir des zones de stockage dans OpenShift.
- Comprendre comment utiliser les zones de stockage pour garantir la résilience des données.
- Pratiquer l'utilisation des zones de stockage dans un environnement OpenShift.

## Instructions

### 1. Définition des Zones de Stockage

1. **Créez une ou plusieurs zones de stockage** en fonction de vos besoins spécifiques. Vous pouvez utiliser la commande `oc create` pour créer des objets de zone de stockage à partir de fichiers de configuration YAML.

2. **Vérifiez que les zones de stockage ont été créées avec succès** :
   
   ```bash
   oc get storagezones
   ```

### 2. Attribution des Applications aux Zones de Stockage

1. **Modifiez vos déploiements d'applications pour utiliser des PVC avec des zones de stockage spécifiques** :
   
   ```yaml
   ...
   spec:
     volumeClaimTemplates:
     - metadata:
         name: my-pvc
       spec:
         storageClassName: my-storage-class
         storageZone: zone1
         accessModes:
           - ReadWriteOnce
         resources:
           requests:
             storage: 10Gi
   ...
   ```

   Assurez-vous que le champ `storageZone` est défini sur la zone de stockage appropriée pour chaque PVC.

2. **Redéployez vos applications avec les nouvelles configurations de PVC** :
   
   ```bash
   oc apply -f deployment.yaml
   ```

### 3. Vérification de la Configuration des Zones de Stockage

1. **Vérifiez que les applications sont correctement configurées avec les zones de stockage** :
   
   ```bash
   oc describe pod <nom-du-pod>
   ```

   Assurez-vous que les volumes montés dans les pods utilisent les zones de stockage spécifiées.

2. **Vérifiez que les données sont stockées dans les zones de stockage correctes** :
   
   Utilisez les outils de gestion du stockage OpenShift pour vérifier que les données sont stockées dans les zones de stockage appropriées et que la réplication des données est correctement configurée.

## Conclusion

Cet exercice vous a permis de pratiquer l'utilisation des zones de stockage dans OpenShift pour garantir la résilience des données et répondre aux exigences de conformité. En utilisant les zones de stockage, vous pouvez contrôler précisément où les données sont stockées dans votre cluster OpenShift, ce qui est essentiel pour garantir la disponibilité et l'intégrité des données.