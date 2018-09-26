---
title: Implementar SQL Server Always On Availability Group en un clúster de Kubernetes
description: En este artículo se explica los parámetros para el SQL Server Kubernetes Always On grupo operador globales requisitos de disponibilidad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4d24cd2ab59e1a7959f5a8ac1c929ff2e5e8e54a
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049605"
---
# <a name="deploy-a-sql-server-always-on-availability-group-on-kubernetes-cluster"></a>Implementar un servidor SQL Server Always On Availability Group en un clúster de Kubernetes

## <a name="requirements"></a>Requisitos

- Un clúster de Kubernetes
- Kubernetes versión 1.11.0 o superior
- Cuatro o más nodos
- [kubectl](http://kubernetes.io/docs/tasks/tools/install-kubectl/).

  >[!NOTE]
  >Puede usar cualquier tipo de clúster de Kubernetes. Para crear un clúster de Kubernetes en Azure Kubernetes Service (AKS), consulte [crear un clúster de AKS](http://docs.microsoft.com/azure/aks/create-cluster.md).
  > El script siguiente crea un clúster de cuatro nodos de Kubernetes en Azure.
  >```azure-cli
  az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 4 --kubernetes-version 1.11.1
  >```

## <a name="steps"></a>Pasos

1. Configurar el almacenamiento

  En entornos de nube como Azure, configurar [volúmenes persistentes](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) para cada instancia de SQL Server.

  Para crear los volúmenes persistentes en Azure, consulte `pv.yaml` y `pvc.yaml` en [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates).

  Para crear el almacenamiento que se ejecute el siguiente comando:

  ```azurecli
  kubectl apply -f <pv.yaml>
  ```

1. Cree los secretos de Kubernetes para la contraseña de SA y la clave maestra.

  El ejemplo siguiente crea dos secretos. `sapassword` es la contraseña de SA y `masterkeypassword` es para la clave maestra. Antes de ejecutar este script de reemplazo `<MyC0mp13xP@55w04d!>` con una contraseña compleja diferente para cada secreto.

   ```azurecli
   kubectl create secret generic sql-secrets --from-literal='sapassword=<MyC0mp13xP@55w04d!>' --from-literal='masterkeypassword=<MyC0mp13xP@55w04d!>'
   ```

1. Configure e implemente el manifiesto de operador de SQL Server.

  Copie el operador de SQL Server `operator.yaml` de archivos de [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

  El `operator.yaml` archivo es el manifiest de implementación para el operador de Kubernetes.

  Para configurar el manifiesto, actualice el `operator.yaml` archivo para su entorno.

  Aplicar el manifiesto para el clúster de Kubernetes.

  ```azurecli
  kubectl apply -f operator.yaml
  ```

1. Implementar el recurso personalizado de SQL Server.

  Copie el manifiesto de SQL Server `sqlserver.yaml` desde [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

  Aplicar el manifiesto para el clúster de Kubernetes.

  ```azurecli
  kubectl apply -f sqlserver.yaml
  ```

Después de implementar el manifiesto de SQL Server, el operador implementa las instancias de SQL Server como los pods en contenedores.

Una vez finalizada la secuencia de comandos, el operador de Kubernetes creará el almacenamiento, las instancias de SQL Server, los servicios de equilibrador de carga. Puede supervisar la implementación con [panel de Kubernetes](http://docs.microsoft.com/azure/aks/kubernetes-dashboard).

Después de que Kubernetes crea los contenedores de SQL Server complete los pasos siguientes para agregar una base de datos al grupo de disponibilidad:

1. [Conectar](sql-server-linux-kubernetes-connect.md) a una instancia de SQL Server en el clúster.

1. Crear una base de datos.

1. Realizar copia de seguridad de la base de datos para iniciar la cadena de registros una completa.

1. Agregue la base de datos al grupo de disponibilidad.

Se crea el grupo de disponibilidad con propagación automática, por lo que SQL Server creará automáticamente las réplicas secundarias.

## <a name="next-steps"></a>Pasos siguientes

[Conectarse al grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-linux-kubernetes-connect.md)

[Administrar grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-linux-kubernetes-manage.md)

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)