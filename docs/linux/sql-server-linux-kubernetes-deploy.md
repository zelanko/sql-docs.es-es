---
title: Implementar un grupo de disponibilidad SQL Server Always On en un clúster de Kubernetes
description: En este artículo se explica los parámetros para el SQL Server Kubernetes Always On grupo operador globales requisitos de disponibilidad
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a4811c1f41c4c8b9a566dc13b3de713576b4980d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952626"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Implementar un grupo de disponibilidad SQL Server Always On en un clúster de Kubernetes

El ejemplo de este artículo implementa un grupo de disponibilidad SQL Server Always On en un clúster de Kubernetes con tres réplicas. Las réplicas secundarias están en modo de confirmación sincrónica.

En Kubernetes, la implementación incluye un operador de SQL Server, los contenedores de SQL Server y los carga servicios equilibrador. El operador organiza automáticamente el grupo de disponibilidad. Este artículo se explica cómo:

- Implementar el operador, los contenedores de SQL Server y servicios de equilibrio de carga.
- Conectarse al grupo de disponibilidad con los servicios.
- Agregar una base de datos al grupo de disponibilidad.

## <a name="requirements"></a>Requisitos

- Un clúster de Kubernetes de AKS con la versión más reciente
- Al menos tres nodos
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- El acceso a la [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) repositorio de GitHub

> [!NOTE]
> Puede usar cualquier tipo de clúster de Kubernetes. Para crear un clúster de Kubernetes en Azure Kubernetes Service (AKS), consulte [crear un clúster de AKS](https://docs.microsoft.com/azure/aks/create-cluster).
>
> Use la versión más reciente de Kubernetes. La versión específica depende de su suscripción y región. Consulte [versiones compatibles de Kubernetes en AKS](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions).  
>
> El script siguiente crea un clúster de cuatro nodos de Kubernetes en Azure. Antes de ejecutar el script de reemplazar `<latest version>` con la última versión disponible. Por ejemplo, `1.12.5`.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>Implementar el operador, los contenedores de SQL Server y servicios de equilibrio de carga

1. Crear un [espacio de nombres](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/).

      Este ejemplo usa un espacio de nombres denominado `ag1`. Ejecute el siguiente comando para crear el espacio de nombres.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      Todos los objetos que pertenecen a esta solución están en el `ag1` espacio de nombres.

1. Configure e implemente el manifiesto de operador de SQL Server.

      Copie el servidor SQL Server [ `operator.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) de archivos de [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      El `operator.yaml` archivo es el manifiesto de implementación para el operador de Kubernetes.
    
      Aplicar el manifiesto para el clúster de Kubernetes.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. Cree un secreto de Kubernetes con las contraseñas para el `sa` cuenta y la clave maestra de instancia de SQL Server.

      Crear el secreto con `kubectl`.
      
      En el ejemplo siguiente se crea un secreto llamado `sql-secrets` en el `ag1` espacio de nombres. El secreto almacena dos contraseñas:
      
      - `sapassword` almacena la contraseña de SQL Server `sa` cuenta.
      - `masterkeypassword` almacena la contraseña utilizada para crear la clave maestra de SQL Server. 
    
   Copie el script en el terminal. Reemplaza cada `<>` con una contraseña compleja y ejecute el script para crear el secreto.
    
   >[!NOTE]
   >No se puede usar la contraseña `&` o `` ` `` caracteres.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. Implementar el recurso personalizado de SQL Server.

      Copie el manifiesto de SQL Server [ `sqlserver.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) desde [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      >[!NOTE]
      >El `sqlserver.yaml` archivo describe los contenedores de SQL Server, las notificaciones de volumen persistente, los volúmenes persistentes y servicios de equilibrio de carga que son necesarios para cada instancia de SQL Server.
    
      Aplicar el manifiesto para el clúster de Kubernetes.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
La siguiente imagen muestra la aplicación correcta de `kubectl apply` en este ejemplo.

![crear sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

Después de aplicar el manifiesto de SQL Server, el operador implementa los contenedores de SQL Server.

Kubernetes coloca los contenedores de pods. Use `kubectl get pods --namespace ag1` para ver el estado de los pods. La siguiente imagen muestra la implementación de ejemplo, una vez implementados los pods de SQL Server. 

![compila los pods](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>Supervisar la implementación

Puede usar el [panel de Kubernetes con Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/kubernetes-dashboard) para supervisar la implementación.

Use `az aks browse` para iniciar el panel. 

## <a name="connect-to-the-availability-group-with-the-services"></a>Conectarse al grupo de disponibilidad con los servicios

El [ `ag-services.yaml` ](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) desde [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) ejemplo describe los servicios de equilibrio de carga que pueden conectarse a las réplicas del grupo de disponibilidad. 

- `ag1-primary` Proporciona un punto de conexión para conectarse a la réplica principal.
- `ag1-secondary` Proporciona un punto de conexión para conectarse a cualquier réplica secundaria.

Al aplicar el archivo de manifiesto, Kubernetes crea los servicios de equilibrio de carga para cada tipo de réplica. El servicio de equilibrio de carga incluye una dirección IP. Use esta dirección IP para conectar con el tipo de réplica que necesita.

Para implementar los servicios, ejecute el siguiente comando.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

Después de implementar los servicios, use `kubectl get services --namespace ag1` para identificar la dirección IP de los servicios.

Con la dirección IP, puede conectarse a la instancia de SQL Server que hospeda cada tipo de réplica.

Se muestra la siguiente imagen:

- La salida de `kubectl get services` del espacio de nombres `ag1`.

- Los servicios de equilibrio de carga que se crean para cada contenedor de SQL Server. Use estas direcciones IP como puntos de conexión para conectarse directamente a la instancia de SQL Server en el clúster.

- El `sqlcmd` conexión a la réplica principal, con el `sa` cuenta a través del extremo del equilibrador de carga.

![Conectar](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>Agregar una base de datos al grupo de disponibilidad

>[!NOTE]
>En este momento, SQL Server Management Studio no puede agregar una base de datos a un grupo de disponibilidad. Usar Transact-SQL.

Después de que Kubernetes crea los contenedores de SQL Server, complete los pasos siguientes para agregar una base de datos al grupo de disponibilidad.

1. [Conectar](sql-server-linux-kubernetes-connect.md) a una instancia de SQL Server en el clúster.

1. Crear una base de datos.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. Realizar copia de seguridad de la base de datos para iniciar la cadena de registros una completa.

      ```sql
      USE MASTER
      GO
      BACKUP DATABASE [demodb] 
      TO DISK = N'/var/opt/mssql/data/demodb.bak'
      ```

1. Agregue la base de datos al grupo de disponibilidad.

      ```sql
      ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [demodb]
      ```
    
Se crea el grupo de disponibilidad con propagación automática para que SQL Server crea automáticamente las réplicas secundarias.

Puede ver el estado del grupo de disponibilidad desde el panel grupos de disponibilidad de SQL Server Management Studio.

![dashboard](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>Pasos siguientes

- [Conectarse a un grupo de disponibilidad de SQL Server en un clúster de Kubernetes](sql-server-linux-kubernetes-connect.md)

- [Administrar un grupo de disponibilidad de SQL Server en un clúster de Kubernetes](sql-server-linux-kubernetes-manage.md)

- [SQL Server admite grupos de disponibilidad en los contenedores de un clúster de Kubernetes](sql-server-ag-kubernetes.md)
