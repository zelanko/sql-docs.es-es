---
title: Implementación de un grupo de disponibilidad Always On de SQL Server en un clúster de Kubernetes
description: En este artículo se explican los parámetros de los requisitos globales del operador de grupo de disponibilidad Always On de Kubernetes de SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/02/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a4811c1f41c4c8b9a566dc13b3de713576b4980d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952626"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-a-kubernetes-cluster"></a>Implementación de un grupo de disponibilidad Always On de SQL Server en un clúster de Kubernetes

En el ejemplo de este artículo se implementa un grupo de disponibilidad Always On de SQL Server en un clúster de Kubernetes con tres réplicas. Las réplicas secundarias están en el modo de confirmación sincrónica.

En Kubernetes, la implementación incluye un operador de SQL Server, los contenedores de SQL Server y los servicios del equilibrador de carga. El operador organiza el grupo de disponibilidad automáticamente. En este artículo se explica lo siguiente:

- Implementación del operador, los contenedores de SQL Server y los servicios de equilibrio de carga.
- Conexión al grupo de disponibilidad con los servicios.
- Adición de una base de datos al grupo de disponibilidad.

## <a name="requirements"></a>Requisitos

- Un clúster de Kubernetes de AKS con la versión más reciente
- Al menos tres nodos
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Acceso al repositorio de GitHub [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files)

