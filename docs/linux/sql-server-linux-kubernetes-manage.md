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
ms.openlocfilehash: 7f713ed7dd5d0260df6441698371b33f94813d7e
ms.sourcegitcommit: 4832ae7557a142f361fbf0a4e2d85945dbf8fff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251982"
---
# <a name="manage-sql-server-always-on-availability-group-kubernetes"></a>Administrar SQL Server Always On Kubernetes del grupo de disponibilidad

Para administrar un grupo de disponibilidad AlwaysOn en Kubernetes, cree un manifiesto y aplicarla al clúster. El manifiesto es un `.yaml` archivo.  

Los ejemplos de este artículo se aplican a todos los clúster de Kubernetes. Los escenarios en los siguientes ejemplos se aplican a un clúster en Azure Kubernetes Service.

Ver un ejemplo de la implementación completa en [grupos de disponibilidad de Always On para los contenedores de SQL Server](sql-server-ag-kubernetes.md).

## <a name="fail-over---sql-server-availability-group-on-kubernetes"></a>Conmutar por error - grupo de disponibilidad de SQL Server en Kubernetes

Para conmutar por error una réplica principal del grupo de disponibilidad a otro nodo en Kubernetes, use un trabajo. Este artículo identifican las variables de entorno para este trabajo.

El siguiente archivo de manifiesto describe un trabajo para conmutar por error manualmente un grupo de disponibilidad. 

Copie el contenido del ejemplo en un nuevo archivo denominado `failover.yaml`.

[failover.yaml](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-deployment-script/templates/failover.yaml)

Para implementar el trabajo, use `Kubectl`.

```azurecli
kubectl apply -f failover.yaml
```

Después de aplicar el archivo de manifiesto, Kubernetes ejecuta el trabajo. El trabajo hace que el supervisor de elegir a un líder nuevo y mueve la réplica principal a la instancia de SQL Server de la directriz.

Después de ejecutar el trabajo, eliminarlo. El objeto de trabajo en Kubernetes permanece después de la finalización para que pueda ver su estado. Deberá eliminar manualmente los trabajos antiguos después de tener en cuenta su estado. La eliminación del trabajo, también elimina los registros de Kubernetes. Si no elimina el trabajo, se producirá un error en los trabajos futuros de conmutación por error a menos que cambie el nombre del trabajo y el selector de pod. Para obtener más información, consulte [trabajos: se ejecutan hasta completarse](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/).

## <a name="rotate-credentials"></a>Rotar las credenciales

Girar las credenciales para actualizar la SA y la clave maestra.

Copia el [creds.yaml girar](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-deployment-script) localmente usar `kubectl` para aplicarlo a su clúster.

```azurecli
kubectl apply -f rotate-creds.yaml
```

## <a name="next-steps"></a>Pasos siguientes

[Tener acceso al panel de Kubernetes con Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/kubernetes-dashboard)

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
