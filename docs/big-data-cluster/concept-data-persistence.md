---
title: Persistencia de los datos en Kubernetes
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo funciona la persistencia de los datos en un clúster de macrodatos de SQL Server 2019.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: cfba93aaca23ca3303b6d9bd9752c1d458a9a81a
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388013"
---
# <a name="data-persistence-with-sql-server-big-data-cluster-on-kubernetes"></a>Persistencia de datos con el clúster de macrodatos de SQL Server en Kubernetes

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[Volúmenes persistentes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) proporcionan un modelo de complemento para el almacenamiento en Kubernetes. Cómo se proporciona el almacenamiento de información se extrae del modo de utilización. Por lo tanto, puede traer su propio almacenamiento de alta disponibilidad y conectarlo al clúster de macrodatos de SQL Server. Esto le ofrece control completo sobre el tipo de almacenamiento, disponibilidad y rendimiento que necesite. Kubernetes admite diversos tipos de soluciones de almacenamiento como discos y archivos de Azure, NFS, almacenamiento local y mucho más.

## <a name="configure-persistent-volumes"></a>Configurar los volúmenes persistentes

Es la forma en un clúster de macrodatos de SQL Server consume estos volúmenes persistentes mediante [clases de almacenamiento](https://kubernetes.io/docs/concepts/storage/storage-classes/). Puede crear clases de almacenamiento diferentes para diferentes tipos de almacenamiento y especificarlos en el momento de implementación del clúster de macrodatos. Puede configurar qué clase de almacenamiento y el tamaño de la notificación de volumen persistente para utilizar con qué propósito en el nivel de grupo. Crea un clúster de SQL Server macrodatos [notificaciones de volumen persistente](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims) con el nombre de clase de almacenamiento especificada para cada componente que requiere volúmenes persistentes. A continuación, monte los volúmenes persistentes correspondientes en el pod. 

## <a name="configure-big-data-cluster-storage-settings"></a>Configurar opciones de almacenamiento de clúster de macrodatos

Al igual que otras personalizaciones, puede especificar la configuración de almacenamiento en los archivos de configuración de clúster en tiempo de implementación para cada grupo y el plano de control. Si no hay ninguna configuración de almacenamiento en las especificaciones de grupo, se usará la configuración de almacenamiento del plano de control. Este es un ejemplo de la sección de configuración de almacenamiento que se puede incluir en las especificaciones:

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

Implementación de clúster de macrodatos usarán almacenamiento persistente para almacenar datos, metadatos y los registros para los distintos componentes. Puede personalizar el tamaño de las notificaciones de volumen persistente creado como parte de la implementación. Como práctica recomendada, se recomienda para usar clases de almacenamiento con un *conservar* [reclamar directiva](https://kubernetes.io/docs/concepts/storage/storage-classes/#reclaim-policy).

> [!NOTE]
> En CTP 3.1, no se puede modificar el almacenamiento configuración configuración posterior a la implementación. Además, solo `ReadWriteOnce` se admite el modo de acceso para todo el clúster.

> [!WARNING]
> Se ejecute sin almacenamiento persistente puede funcionar en un entorno de prueba, pero podría dar como resultado en un clúster que no son funcionales. Tras el reinicio de pod, datos de metadatos o el usuario del clúster se perderán permanentemente. No se recomienda para ejecutar en esta configuración. 

[Configurar el almacenamiento](#config-samples) sección proporciona más ejemplos sobre cómo configurar opciones de almacenamiento para la implementación de clúster de macrodatos de SQL Server.

## <a name="aks-storage-classes"></a>Clases de almacenamiento AKS

AKS viene con [dos clases de almacenamiento integradas](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) **predeterminada** y **premium managed** junto con aprovisionador dinámica para ellos. Puede especificar cualquiera de ellos o crear su propia clase de almacenamiento para la implementación de clúster de macrodatos con habilitado el almacenamiento persistente. De forma predeterminada, la compilación en el archivo de configuración de clúster de aks *aks-dev-test* viene con configuraciones de almacenamiento persistente para usar **predeterminada** clase de almacenamiento.

> [!WARNING]
> Volúmenes persistentes creados con las clases de almacenamiento integrada **predeterminada** y **premium managed** tienen una directiva de recuperación de *eliminar*. Por lo que en el momento en el se elimina el clúster de macrodatos de SQL Server, las notificaciones de volumen persistente obtención también los volúmenes eliminados y, a continuación, persistentes. Puede crear clases de almacenamiento personalizado mediante **azure disco** privioner con un *conservar* reclamar directiva como se muestra en [esto](https://docs.microsoft.com/en-us/azure/aks/concepts-storage#storage-classes) artículo.


## <a name="minikube-storage-class"></a>Clase de almacenamiento de Minikube

Minikube viene con una clase de almacenamiento integrada llamada **estándar** junto con una dinámica aprovisionador para él. La configuración generada en el archivo de minikube *minikube-dev-test* tiene las opciones de configuración de almacenamiento en la especificación de plano de control. La misma configuración se aplicará a todas las especificaciones de los grupos. También puede personalizar una copia de este archivo y usarlo para implementar el clúster de macrodatos en minikube. Puede editar el archivo personalizado manualmente y cambiar el tamaño de las notificaciones de los volúmenes persistentes para los grupos específicos dar cabida a las cargas de trabajo que desea ejecutar. O bien, consulte [configurar almacenamiento](#config-samples) sección para obtener ejemplos sobre cómo hacerlo edita utilizando *mssqlctl* comandos.

## <a name="kubeadm-storage-classes"></a>Clases de almacenamiento Kubeadm

Kubeadm no viene con una clase de almacenamiento integrada. Debe crear sus propias clases de almacenamiento y los volúmenes persistentes con almacenamiento local o el aprovisionador preferido, como [torre](https://github.com/rook/rook). En ese caso, establecería el **className** a la clase de almacenamiento que configuró. 

> [!NOTE]
>  En la compilación en el archivo de configuración de implementación para *kubeadm kubeadm-dev-test* hay ningún nombre de clase de almacenamiento especificada para el almacenamiento de datos y de registro. Antes de la implementación, debe personalizar el archivo de configuración y establezca el valor de className en caso contrario, que se producirá un error en las validaciones previas a la implementación. La implementación también tiene un paso de validación que comprueba la existencia de la clase de almacenamiento, pero no para los volúmenes persistentes necesarios. Debe asegurarse de que crear suficiente volúmenes según la escala del clúster. En CTP 3.1, para el tamaño predeterminado del clúster debe crear al menos 23 volúmenes. [Aquí](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu) es un ejemplo sobre cómo crear los volúmenes persistentes con aprovisionador local.


## <a name="customize-storage-configurations-for-each-pool"></a>Personalizar las configuraciones de almacenamiento para cada grupo

Para todas las personalizaciones, primero debe crear una copia de la compilación en el archivo de configuración que desea usar. Por ejemplo, el siguiente comando crea una copia de la *aks-dev-test* archivo de configuración de implementación en un subdirectorio denominado `custom`:

```bash
mssqlctl bdc config init --source aks-dev-test --target custom
```

A continuación, puede personalizar el archivo de configuración mediante la edición de forma manual, o puede usar **mssqlctl bdc config sección conjunto** comando. Este comando usa una combinación de bibliotecas jsonpath y jsonpatch para proporcionar maneras de modificar el archivo de configuración.

### <a name="configure-size"></a>Configurar el tamaño

De forma predeterminada, el tamaño de las notificaciones de volumen persistente aprovisionados para cada uno de los pods aprovisionados en el clúster es 10 GB. Puede actualizar este valor para dar cabida a las cargas de trabajo que se ejecuta en un archivo de configuración personalizado antes de la implementación de clúster.

El ejemplo siguiente actualiza solo el tamaño de volumen persistente notificaciones para los datos almacenados en el grupo de almacenamiento para 100Gi. Tenga en cuenta que la sección de almacenamiento debe existir en el archivo de configuración del grupo de almacenamiento antes de ejecutar este comando:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=100Gi"
```

El ejemplo siguiente actualiza el tamaño de volumen persistente notificaciones para todos los grupos a 32Gi:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.storage.data.size=32Gi"
```

### <a id="config-samples"></a> Configurar clase de almacenamiento

El ejemplo siguiente muestra cómo modificar la clase de almacenamiento para el plano de control:

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.storage.data.className=<yourStorageClassName>"
```

Otra opción es modificar manualmente el archivo de configuración personalizado o utilizar jsonpatch como en el ejemplo siguiente que cambia la clase de almacenamiento para el grupo de almacenamiento. Crear un *patch.json* archivo con este contenido:

```json
{
  "patch": [
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
      "value": {
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

Aplicar el archivo de revisión. Use **mssqlctl bdc config sección conjunto** comando para aplicar los cambios en el archivo de revisión JSON. El ejemplo siguiente aplica el archivo patch.json a un custom.json de archivo de configuración de implementación de destino.

```bash
mssqlctl bdc config section set --config-profile custom -p ./patch.json
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener documentación completa sobre los volúmenes de Kubernetes, consulte el [documentación de Kubernetes en volúmenes](https://kubernetes.io/docs/concepts/storage/volumes/).

Para obtener más información sobre cómo implementar un clúster de macrodatos de SQL Server, vea [cómo implementar SQL Server al clúster de macrodatos en Kubernetes](deployment-guidance.md).

