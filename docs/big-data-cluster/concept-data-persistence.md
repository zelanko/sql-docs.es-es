---
title: Persistencia de los datos en Kubernetes
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo funciona la persistencia de datos en un clúster de macrodatos SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9142836032acc5e302c947e1619d17b07faff683
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419469"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistencia de datos con SQL Server clúster de macrodatos en Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Los [volúmenes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) proporcionan un modelo de complemento para el almacenamiento en Kubernetes. La forma en que se proporciona el almacenamiento se abstrae del modo en que se consume. Por lo tanto, puede traer su propio almacenamiento de alta disponibilidad y conectarlo al SQL Server clúster de Big Data. Esto le proporciona un control total sobre el tipo de almacenamiento, la disponibilidad y el rendimiento que necesita. Kubernetes admite varios tipos de soluciones de almacenamiento, como discos y archivos de Azure, NFS, almacenamiento local, etc.

## <a name="configure-persistent-volumes"></a>Configurar volúmenes persistentes

La forma en que un clúster de macrodatos de SQL Server consume estos volúmenes persistentes es mediante el uso de [clases de almacenamiento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Puede crear diferentes clases de almacenamiento para diferentes tipos de almacenamiento y especificarlas en el momento de la implementación del clúster de Big Data. Puede configurar la clase de almacenamiento y el tamaño de la demanda de volumen persistente que se usará para cada propósito en el nivel de grupo. Un clúster de macrodatos SQL Server crea notificaciones de [volumen persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con el nombre de clase de almacenamiento especificado para cada componente que requiere volúmenes persistentes. A continuación, monta los volúmenes persistentes correspondientes en el POD. 

## <a name="configure-big-data-cluster-storage-settings"></a>Configurar las opciones de almacenamiento del clúster de Big Data

Al igual que otras personalizaciones, puede especificar la configuración de almacenamiento en los archivos de configuración del clúster en el momento de la implementación para cada grupo y el plano de control. Si no hay ninguna opción de configuración de almacenamiento en las especificaciones del grupo, se usará la configuración de almacenamiento del plano de control. Este es un ejemplo de la sección de configuración de almacenamiento que puede incluir en las especificaciones:

```json
    "storage": 
    {
      "data": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "15Gi"
      },
      "logs": {
        "className": "default",
        "accessMode": "ReadWriteOnce",
        "size": "10Gi"
    }
```

La implementación del clúster de Big Data usará el almacenamiento persistente para almacenar datos, metadatos y registros para varios componentes. Puede personalizar el tamaño de las notificaciones de volumen persistentes creadas como parte de la implementación. Como práctica recomendada, se recomienda usar las clases de almacenamiento con una  [Directiva](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy)de retención retenida.

> [!NOTE]
> En CTP 3,2, no se puede modificar la configuración de almacenamiento después de la implementación. Además, solo `ReadWriteOnce` se admite el modo de acceso para todo el clúster.

> [!WARNING]
> La ejecución sin almacenamiento persistente puede funcionar en un entorno de prueba, pero podría dar lugar a un clúster no funcional. Tras reiniciarse Pod, los metadatos de clúster o los datos de usuario se perderán de forma permanente. No se recomienda ejecutar en esta configuración. 

En la sección [configuración de almacenamiento](#config-samples) se proporcionan más ejemplos sobre cómo configurar las opciones de almacenamiento para la implementación de SQL Server Big Data cluster.

## <a name="aks-storage-classes"></a>Clases de almacenamiento AKS

AKS incluye [dos clases de almacenamiento integradas](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv)  predeterminadas y **Managed-Premium** junto con el aprovisionamiento dinámico para ellas. Puede especificar cualquiera de esos o crear su propia clase de almacenamiento para implementar un clúster de Big Data con almacenamiento persistente habilitado. De forma predeterminada, el archivo de configuración de clúster integrado para AKS *AKS-dev-test* incluye configuraciones de almacenamiento persistentes para usar la clase de almacenamiento **predeterminada** .

> [!WARNING]
> Los volúmenes persistentes creados con las clases de almacenamiento integradas **default** y **Managed-Premium** tienen una directiva de recuperación de *eliminación*. Por lo tanto, en el momento en que se elimina el clúster de macrodatos SQL Server, las notificaciones de volumen persistentes se eliminan y, luego, los volúmenes persistentes. Puede crear clases de almacenamiento personalizadas mediante **Azure-Disk** privioner con una  Directiva retain retain, tal como se muestra en [este](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) artículo.


## <a name="minikube-storage-class"></a>Clase de almacenamiento Minikube

Minikube incluye una clase de almacenamiento integrada denominada **Standard** junto con un aprovisionamiento dinámico para ella. El archivo de configuración integrado para minikube *minikube-dev-test* tiene las opciones de configuración de almacenamiento en la especificación del plano de control. Se aplicará la misma configuración a todas las especificaciones de grupos. También puede personalizar una copia de este archivo y usarlo para la implementación del clúster de Big Data en minikube. Puede editar manualmente el archivo personalizado y cambiar el tamaño de las notificaciones de volúmenes persistentes para grupos específicos para acomodar las cargas de trabajo que desea ejecutar. O bien, consulte Configuración de la sección de [almacenamiento](#config-samples) para ver ejemplos de cómo realizar modificaciones con comandos de *azdata* .

## <a name="kubeadm-storage-classes"></a>Clases de almacenamiento Kubeadm

Kubeadm no se incluye con una clase de almacenamiento integrada. Debe crear sus propias clases de almacenamiento y volúmenes persistentes mediante el almacenamiento local o el aprovisionamiento preferido, como [torre](https://github.com/rook/rook). En ese caso, debe establecer el valor de **className** en la clase de almacenamiento que configuró. 

> [!NOTE]
>  En el archivo de configuración de implementación integrado para *kubeadm kubeadm-dev-test* no hay ningún nombre de clase de almacenamiento especificado para el almacenamiento de datos y de registros. Antes de la implementación, debe personalizar el archivo de configuración y establecer el valor de className; de lo contrario, se producirá un error en las validaciones anteriores a la implementación. La implementación también tiene un paso de validación que comprueba la existencia de la clase de almacenamiento, pero no los volúmenes persistentes necesarios. Debe asegurarse de que crea volúmenes suficientes en función de la escala del clúster. En CTP 3,1, para el tamaño de clúster predeterminado, debe crear al menos 23 volúmenes. [Este](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) es un ejemplo de cómo crear volúmenes persistentes con el aprovisionamiento local.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalización de las configuraciones de almacenamiento para cada grupo

Para todas las personalizaciones, debe crear primero una copia del archivo de configuración integrado que desee usar. Por ejemplo, el siguiente comando crea una copia de los archivos de configuración de implementación de *AKS-dev-test* en un subdirectorio denominado `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Esto crea dos archivos, **cluster. JSON** y **control. JSON** que se pueden personalizar editando manualmente, o bien se puede usar el comando **azdata de configuración de BDC** . Puede usar una combinación de las bibliotecas jsonpath y jsonpatch para proporcionar maneras de editar los archivos de configuración.


### <a id="config-samples"></a>Configuración del nombre de clase de almacenamiento y/o el tamaño de las notificaciones

De forma predeterminada, el tamaño de las notificaciones de volumen persistente aprovisionadas para cada Pod aprovisionado en el clúster es de 10 GB. Puede actualizar este valor para acomodar las cargas de trabajo que se ejecutan en un archivo de configuración personalizado antes de la implementación del clúster.

En el ejemplo siguiente se actualiza el tamaño del tamaño de las notificaciones de volumen persistentes a 32Gi en el **control. jsaon**. Si no se invalida en el nivel de grupo, esta configuración se aplicará a todos los grupos:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

En el ejemplo siguiente se muestra cómo modificar la clase de almacenamiento para el archivo **control. JSON** :

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Otra opción consiste en editar manualmente el archivo de configuración personalizado o usar el parche JSON como en el ejemplo siguiente, que cambia la clase de almacenamiento para el bloque de almacenamiento. Cree un archivo *patch. JSON* con este contenido:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage"
      "value": {
          "type":"Storage",
          "replicas":2,
          "data": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "default",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
      }
  ]
}
```

Aplique el archivo de revisión. Use el comando **azdata de configuración de BDC** para aplicar los cambios en el archivo de revisión de JSON. En el ejemplo siguiente se aplica el archivo patch. JSON a un archivo de configuración de implementación de destino Custom. JSON.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener documentación completa sobre los volúmenes de Kubernetes, consulte la [documentación de Kubernetes sobre volúmenes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obtener más información sobre la implementación de un clúster de macrodatos SQL Server, consulte [How to deploy SQL Server Big Data Cluster in Kubernetes](deployment-guidance.md).

