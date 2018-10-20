---
title: Administrar un grupo de disponibilidad SQL Server Always On Kubernetes
description: En este artículo se explica cómo administrar un SQL Server grupo de disponibilidad AlwaysOn en Kubernetes.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 09/24/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1760256333abad2c6ae32d0aa2a94e1deaebd551
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356366"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Administrar SQL Server Always On Kubernetes del grupo de disponibilidad

Para administrar un grupo de disponibilidad AlwaysOn en Kubernetes, cree un manifiesto y aplicarla al clúster. El manifiesto es un `.yaml` archivo.  

Los ejemplos de este artículo se aplican a todos los clúster de Kubernetes. Los escenarios en los siguientes ejemplos se aplican a un clúster en Azure Kubernetes Service.

Ver un ejemplo de la implementación completa en [implementar un SQL Server grupo de disponibilidad AlwaysOn en un clúster de Kubernetes](sql-server-linux-kubernetes-deploy.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Conmutar por error - grupo de disponibilidad de SQL Server en Kubernetes

Para mover una réplica principal a otro nodo en un grupo de disponibilidad o conmutación por error, complete los pasos siguientes:

1. Define un trabajo en un archivo de manifiesto.

  [`failover.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/failover.yaml) -en el [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) repositorio de github describe un trabajo de conmutación por error.

  Copie el archivo de manifiesto en la administración de terminal.

  Actualice el archivo para su entorno.

  - Reemplace `<containerName>` con el nombre del destino del grupo de disponibilidad esperada.
  - Si el grupo de disponibilidad no está en el `ag1` espacio de nombres, reemplace `ag1` con el espacio de nombres.

  Este archivo define un trabajo de conmutación por error con el nombre `manual-failover`.

1. Para implementar el trabajo, use `kubectl apply`. El script siguiente implementa el trabajo.

  ```azurecli
  kubectl apply -f failover.yaml
  ```

  Después de implementa el trabajo, kubernetes, con el operador de SQL Server, realiza las siguientes tareas:
  
  - Degrada la réplica principal a secundario
  
  - Promueve la réplica a principal especificada
  
  Después de aplicar el archivo de manifiesto, Kubernetes ejecuta el trabajo. El trabajo hace que el supervisor de seleccionar un nuevo líder y mueve la réplica principal a la instancia de SQL Server de la directriz.

1. Compruebe que se complete el trabajo.
  
  Después de Kubernetes ejecuta el trabajo, puede revisar el registro.
  
  El ejemplo siguiente devuelve el estado del trabajo denominado `manual-failover`.

  ```azurecli
  kubectl describe jobs/manual-failover -–namespace ag1
  ```

1. Eliminar el trabajo de conmutación por error manual. 

  >[!IMPORTANT]
  >Debe eliminar manualmente el trabajo antes de emitir otra conmutación por error manual.
  > 
  >El objeto de trabajo en Kubernetes permanece después de la finalización para que pueda ver su estado. Deberá eliminar manualmente los trabajos antiguos después de tener en cuenta su estado. La eliminación del trabajo, también elimina los registros de Kubernetes. Si no elimina el trabajo, se producirá un error en los trabajos futuros de conmutación por error a menos que cambie el nombre del trabajo y el selector de pod. Para obtener más información, consulte [trabajos: se ejecutan hasta completarse](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

  El siguiente comando elimina el trabajo.

  ```azurecli
  kubectl delete jobs manual-failover -–namespace ag1
  ```

## <a name="rotate-credentials"></a>Rotar las credenciales

Rotar las credenciales para restablecer la contraseña de SQL Server `sa` cuenta y el servidor SQL [clave maestra de servicio](../relational-databases/security/encryption/service-master-key.md). 

Para completar esta tarea, creará nuevos secretos en el clúster de Kubernetes y, a continuación, crear un trabajo para girar las credenciales.

Antes de rotar las credenciales, asegúrese de un secreto nuevo para la contraseña y la clave maestra.

El script siguiente crea un secreto llamado `new-sql-secrets`. Antes de ejecutar el script, reemplace `<>` con contraseñas complejas para la `sapassword` y `masterkeypassword`. Utilice contraseñas diferentes para cada valor correspondiente.

```azurecli
kubectl create secret generic new-sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
```

Complete los pasos siguientes para cada instancia de SQL Server que necesita la clave maestra o `sa` contraseña.

1. Copia [ `rotate-creds.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) para la administración de terminal.

  [`rotate-creds.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/rotate-creds.yaml) en el [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/) repositorio de github es un ejemplo de un manifiesto para este trabajo.

  Antes de aplicar este manifiesto, actualice el manifiesto para su entorno. Revisar y cambiar la configuración siguiente, según sea necesario.

  - Compruebe el espacio de nombres. Actualice si es necesario. El siguiente ejemplo en un manifiesto que se aplica a un espacio de nombres denominado `ag1`.

    ```yaml
    metadata:
      name: rotate-creds
      namespace: ag1
    ```

  - Compruebe el nombre de la instancia de SQL Server. Actualice si es necesario. El ejemplo siguiente en una especificación de manifiesto que se aplica a una instancia de SQL Server denominada `mssql1`.

    ```yaml
    env:
      - name: MSSQL_K8S_SQL_SERVER_NAME
        value: mssql1
    ```

  Guarde el archivo de manifiesto actualizado a la estación de trabajo.

1. Use `kubectl` para implementar el trabajo.

  ```azurecli
  kubectl apply -f rotate-creds.yaml --namespace ag1
  ```

  Kubernetes actualiza la clave maestra y `sa` contraseña para una instancia de SQL Server en un grupo de disponibilidad.

1. Compruebe que se ha completado el trabajo. Ejecute el siguiente comando: para comprobar que se ha completado el trabajo, ejecute 

  ```azcli
  kubectl describe job rotate-creds --namespace ag1
  ```

  Después de que el trabajo tiene éxito, la clave maestra y `sa` se actualizan la contraseña para una instancia de SQL Server.


1. Antes de volver a ejecutar el trabajo, eliminar el trabajo. Cada nombre de trabajo debe ser único.

  ```azurecli
  kubectl delete job rotate-creds --namespace ag1
  ```

Para establecer el mismo `sa` contraseña para todas las instancias de SQL Server, repita los pasos anteriores para cada instancia de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

[Tener acceso al panel de Kubernetes con Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