> [!NOTE]
> Puede usar cualquier tipo de clúster de Kubernetes. Para crear un clúster de Kubernetes en Azure Kubernetes Service (AKS), consulte [Creación de un clúster de AKS](https://docs.microsoft.com/azure/aks/create-cluster).
>
> Use la versión más reciente de Kubernetes. La versión específica depende de su suscripción y región. Consulte [Versiones de Kubernetes compatibles en AKS](https://docs.microsoft.com/en-us/azure/aks/supported-kubernetes-versions).  
>
> El siguiente script crea un clúster de Kubernetes de cuatro nodos en Azure. Antes de ejecutar el script, reemplace `<latest version>` por la última versión disponible. Por ejemplo, `1.12.5`.
>
> ```azure-cli
> az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version <latest version> --generate-ssh-keys
> ```

## <a name="deploy-the-operator-sql-server-containers-and-load-balancing-services"></a>Implementación del operador, los contenedores de SQL Server y los servicios de equilibrio de carga

1. Cree un [espacio de nombres](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/).

      En este ejemplo se usa un espacio de nombres denominado `ag1`. Ejecute el siguiente comando para crear el espacio de nombres.
    
      ```azurecli
      kubectl create namespace ag1
      ```
    
      Todos los objetos que pertenecen a esta solución se encuentran en el espacio de nombres `ag1`.

1. Configure e implemente el manifiesto del operador de SQL Server.

      Copie el archivo [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml) de SQL Server de [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      El archivo `operator.yaml` es el manifiesto de implementación del operador de Kubernetes.
    
      Aplique el manifiesto al clúster de Kubernetes.
    
      ```azurecli
      kubectl apply -f operator.yaml --namespace ag1
      ```
    
1. Cree un secreto para Kubernetes con las contraseñas de la cuenta `sa` y la clave maestra de la instancia de SQL Server.

      Cree el secreto con `kubectl`.
      
      En el siguiente ejemplo se crea un secreto denominado `sql-secrets` en el espacio de nombres `ag1`. El secreto almacena dos contraseñas:
      
      - `sapassword` almacena la contraseña de la cuenta `sa` de SQL Server.
      - `masterkeypassword` almacena la contraseña usada para crear la clave maestra de SQL Server. 
    
   Copie el script en el terminal. Reemplace cada `<>` por una contraseña compleja y ejecute el script para crear el secreto.
    
   >[!NOTE]
   >La contraseña no puede usar los caracteres `&` ni `` ` ``.
    
   ```azurecli
   kubectl create secret generic sql-secrets --from-literal=sapassword="<>" --from-literal=masterkeypassword="<>"  --namespace ag1
   ```

1. Implemente el recurso personalizado de SQL Server.

      Copie el manifiesto [`sqlserver.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) de SQL Server de [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).
    
      >[!NOTE]
      >El archivo `sqlserver.yaml` describe los contenedores de SQL Server, las notificaciones de volumen persistentes, los volúmenes persistentes y los servicios de equilibrio de carga necesarios para cada instancia de SQL Server.
    
      Aplique el manifiesto al clúster de Kubernetes.
    
      ```azurecli
      kubectl apply -f sqlserver.yaml --namespace ag1
      ```
      
En la imagen siguiente se muestra la aplicación correcta de `kubectl apply` para este ejemplo.

![Creación de sqlservers](./media/sql-server-linux-kubernetes-deploy/create-sqlservers.png)

Después de aplicar el manifiesto de SQL Server, el operador implementa los contenedores de SQL Server.

Kubernetes coloca los contenedores en pods. Use `kubectl get pods --namespace ag1` para ver el estado de los pods. En la imagen siguiente se muestra la implementación de ejemplo una vez que se han implementado los pods de SQL Server. 

![Compilación de los pods](./media/sql-server-linux-kubernetes-deploy/builtpods.png)

### <a name="monitor-the-deployment"></a>Supervisión de la implementación

Puede usar el [panel de Kubernetes con Azure Kubernetes Service](https://docs.microsoft.com/azure/aks/kubernetes-dashboard) para supervisar la implementación.

Use `az aks browse` para iniciar el panel. 

## <a name="connect-to-the-availability-group-with-the-services"></a>Conexión al grupo de disponibilidad con los servicios

El archivo [`ag-services.yaml`](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) del ejemplo [sql-server-samples](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) describe los servicios de equilibrio de carga que se pueden conectar con réplicas del grupo de disponibilidad. 

- `ag1-primary` proporciona un punto de conexión para conectarse a la réplica principal.
- `ag1-secondary` proporciona un punto de conexión para conectarse a cualquier réplica secundaria.

Al aplicar el archivo de manifiesto, Kubernetes crea los servicios de equilibrio de carga de cada tipo de réplica. El servicio de equilibrio de carga incluye una dirección IP. Use esta dirección IP para conectarse al tipo de réplica que necesite.

Para implementar los servicios, ejecute el siguiente comando.

```azurecli
kubectl apply -f ag-services.yaml --namespace ag1
```

Después de implementar los servicios, use `kubectl get services --namespace ag1` para identificar la dirección IP de los servicios.

Con la dirección IP, puede conectarse a la instancia de SQL Server que hospeda cada tipo de réplica.

En la imagen siguiente se muestra:

- La salida de `kubectl get services` del espacio de nombres `ag1`.

- Los servicios de equilibrio de carga que se crean para cada contenedor de SQL Server. Use estas direcciones IP como puntos de conexión para conectarse directamente a las instancias de SQL Server en el clúster.

- La conexión `sqlcmd` a la réplica principal, con la cuenta `sa` mediante el punto de conexión del equilibrador de carga.

![Conectar](./media/sql-server-linux-kubernetes-deploy/connect.png)

## <a name="add-a-database-to-the-availability-group"></a>Agregar una base de datos al grupo de disponibilidad

>[!NOTE]
>Actualmente, SQL Server Management Studio no puede agregar una base de datos a un grupo de disponibilidad. Use Transact-SQL.

Una vez que Kubernetes haya creado los contenedores de SQL Server, complete los pasos siguientes para agregar una base de datos al grupo de disponibilidad.

1. [Conéctese](sql-server-linux-kubernetes-connect.md) a una instancia de SQL Server en el clúster.

1. Crear una base de datos.

      ```sql
      CREATE DATABASE [demodb]
      ```

1. Haga una copia de seguridad completa de la base de datos para iniciar la cadena de registros.

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
    
El grupo de disponibilidad se crea con propagación automática, de modo que SQL Server cree automáticamente las réplicas secundarias.

Puede ver el estado del grupo de disponibilidad en el panel de grupos de disponibilidad de SQL Server Management Studio.

![panel](./media/sql-server-linux-kubernetes-deploy/dashboard.png)

## <a name="next-steps"></a>Pasos siguientes

- [Conexión a un grupo de disponibilidad de SQL Server en un clúster de Kubernetes](sql-server-linux-kubernetes-connect.md)

- [Administración de un grupo de disponibilidad de SQL Server en un clúster de Kubernetes](sql-server-linux-kubernetes-manage.md)

- [SQL Server admite grupos de disponibilidad en contenedores de un clúster de Kubernetes](sql-server-ag-kubernetes.md)
