---
title: Persistencia de los datos en Kubernetes
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo funciona la persistencia de los datos en un clúster de macrodatos de SQL Server 2019.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb6d87803c0a3839afd8dbd1333b52c3abcc4518
ms.sourcegitcommit: dacf6c57f6a2e3cf2005f3268116f3c609639905
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/11/2019
ms.locfileid: "70878738"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistencia de los datos con un clúster de macrodatos de SQL Server en Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Los [volúmenes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) proporcionan un modelo de complemento para el almacenamiento en Kubernetes. La forma en que se proporciona el almacenamiento depende de cómo se use. Por lo tanto, puede usar su propio almacenamiento con alta disponibilidad y conectarlo al clúster de macrodatos de SQL Server. Esto le proporciona control total sobre el tipo de almacenamiento, la disponibilidad y el rendimiento que necesite. Kubernetes admite distintos tipos de soluciones de almacenamiento, como discos o archivos de Azure, NFS, almacenamiento local, y más.

## <a name="configure-persistent-volumes"></a>Configurar volúmenes persistentes

El clúster de macrodatos de SQL Server consume estos volúmenes persistentes mediante [clases de almacenamiento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Puede crear distintas clases de almacenamiento para diferentes tipos de almacenamiento y especificarlos todos en el momento de la implementación del clúster de macrodatos. Puede configurar la clase de almacenamiento y el tamaño de la reclamación de volumen persistente que se usará para cada finalidad en el nivel de grupo. Un clúster de macrodatos de SQL Server crea [reclamaciones de volúmenes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con el nombre de la clase de almacenamiento especificado para cada componente que necesite volúmenes persistentes. Después, monta los volúmenes persistentes correspondientes en el pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Configurar las opciones de almacenamiento del clúster de macrodatos

De forma similar a otras personalizaciones, puede especificar la configuración de almacenamiento en los archivos de configuración del clúster en el momento de la implementación para cada grupo del archivo de configuración **BDC. JSON** y para los servicios de control en el archivo **control. JSON** . Si no hay ninguna opción de configuración de almacenamiento en las especificaciones del grupo, la configuración de almacenamiento del control se usará **para todos los demás componentes**, incluidos SQL Server maestro (recurso**principal** ), HDFS (recurso**de almacenamiento 0** ) o datos Fondo. Esto es un ejemplo de la sección de configuración de almacenamiento que puede incluir en las especificaciones:

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

La implementación del clúster de macrodatos usará el almacenamiento persistente para almacenar datos, metadatos y registros para distintos componentes. Puede personalizar el tamaño de las reclamaciones de volúmenes persistentes creadas como parte de la implementación. El procedimiento recomendado es usar clases de almacenamiento con una *directiva de reclamación* de [Conservar](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy).

> [!NOTE]
> En CTP 3.2, no se puede modificar la configuración de almacenamiento después de la implementación. Además, solo se admite el modo de acceso `ReadWriteOnce` para todo el clúster.

> [!WARNING]
> La ejecución sin almacenamiento persistente puede funcionar en un entorno de prueba, pero daría como resultado un clúster no funcional. Al reiniciarse el pod, los metadatos del clúster o los datos de usuario se perderían de forma permanente. No le recomendamos ejecutarlo en esta configuración. 

En la sección [Configurar el almacenamiento](#config-samples), se proporcionan más ejemplos de cómo configurar el almacenamiento para su implementación del clúster de macrodatos de SQL Server.

## <a name="aks-storage-classes"></a>Clases de almacenamiento de AKS

AKS tiene [dos clases de almacenamiento integradas](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) (**default** y **managed-premium**), además del aprovisionador dinámico para estas. Puede especificar una de estas, o bien puede crear su propia clase de almacenamiento para implementar el clúster de macrodatos con el almacenamiento persistente habilitado. De forma predeterminada, en el archivo de configuración del clúster integrado para AKS (*aks-dev-test*) se incluyen configuraciones de almacenamiento persistente que usan la clase de almacenamiento **default**.

> [!WARNING]
> Los volúmenes persistentes creados con las clases de almacenamiento integradas **default** y **managed-premium** tienen una directiva de reclamación de *Eliminar*. Por lo tanto, al eliminar el clúster de macrodatos de SQL Server, también se eliminarán las reclamaciones de volúmenes persistentes, así como los volúmenes persistentes. Puede crear clases de almacenamiento personalizadas mediante el aprovisionador **azure-disk** con una directiva de reclamación de *Conservar*, como se muestra en [este artículo](https://docs.microsoft.com/azure/aks/concepts-storage#storage-classes).


## <a name="minikube-storage-class"></a>Clase de almacenamiento de Minikube

Minikube cuenta con una clase de almacenamiento integrada denominada **standard**, además de un aprovisionador dinámico para esta. El archivo de configuración integrado de Minikube (*minikube-dev-test*) tiene las opciones de configuración en la especificación del plano de control. La misma configuración se aplicará a todas las especificaciones de grupos. También puede personalizar una copia del archivo y usarla para su implementación del clúster de macrodatos en Minikube. Puede editar de forma manual el archivo personalizado y cambiar el tamaño de las reclamaciones de los volúmenes persistentes para grupos específicos con el fin de adaptarse a las cargas de trabajo que quiera ejecutar. O bien vea la sección [Configurar el almacenamiento](#config-samples) para obtener ejemplos de cómo realizar ediciones mediante los comandos de *azdata*.

## <a name="kubeadm-storage-classes"></a>Clases de almacenamiento de Kubeadm

En Kubeadm, no se incluye una clase de almacenamiento integrada. Necesita crear sus propias clases de almacenamiento y volúmenes persistentes mediante almacenamiento local o su aprovisionador preferido, como [Rook](https://github.com/rook/rook). En ese caso, tendría que establecer el elemento **className** en la clase de almacenamiento que haya configurado. 

> [!NOTE]
>  En el archivo de configuración de implementación integrado de *kubeadm kubeadm-dev-test*, no se especifica ningún nombre de clase de almacenamiento para los datos y el almacenamiento de registros. Antes de la implementación, necesita personalizar el archivo de configuración y establecer el valor del elemento className; de lo contrario, las validaciones antes de la implementación producirán errores. La implementación también tiene un paso de validación que comprueba si existe la clase de almacenamiento, pero no para los volúmenes persistentes necesarios. Tiene que asegurarse de crear volúmenes suficientes, según la escala del clúster. En CTP 3.1, para el tamaño del clúster predeterminado, necesita crear como mínimo 23 volúmenes. [Aquí](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) puede ver un ejemplo de cómo crear volúmenes persistentes mediante el aprovisionador local.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar las configuraciones de almacenamiento para cada grupo

Para todas las personalizaciones, primero tiene que crear una copia del archivo de configuración integrado que quiera usar. Por ejemplo, el comando siguiente crea una copia de los archivos de configuración de implementación de *aks-dev-test* en un subdirectorio llamado `custom`:

```bash
azdata bdc config init --source aks-dev-test --target custom
```

Esto crea dos archivos, **BDC. JSON** y **control. JSON** , que se pueden personalizar editando manualmente, o bien se puede usar el comando **azdata de configuración de BDC** . Puede usar una combinación de las bibliotecas jsonpath y jsonpatch para proporcionar formas de editar los archivos de configuración.


### <a id="config-samples"></a> Configurar el nombre de la clase de almacenamiento o el tamaño de las reclamaciones

De forma predeterminada, el tamaño de las reclamaciones de volúmenes persistentes aprovisionadas para cada pod en el clúster es de 10 GB. Puede actualizar este valor para adaptarse a las cargas de trabajo que ejecute en un archivo de configuración personalizado antes de la implementación del clúster.

En el ejemplo siguiente, se actualiza a 32 Gi el tamaño de las reclamaciones de volúmenes persistentes tamaño en el archivo **control.jsaon**. Si no se reemplaza en el nivel de grupo, esta opción se aplicará en todos los grupos:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.size=100Gi"
```

En el ejemplo siguiente, se muestra cómo modificar la clase de almacenamiento del archivo **control.json**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.storage.data.className=<yourStorageClassName>"
```

Otra opción es editar de forma manual el archivo de configuración personalizado o usar una revisión de JSON (como en el ejemplo siguiente) que cambia la clase de almacenamiento para el grupo de almacenamiento. Cree un archivo *patch.json* con este contenido:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.resources.storage-0.spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
            "data":{
                    "size": "100Gi",
                    "className": "myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    },
            "logs":{
                    "size":"32Gi",
                    "className":"myStorageClass",
                    "accessMode":"ReadWriteOnce"
                    }
                }
            }
        }
    ]
}
```

Aplique el archivo de revisión. Use el comando **azdata bdc config patch** para aplicar los cambios en el archivo de revisión JSON. En el ejemplo siguiente, se aplica el archivo patch.json en un archivo de configuración de implementación de destino custom.json.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los volúmenes en Kubernetes, vea la [Documentación de Kubernetes sobre volúmenes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obtener más información sobre cómo implementar un clúster de macrodatos de SQL Server, vea [Procedimiento para implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).

