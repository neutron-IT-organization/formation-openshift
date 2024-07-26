# Approvisionnement des Bases de Données Persistantes

Dans Kubernetes, il est essentiel de pouvoir provisionner des volumes persistants pour stocker les données des applications, notamment les bases de données. Cela garantit que les données sont conservées même en cas de redémarrage ou de mise à jour des pods.

## PersistentVolume (PV) et PersistentVolumeClaim (PVC)

Les PersistentVolumes (PV) sont des ressources dans Kubernetes qui représentent des volumes de stockage persistants, tels que des disques sur un serveur ou des volumes cloud. Les PersistentVolumeClaims (PVC) sont des demandes de stockage émises par les utilisateurs pour obtenir un accès au stockage persistant. Un PVC spécifie les caractéristiques requises du stockage, telles que la taille et le mode d'accès, et Kubernetes trouve un PV correspondant pour satisfaire la demande.

## Stockage Dynamique

Le stockage dynamique est une fonctionnalité de Kubernetes qui permet la création automatique de PersistentVolumes en réponse à des PersistentVolumeClaims. Avec le stockage dynamique, les administrateurs de cluster n'ont pas besoin de provisionner manuellement des volumes de stockage avant que les utilisateurs ne demandent du stockage persistant. Cela simplifie grandement la gestion du stockage dans un cluster Kubernetes.

## Utilisation dans les Déploiements

Une fois qu'un PersistentVolume a été provisionné et qu'un PersistentVolumeClaim a été émis pour l'obtenir, un déploiement Kubernetes peut utiliser le PVC pour monter le volume dans les conteneurs des pods. Les applications peuvent ensuite écrire et lire des données sur le volume monté comme si c'était un système de fichiers local.

## Exemple d'Utilisation

Voici un exemple de spécification de PVC dans Kubernetes :

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
      storage: 10Gi
```

Ce PVC demande un volume de stockage persistant d'au moins 10 gigaoctets avec un mode d'accès en lecture/écriture.

## Conclusion

L'approvisionnement des bases de données persistantes dans Kubernetes est un aspect crucial de la gestion des applications étatiques. En utilisant des PersistentVolumes et des PersistentVolumeClaims, combinés avec le stockage dynamique, vous pouvez garantir que vos données sont sécurisées et disponibles même en cas de défaillance des pods ou des nœuds.

