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
ms.openlocfilehash: 8ad318c0f0967f26f5cfdf2c5ad9af2d94323bf0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622843"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Administrar SQL Server Always On Kubernetes del grupo de disponibilidad

Para administrar un grupo de disponibilidad AlwaysOn en Kubernetes, cree un manifiesto y aplicarla al clúster. El manifiesto es un `.yaml` archivo.  

Los ejemplos de este artículo se aplican a todos los clúster de Kubernetes. Los escenarios en los siguientes ejemplos se aplican a un clúster en Azure Kubernetes Service.

Ver un ejemplo de la de la implementación to-end en [este tutorial](tutorial-sql-server-ag-kubernetes.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Conmutar por error - grupo de disponibilidad de SQL Server en Kubernetes

Para conmutar por error una réplica principal del grupo de disponibilidad a otro nodo en Kubernetes, use un trabajo. Este artículo identifican las variables de entorno para este trabajo.

El siguiente ejemplo de un archivo de manifiesto describe un trabajo para conmutar por error manualmente el trabajo de un grupo de disponibilidad en una réplica de Kubernetes. Copie el contenido del ejemplo en un nuevo archivo denominado `failover.yaml`.

[failover.yaml](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates/failover.yaml)

Para implementar el trabajo, use `Kubectl`.

```azurecli
kubectl apply -f failover.yaml
```

Al aplicar el archivo de manifiesto, Kubernetes ejecuta el trabajo. Cuando se ejecuta el trabajo, el supervisor elige a un nuevo líder y mueve la réplica principal a la instancia de SQL Server de la directriz.

Después de ejecutar el trabajo, eliminarlo. El objeto de trabajo en Kubernetes permanece después de la finalización para que pueda ver su estado. Tendrá que eliminar manualmente los trabajos antiguos después de tener en cuenta su estado. La eliminación del trabajo, también elimina los registros de Kubernetes. Si no se elimina el trabajo, se producirá un error en los trabajos futuros de conmutación por error a menos que cambie el nombre del trabajo y el selector de pod. Para obtener más información, consulte [trabajos: se ejecutan hasta completarse](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

## <a name="rotate-credentials"></a>Rotar las credenciales

Girar las credenciales para actualizar la SA y la clave maestra.

Copia el [creds.yaml girar](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script) localmente usar `kubectl` para aplicarlo a su clúster.

```azurecli
kubectl apply -f rotate-creds.yaml
```

## <a name="next-steps"></a>Pasos siguientes

[Tener acceso al panel de Kubernetes con Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
