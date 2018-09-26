---
title: Configurar un grupo de disponibilidad SQL Server Always On en contenedores de Docker en Kubernetes | Microsoft Docs
description: Este tutorial muestra cómo implementar un servidor de SQL Server siempre en el grupo de disponibilidad con Kubernetes en Azure Container Service.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: tutorial
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux,mvc
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6d21866f3f7004dff1ea86ca4f608580a79ab754
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049365"
---
# <a name="configure-a-sql-server-always-on-availability-group-on-docker-containers-in-kubernetes-with-azure-kubernetes-service-aks"></a>Configurar un grupo de disponibilidad SQL Server Always On en contenedores de Docker en Kubernetes con Azure Kubernetes Service (AKS)

Este tutorial muestra cómo configurar una instancia de SQL Server de alta disponibilidad en un contenedor de AKS. También puede [implementar un contenedor de SQL Server en Kubernetes](tutorial-sql-server-containers-kubernetes.md). Para comparar las dos soluciones diferentes de Kubernetes, consulte [alta disponibilidad para los contenedores de SQL Server](sql-server-linux-container-ha-overview.md).

En este tutorial, obtendrá información sobre cómo:  

> [!div class="checklist"]
> * Crear almacenamiento
> * Implementar el operador de SQL Server en un clúster de Kubernetes 
> * Cree los secretos de Kubernetes
> * Implementar instancias de SQL Server y los agentes de mantenimiento
> * Conectarse a la réplica principal
> * Agregar una base de datos al grupo de disponibilidad

