---
title: Administración de un grupo de disponibilidad AlwaysOn de SQL Server en Kubernetes
description: En este artículo se explica cómo administrar un grupo de disponibilidad AlwaysOn de SQL Server en Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 893e502c35ae33ce6ff87efd88049db97a40f875
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952540"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Administración de un grupo de disponibilidad AlwaysOn de SQL Server en Kubernetes

Para administrar un grupo de disponibilidad AlwaysOn en Kubernetes, cree un manifiesto y aplíquelo al clúster. El manifiesto es un archivo `.yaml`.  

Los ejemplos de este artículo se aplican a todos los clústeres de Kubernetes. Los escenarios de estos ejemplos se aplican a un clúster de Azure Kubernetes Service.

Vea un ejemplo de la implementación completa en [Implementación de un grupo de disponibilidad AlwaysOn de SQL Server en un clúster de Kubernetes](sql-server-linux-kubernetes-deploy.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Conmutar por error: grupo de disponibilidad de SQL Server en Kubernetes

Para conmutar por error o trasladar una réplica principal a otro nodo de un grupo de disponibilidad, siga estos pasos:

1. Defina un trabajo en un archivo de manifiesto.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml): en el repositorio de github [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) se describe un trabajo de conmutación por error.

  Copie el archivo de manifiesto en el terminal de administración.

  Actualice el archivo del entorno.

  - Reemplace `<containerName>` por el nombre del pod (por ejemplo, mssql2-0) del destino de grupo de disponibilidad esperado.
  - Si el grupo de disponibilidad no está en el espacio de nombres `ag1`, reemplace `ag1` por el espacio de nombres.

  Este archivo define un trabajo de conmutación por error denominado `manual-failover`.

1. Para implementar el trabajo, use `kubectl apply`. El siguiente script implementa el trabajo.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  Una vez implementado el trabajo, Kubernetes, con el operador de SQL Server, realiza las tareas siguientes:
  
  - Degrada la réplica principal a secundaria
  
  - Promueve la réplica especificada a principal
  
  Después de aplicar el archivo de manifiesto, Kubernetes ejecuta el trabajo. El trabajo hace que el supervisor seleccione un nuevo líder y mueve la réplica principal a la instancia de SQL Server del líder.

1. Compruebe que el trabajo se ha completado.
  
  Después de que Kubernetes ejecute el trabajo, puede revisar el registro.
  
  En el ejemplo siguiente se devuelve el estado del trabajo denominado `manual-failover`.

  ```azurecli
  kubectl describe jobs/manual-failover --namespace ag1
  ```

1. Elimine el trabajo de conmutación por error manual. 

  >[!IMPORTANT]
  >Debe eliminar el trabajo manualmente para poder emitir otra conmutación por error manual.
  > 
  >El objeto de trabajo de Kubernetes permanece después de la finalización para que pueda ver su estado. Debe eliminar manualmente los trabajos antiguos después de anotar su estado. Al eliminar el trabajo también se eliminan los registros de Kubernetes. Si no elimina el trabajo, se produce un error en los trabajos de conmutación por error futuros, a menos que cambie el nombre del trabajo y el selector del pod. Para obtener más información, vea [Trabajos: ejecución hasta su finalización](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

  El comando siguiente elimina el trabajo.

  ```azurecli
  kubectl delete jobs manual-failover --namespace ag1
  ```

## <a name="rotate-credentials"></a>Rotación de las credenciales

Rote las credenciales para restablecer la contraseña de la cuenta de `sa` de SQL Server y la [clave maestra de servicio](../relational-databases/security/encryption/service-master-key.md) de SQL Server. 

Para completar esta tarea, cree nuevos secretos en el clúster de Kubernetes y luego cree un trabajo para rotar las credenciales.

Antes de rotar las credenciales, cree un nuevo secreto para la contraseña y la clave maestra.

El siguiente script crea un secreto denominado `new-sql-secrets`. Antes de ejecutar el script, reemplace `<>` por contraseñas complejas para `sapassword` y `masterkeypassword`. Use contraseñas diferentes para cada valor respectivo.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

Realice los pasos siguientes para cada instancia de SQL Server que necesite la clave maestra o la contraseña de `sa`.

1. Copie [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) en el terminal de administración.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) en el repositorio de github [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) es un ejemplo de manifiesto para este trabajo.

  Antes de aplicar este manifiesto, actualice el manifiesto del entorno. Revise y cambie la configuración siguiente, según sea necesario.

  - Compruebe el espacio de nombres. Actualice en caso necesario. El siguiente ejemplo de manifiesto se aplica a un espacio de nombres denominado `ag1`.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - Compruebe el nombre de la instancia de SQL Server. Actualice en caso necesario. El ejemplo siguiente de una especificación de manifiesto se aplica a una instancia de SQL Server denominada `mssql1`.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  Guarde el archivo de manifiesto actualizado en la estación de trabajo.

1. Use `kubectl` para implementar el trabajo.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes actualiza la clave maestra y la contraseña de `sa` para una instancia de SQL Server de un grupo de disponibilidad.

1. Compruebe que el trabajo se ha completado. Ejecute el siguiente comando: Para comprobar que el trabajo se ha completado, ejecute 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  Una vez que el trabajo se realiza correctamente, se actualizan la clave maestra y la contraseña de `sa` para una instancia de SQL Server.


1. Antes de volver a ejecutar el trabajo, elimine el trabajo. Cada nombre de trabajo debe ser único.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

Para establecer la misma contraseña de `sa` para todas las instancias de SQL Server, repita los pasos anteriores para cada instancia de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

[Acceso al panel de Kubernetes con Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
