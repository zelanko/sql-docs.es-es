---
title: Alta disponibilidad para contenedores de SQL Server
description: En este artículo se presenta la alta disponibilidad para contenedores de SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: aa54849c16ea9dfb821404b553b1e9183b61d66a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077479"
---
# <a name="high-availability-for-sql-server-containers"></a>Alta disponibilidad para contenedores de SQL Server

Cree y administre las instancias de SQL Server de forma nativa en Kubernetes.

Implemente SQL Server en contenedores de Docker administrados por [Kubernetes](https://kubernetes.io/). En Kubernetes, un contenedor con una instancia de SQL Server se puede recuperar automáticamente en caso de error en un nodo de clúster. Para una disponibilidad más sólida, configure un grupo de disponibilidad AlwaysOn de SQL Server con instancias de SQL Server en contenedores en un clúster de Kubernetes. En este artículo se comparan las dos soluciones.

## <a name="compare-sql-server-versions-on-kubernetes"></a>Comparación de versiones de SQL Server en Kubernetes

SQL Server 2017 proporciona una imagen de Docker que se puede implementar en Kubernetes. Puede configurar la imagen con una notificación de volumen persistente (PVC) de Kubernetes. Kubernetes supervisa el proceso de SQL Server en el contenedor. Si se produce un error en el proceso, el pod, el contenedor o el nodo, Kubernetes arranca automáticamente otra instancia y vuelve a conectar al almacenamiento.

SQL Server 2019 (versión preliminar) presenta una arquitectura más sólida con StatefulSet de Kubernetes. Kubernetes orquesta las instancias de SQL Server en las imágenes de contenedor que participan en un grupo de disponibilidad AlwaysOn de SQL Server. Este patrón proporciona una mejor supervisión de estado, una recuperación más rápida, copia de seguridad de descarga y escalado horizontal de lectura.  

## <a name="container-with-sql-server-instance-on-kubernetes"></a>Contenedor con instancia de SQL Server en Kubernetes

Kubernetes 1.6 y posterior admite [*clases de almacenamiento*](https://kubernetes.io/docs/concepts/storage/storage-classes/), [*notificaciones de volumen persistente*](https://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims) y el [*tipo de volumen de disco de Azure*](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). 

En esta configuración, Kubernetes desempeña el rol de orquestador de contenedores. 

![Diagrama de clúster de SQL Server de Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

En el diagrama anterior, `mssql-server` es una instancia de SQL Server (contenedor) en un [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod/). Un [conjunto de réplicas](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garantiza que el pod se recupere automáticamente tras un error de nodo. Las aplicaciones se conectan al servicio. En este caso, el servicio representa un equilibrador de carga que hospeda una dirección IP que permanece igual tras un error de `mssql-server`.

Kubernetes orquesta los recursos del clúster. Cuando se produce un error en un nodo que hospeda un contenedor de instancia de SQL Server, arranca un nuevo contenedor con una instancia de SQL Server y lo asocia al mismo almacenamiento persistente.

SQL Server 2017 y posterior admite contenedores en Kubernetes.

Para crear un contenedor en Kubernetes, vea [Implementar un contenedor de SQL Server en Kubernetes](tutorial-sql-server-containers-kubernetes.md)

## <a name="a-sql-server-always-on-availability-group-on-sql-server-containers-in-kubernetes"></a>Grupo de disponibilidad AlwaysOn de SQL Server en contenedores de SQL Server en Kubernetes

SQL Server 2019 admite grupos de disponibilidad en contenedores de Kubernetes. En los grupos de disponibilidad, implemente el [ operador de Kubernetes](https://coreos.com/blog/introducing-operators.html) de SQL Server en el clúster de Kubernetes. El operador ayuda a empaquetar, implementar y administrar instancias de SQL Server y el grupo de disponibilidad en un clúster.

![Grupo de disponibilidad en contenedor de Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

En la imagen anterior, un clúster de Kubernetes de cuatro nodos hospeda un grupo de disponibilidad con tres réplicas. La solución incluye los componentes siguientes:

* Una [*implementación*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) de Kubernetes. La implementación incluye el operador y un mapa de configuración. La implementación describe la imagen de contenedor, el software y las instrucciones necesarias para implementar instancias de SQL Server para el grupo de disponibilidad.

* Tres nodos, cada uno de los cuales hospeda un [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). StatefulSet contiene un pod. Cada pod contiene:
  * Un contenedor de SQL Server que ejecuta una instancia de SQL Server.
  * Un supervisor `mcr.microsoft.com/mssql/ha` para administrar el grupo de disponibilidad.

* Dos [*ConfigMaps*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionados con el grupo de disponibilidad. ConfigMaps proporciona información sobre:
  * La implementación para el operador.
  * Grupo de disponibilidad.

 * Los volúmenes persistentes de cada instancia de SQL Server proporcionan el almacenamiento para los archivos de datos y de registro.

Además, el clúster almacena [*secretos*](https://kubernetes.io/docs/concepts/configuration/secret/) para las contraseñas, los certificados, las claves y otra información confidencial.

## <a name="compare-sql-server-high-availability-on-containers-with-and-without-the-availability-group"></a>Comparar la alta disponibilidad de SQL Server en contenedores con y sin el grupo de disponibilidad

En la tabla siguiente se compara la capacidad de alta disponibilidad de SQL Server en contenedores de Kubernetes con y sin un grupo de disponibilidad:

| |Con un grupo de disponibilidad | Instancia de contenedor independiente<br/> Sin grupo de disponibilidad
|:------|:------|:------
|Recuperación automática tras error de nodo | Sí | Sí
|Recuperación automática tras error de pod | Sí | Sí
|Conmutación por error más rápida |Sí |
|Recuperación automática tras error de instancia de SQL Server | Sí | 
|Recuperación automática tras error de comprobación de estado de base de datos | Sí | 
|Réplicas de solo lectura | Sí |
|Copia de seguridad de réplica secundaria | Sí | 
|Ejecución como StatefulSet | Sí | 

Una diferencia clave es que el tiempo de recuperación (o conmutación por error) es más rápido con un grupo de disponibilidad que con una única instancia de SQL Server en un contenedor. Esta mejora se debe a que el grupo de disponibilidad de SQL Server mantiene las réplicas secundarias en otros nodos del clúster. En la conmutación por error, se selecciona una réplica secundaria y se promueve a principal. Las aplicaciones conectadas al servicio se redirigen a la nueva réplica principal.

Sin el grupo de disponibilidad, cuando Kubernetes detecta una conmutación por error, debe crear el contenedor, conectarlo al almacenamiento y, luego, volver a conectar las aplicaciones conectadas al servicio. El tiempo de conmutación por error exacto depende de la ubicación de la conmutación por error y de cómo se haya detectado. 

Por lo general, el tiempo de conmutación por error de un grupo de disponibilidad se mide en segundos, mientras que el tiempo de conmutación por error de una única instancia para recuperar un contenedor puede ser de hasta 10 minutos.

## <a name="next-steps"></a>Pasos siguientes

Para implementar contenedores de SQL Server en Azure Kubernetes Service (AKS), vea estos ejemplos:

* [Implementación de SQL Server en contenedor de Docker](sql-server-linux-configure-docker.md)
* [Implementar un contenedor de SQL Server en Kubernetes](tutorial-sql-server-containers-kubernetes.md)
* [Grupos de disponibilidad de AlwaysOn para los contenedores de SQL Server](sql-server-ag-kubernetes.md)