Este tutorial muestra la arquitectura de [Azure Kubernetes Service (AKS)](http://docs.microsoft.com/azure/aks/). Si no tiene una suscripción de Azure, cree un [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de comenzar.

Este diagrama representa la solución que se realiza en este tutorial:

![clúster de kubernetes ag](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

### <a name="deployment-methodology-for-kubernetes"></a>Metodología de implementación de Kubernetes

Algunos de los pasos descritos en este artículo creación un manifiesto y, a continuación, implementación el manifiesto en el clúster. El manifiesto es un archivo .yaml con la descripción de los objetos de Kubernetes que se implementan.

Los archivos .yaml en este ejemplo están disponibles en [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability).

Los objetos incluyen el almacenamiento, operadores, pods, contenedores y servicios.

## <a name="prerequisites"></a>Requisitos previos

* Estar familiarizado con estas tecnologías

  * [Kubernetes](http://kubernetes.io) versión 1.8
  * [Azure Kubernetes Service (AKS)](http://docs.microsoft.com/azure/aks/)
  * [SQL Server en Docker](quickstart-install-connect-docker.md)
  * [Grupo de disponibilidad de SQL Server Always On](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

* Un clúster de Kubernetes con cuatro nodos.

  Para obtener instrucciones, consulte [Tutorial: implementar un clúster de Azure Kubernetes Service (AKS)](http://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster).

* Instalar [ `kubectl` ](https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#install-the-kubectl-cli).

## <a name="configuration-and-deployment-procedures"></a>Procedimientos de configuración e implementación

El tutorial mostrará cómo aplicar los archivos .yaml en el clúster de Kubernetes.

## <a name="create-the-secrets"></a>Cree los secretos

Para crear los secretos de Kubernetes para almacenar las contraseñas para la cuenta de SA de SQL Server y la clave maestra de SQL Server, ejecute el siguiente comando.

```azurecli
kubectl create secret generic sql-secrets --from-literal=sapassword="MyC0m9l&xP@ssw0rd" --from-literal=masterkeypassword="MyC0m9l&xP@ssw0rd2"
```

En un entorno de producción, utilice una contraseña diferente y compleja.

## <a name="deploy-the-operator"></a>Implementar el operador

Un operador de Kubernetes instancias de SQL Server implementa y configura el grupo de disponibilidad del clúster de Kubernetes. 

Vea un operador de ejemplo de [`operator.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/operator.yaml)

Descargar `operator.yaml` desde [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/)

Implementar el operador como una réplica de implementación de Kubernetes.

Para implementar el operador:

Implementar el operador con el `kubectl apply` comando.

```azurecli
kubectl apply -f operator.yaml
```

## <a name="create-the-sql-server-ag-deployment"></a>Crear la implementación de grupos de disponibilidad de SQL Server

El paso siguiente crea las instancias de SQL Server y el grupo de disponibilidad en una implementación de Kubernetes. Después de aplicar esta implementación en el clúster, el operador implementará las instancias de SQL Server como contenedores de Docker. Esta implementación dará como resultado tres StatefulSets con un pod. Cada pod incluirá dos contenedores:

* Instancia de SQL Server según la `mssql-server` imagen
* Supervisor de alta disponibilidad

Además, describe la implementación de un servicio de equilibrador de carga para el agente de escucha del grupo de disponibilidad

Para implementar mssql-server:

1. Copia [sqlserver.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/sqlserver.yaml) a su equipo.
2. Actualización `sqlserver.yaml` para su entorno.


Para implementar las instancias de SQL Server y crear el grupo de disponibilidad, ejecute el siguiente comando.

```azurecli
kubectl apply -f sqlserver.yaml
```

## <a name="deploy-ag-services"></a>Servicios de implementación AG

Creación de servicios de equilibrador de carga para las llamadas directas a las réplicas del grupo de disponibilidad del clúster de Kubernetes.

[AG services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files) crea cuatro servicios.

* AG1 principal se conecta a la réplica principal.
* sincronización de base de datos secundaria AG1 se conecta a una réplica secundaria sincrónica.
* AG1-async-base de datos secundaria se conecta a una réplica secundaria asincrónica.
* configuración de base de datos secundaria AG1 se conecta a una réplica de solo configuración. 

  >[!NOTE]
  >Estos servicios de equilibrador de carga se proporcionan como ejemplos. En este tutorial no es de solo configuración de réplica.


Implementar los servicios de equilibrador de carga para que puedan conectarse al grupo de disponibilidad.

Para implementar los servicios, ejecute el siguiente comando.

```azurecli
kubectl apply -f ag-services.yaml
```

### <a name="monitor-the-deployment"></a>Supervisar la implementación

Puede usar [panel de Kubernetes con Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/kubernetes-dashboard) para supervisar la implementación. 

Use `az aks browse` para iniciar el panel. 

Después de la implementación, se puede actualizar solo AG pertenencia lista y post-init script T-SQL. No se puede actualizar otras propiedades, se debe eliminar y volver a crear el recurso. Las credenciales de los usuarios generado automáticamente se pueden girar mediante un `mssql-server-k8s-rotate-creds` trabajo.

## <a name="connect-to-the-sql-server-instance-hosting-the-primary-replica"></a>Conéctese a la instancia de SQL Server que hospeda la réplica principal

El `ag-services.yaml` describe un nombre de servicio de Kubernetes `ag1-primary`. `ag1-primary` crea un equilibrador de carga que apuntan a la instancia de SQL Server que hospeda la réplica principal. Usar la dirección IP externa del servicio como servidor de destino, `sa` cuenta de identificación y la contraseña que creó anteriormente en el `mssql secret` la contraseña.

Use `kubectl get services` para obtener esta dirección IP.

Por ejemplo:

![Obtener el ejemplo de servicio](media\tutorial-sql-server-ag-containers-kubernetes\KubernetesGetServices.png)

En la imagen anterior, `ag1-primary` servicio tiene una dirección IP externa de `104.42-50.138`. 

Para conectarse a SQL Server con la autenticación de SQL, use la `sa` cuenta, el valor de `sapassword` desde el secreto que creó y esta dirección IP.

Por ejemplo:

```cmd
sqlcmd -S 104.42.50.138 -U sa -P "MyC0m9l&xP@ssw0rd"
```

![Conectar con sqlcmd](./media/tutorial-sql-server-ag-containers-kubernetes/sqlcmdConnect.png)

También se puede conectar con [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md).

Para comprobar la conexión, a la instancia de SQL Server que hospeda la réplica principal, ejecute la siguiente consulta:

```sql
SELECT @@SERVERNAME;
```

La consulta devuelve el nombre de la instancia de SQL Server que hospeda la réplica principal.

En este momento, el clúster de Kubernetes tiene tres instancias de SQL Server en contenedores de docker. Un grupo de disponibilidad abarca las tres instancias de SQL Server, pero ninguna base de datos está en el grupo de disponibilidad. El siguiente paso es agregar una base de datos al grupo de disponibilidad.

## <a name="add-a-database-to-the-availability-group"></a>Agregar una base de datos al grupo de disponibilidad

Para agregar una base de datos al grupo de disponibilidad:

1. Crear una base de datos

  ```sql
  CREATE DATABASE [DemoDB]
  ```

1. Realizar copia de seguridad de la base de datos para iniciar la cadena de registro de transacciones completo

  ```sql
  BACKUP DATABASE [DemoDB] 
  TO  DISK = N'/var/opt/mssql/data/DemoDB.bak' 
    WITH NOFORMAT, 
    NOINIT,  
    NAME = N'DemoDB-Full Database Backup', 
    SKIP, 
    NOREWIND, 
    NOUNLOAD,  
    STATS = 10;
  GO
  ```

1. Agregar la base de datos al grupo de disponibilidad

  ```sql
  ALTER AVAILABILITY GROUP ag1 ADD DATABASE [DemoDB]; 
  ```

La réplica se configura automáticamente con el modo de propagación automática, por lo que el grupo de disponibilidad propaga la base de datos en las réplicas secundarias.

En SQL Server Management Studio, puede conectarse a la réplica principal y ver el grupo de disponibilidad en el panel.

El ejemplo siguiente muestra el grupo de disponibilidad con réplicas en tres nodos configurados en el panel.

![Panel de AG1](./media/tutorial-sql-server-ag-containers-kubernetes/ssms_AG1.png)

## <a name="verify-failure-and-recovery"></a>Compruebe el error y recuperación

Para comprobar la conmutación por error y la detección de errores puede eliminar el pod que hospeda la réplica principal. Kubernetes se elige una nueva réplica principal y redirigir el agente de escucha. A continuación, volverá a crear el pod eliminado. 

Para demostrar este proceso, realice los pasos siguientes:

1. Lista de lo pod que ejecuta SQL Server.

   ```azurecli
   kubectl get pods
   ```

2. Identifique el pod de la réplica principal.

   Una conexión a la réplica principal utilizando la dirección IP y la consulta externa `@@servername` o use `kubectl` para obtener el pod adecuado. Este comando devolverá el nombre del pod que incluye el contenedor que se ejecuta la réplica principal del grupo de disponibilidad:

   ```azurecli
   kubectl get pods --selector="role.ag.mssql.microsoft.com/ag1"="primary" --output=jsonpath={.items..metadata.name}
   ```

3. Elimine el pod.

   ```azurecli
   kubectl delete pod <podName>
   ```

Reemplace `<podName>` con el valor devuelto desde el paso anterior para el nombre del pod. 

Kubernetes automáticamente conmuta por error a una de las réplicas secundarias de sincronización disponibles, así como el pod eliminado se vuelve a crear.

## <a name="clean-up-resources"></a>Limpiar recursos

Cuando ya no necesite, elimine el grupo de recursos y todos los recursos relacionados. Ejecute el siguiente comando:
>[!WARNING]
>Este comando elimina completamente todo el contenido del grupo de recursos. Ninguno de los componentes del clúster de Kubernetes estarán disponible después de eliminar el grupo de recursos.

```azurecli
az group delete --name <MyResourceGroup>
```

Para ejecutar el comando anterior, reemplace `<MyResourceGroup>` con el nombre del grupo de recursos. 

Azure elimina el grupo de recursos.

## <a name="summary"></a>Resumen

En este tutorial, ha aprendido cómo:  

> [!div class="checklist"]
> * Crear almacenamiento
> * Implementar el operador de SQL Server en un clúster de Kubernetes 
> * Cree los secretos de Kubernetes
> * Implementar instancias de SQL Server y los agentes de mantenimiento
> * Conectarse a la réplica principal
> * Agregar una base de datos al grupo de disponibilidad

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
>[Introducción a Kubernetes](http://docs.microsoft.com/azure/aks/intro-kubernetes)
>[administrar SQL Server en Kubernetes](sql-server-linux-kubernetes-manage.md)