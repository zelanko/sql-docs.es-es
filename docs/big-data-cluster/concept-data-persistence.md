---
title: Persistencia de datos con SQL Server al clúster de macrodatos en Kubernetes | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/01/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 942442bca18e836c4f8711abc808a89649ff8593
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460580"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistencia de datos con el clúster de macrodatos de SQL Server en Kubernetes

[Volúmenes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) proporcionan un modelo de complemento de almacenamiento en donde cómo se proporciona el almacenamiento de Kubernetes es completado abstraen de cómo se consume. Por lo tanto, puede traer su propio almacenamiento de alta disponibilidad y conectarlo al clúster de clúster de macrodatos de SQL Server. Esto le ofrece control completo sobre el tipo de almacenamiento, disponibilidad y rendimiento que necesite. Kubernetes admite diversos tipos de soluciones de almacenamiento como discos y archivos de Azure, NFS, almacenamiento local y mucho más.

## <a name="configure-persistent-volumes"></a>Configurar los volúmenes persistentes

El clúster de macrodatos de SQL Server consume estos volúmenes persistentes de forma es mediante [clases de almacenamiento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Puede crear clases de almacenamiento diferentes para diferentes tipos de almacenamiento y especificarlos en el momento de implementación del clúster de macrodatos. Puede configurar qué clase de almacenamiento para usar con qué propósito (grupo). Crea el clúster de SQL Server macrodatos [notificaciones de volumen persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con el nombre de clase de almacenamiento especificada para cada pod que requiere volúmenes persistentes. A continuación, monte los volúmenes persistentes correspondientes en el pod.

> [!NOTE]

> Para CTP 2.0, solo `ReadWriteOnce` se admite el modo de acceso para todo el clúster.

## <a name="deployment-settings"></a>Configuración de implementación

Para usar el almacenamiento persistente durante la implementación, configure el **USE_PERSISTENT_VOLUME** y **STORAGE_CLASS_NAME** variables de entorno antes de ejecutar `mssqlctl create cluster` comando. **USE_PERSISTENT_VOLUME** está establecido en `true` de forma predeterminada. Puede invalidar el valor predeterminado y establézcalo como `false` y, en este caso, el clúster de macrodatos de SQL Server usa emptyDir montajes. 

> [!WARNING]
> Puede dar lugar a ejecución sin almacenamiento persistente en un clúster que no son funcionales. Tras el reinicio de pod, datos de metadatos o el usuario del clúster se perderán permanentemente.

Si establece la marca en true, también debe proporcionar **STORAGE_CLASS_NAME** como un parámetro en el momento de la implementación.

## <a name="aks-storage-classes"></a>Clases de almacenamiento AKS

AKS viene con [dos clases de almacenamiento integradas](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **predeterminada** y **premium managed** junto con aprovisionador dinámica para ellos. Puede especificar cualquiera de ellos o crear su propia clase de almacenamiento para la implementación de clúster de macrodatos con habilitado el almacenamiento persistente.

## <a name="minikube-storage-class"></a>Clase de almacenamiento de Minikube

Minikube viene con una clase de almacenamiento integrada llamada **estándar** junto con una dinámica aprovisionador para él. Tenga en cuenta que en Minikube, si USE_PERSISTENT_VOLUME = true (valor predeterminado), también debe invalidar el valor predeterminado de la variable de entorno STORAGE_CLASS_NAME porque el valor predeterminado es diferente. Establezca el valor en `standard`: 
```
SET STORAGE_CLASS_NAME=standard
```

Como alternativa, puede suprimir con volúmenes persistentes en Minikube:
```
SET USE_PERSISTENT_VOLUME=false
```


## <a name="kubeadm"></a>Kubeadm

Kubeadm no se incluye con una clase de almacenamiento integradas; por lo tanto, hemos creado las secuencias de comandos para configurar los volúmenes persistentes y las clases de almacenamiento mediante el almacenamiento local o [torre](https://github.com/rook/rook) almacenamiento.

## <a name="on-premises-cluster"></a>Clúster local

Clústeres locales obviamente no se suministran con cualquier clase de almacenamiento integrada, por lo tanto, debe configurar [volúmenes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)/[aprovisionadores](https://kubernetes.io/docs/concepts/storage/dynamic-provisioning/) con antelación y, a continuación, utilice el correspondiente clases de almacenamiento durante la implementación de clúster de macrodatos de SQL Server.

# <a name="customize-storage-size-for-each-pool"></a>Personalizar el tamaño de cada grupo de almacenamiento
De forma predeterminada, el tamaño del volumen persistente aprovisionado para cada uno de los pods aprovisionados en el clúster es 6 GB. Esto es configurable mediante el establecimiento de la variable de entorno `STORAGE_SIZE` en un valor diferente. Por ejemplo, puede ejecutar comando siguiente para establecer el valor a 10 GB, antes de ejecutar el `mssqlctl create cluster command`.

```bash
export STORAGE_SIZE=10Gi
```

También puede tener diferentes configuraciones para la configuración de almacenamiento persistente de tal nombre de clase de almacenamiento y los tamaños de volumen persistente para los diferentes grupos en el clúster. Por ejemplo, puede configurar los volúmenes persistentes implementados para que el grupo de almacenamiento usar una clase de almacenamiento diferente y tiene una capacidad mayor por valor debajo de las variables de entorno antes de implementar el clúster:

```bash
export STORAGE_POOL_USE_PERSISTENT_VOLUME=true
export STORAGE_POOL_STORAGE_CLASS_NAME=managed-premium
export STORAGE_POOL_STORAGE_SIZE=100Gi
```

Esta es una lista completa de las variables de entorno relacionadas con la configuración de almacenamiento persistente para el clúster de SQL Server Big Data:

| Variable de entorno | Valor predeterminado | Descripción |
|---|---|---|
| **USE_PERSISTENT_VOLUME** | true | `true` Para usar notificaciones de volumen persistente de Kubernetes para el almacenamiento de pod. `false` uso del almacenamiento efímero host para el almacenamiento de pod. |
| **STORAGE_CLASS_NAME** | predeterminados | Si `USE_PERSISTENT_VOLUME` es `true` indica el nombre de la clase de almacenamiento de Kubernetes para usar. |
| **STORAGE_SIZE** | 6gi | Si `USE_PERSISTENT_VOLUME` es `true`, esto indica el tamaño del volumen persistente para cada pod. |
| **DATA_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Para usar notificaciones de volumen persistente de Kubernetes para los pods en el grupo de datos. `false` Para usar el almacenamiento efímero host para los pods de grupo de datos. |
| **DATA_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | Indica el nombre de la clase de almacenamiento de Kubernetes que se usará para los volúmenes persistentes asociados con los pods de grupo de datos.|
| **DATA_POOL_STORAGE_SIZE** | STORAGE_SIZE |Indica el tamaño de volumen persistente para cada pod en el grupo de datos. |
| **STORAGE_POOL_USE_PERSISTENT_VOLUME** | USE_PERSISTENT_VOLUME | `true` Para usar notificaciones de volumen persistente de Kubernetes para los pods en el bloque de almacenamiento. `false` Para usar el almacenamiento efímero host para los pods de grupo de almacenamiento.|
| **STORAGE_POOL_STORAGE_CLASS_NAME** | STORAGE_CLASS_NAME | El nombre de la clase de almacenamiento de Kubernetes que se usará para los volúmenes persistentes TIndicates asociado pods del grupo de almacenamiento. |
| **STORAGE_POOL_STORAGE_SIZE** | STORAGE_SIZE | Indica el tamaño de volumen persistente para cada pod del bloque de almacenamiento. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener documentación completa sobre los volúmenes de Kubernetes, consulte el [documentación de Kubernetes en volúmenes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obtener más información sobre la implementación de clúster de macrodatos de SQL Server, vea [cómo implementar SQL Server al clúster de macrodatos en Kubernetes](deployment-guidance.md).

