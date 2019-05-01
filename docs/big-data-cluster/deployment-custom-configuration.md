---
title: Configurar las implementaciones
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo personalizar la implementación de un clúster de macrodatos con archivos de configuración.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7dd774d390587d0c2c0248ab9b419ad40f8f212b
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759172"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Configurar opciones de implementación para los clústeres de datos de gran tamaño

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar el archivo de configuración de implementación de clúster, puede usar cualquier editor de formato de json como VSCode. Para estas modificaciones para fines de automatización de la secuencia de comandos, proporcionamos un **sección de configuración de clúster mssqlctl** comando. En este artículo se explica cómo configurar las implementaciones de clústeres de datos de gran tamaño mediante la modificación de los archivos de configuración de implementación. Se proporcionan ejemplos de cómo cambiar la configuración para diferentes escenarios. Para obtener más información sobre cómo se usan archivos de configuración en las implementaciones, consulte la [instrucciones de implementación](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Requisitos previos

- [Instalar mssqlctl](deploy-install-mssqlctl.md).

- Cada uno de los ejemplos en esta sección se supone que ha creado una copia de uno de los archivos de configuración estándar. Para obtener más información, consulte [crear un archivo de configuración personalizado](deployment-guidance.md#customconfig). Por ejemplo, el siguiente comando crea un **custom.json** archivo según el valor predeterminado **aks-dev-test.json** configuración:

   ```bash
   mssqlctl cluster config init --src aks-dev-test.json --target custom.json
   ```

## <a id="clustername"></a> Cambiar el nombre de clúster

El nombre del clúster es el nombre del clúster datos de gran tamaño y el espacio de nombres de Kubernetes que se crearán en la implementación. Se especifica en la siguiente parte del archivo de configuración de implementación:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

El siguiente comando envía un par clave-valor a la **--json valores** parámetro para cambiar el nombre del clúster de macrodatos a **test-cluster**:

```bash
mssqlctl cluster config section set -f custom.json -j ".metadata.name=test-cluster"
```

> [!IMPORTANT]
> El nombre del clúster debe ser solo alfanuméricos caracteres en minúsculas, sin espacios en blanco. Todos los artefactos de Kubernetes (contenedores, pods, conjuntos con estado, los servicios) para el clúster se creará en un espacio de nombres con el mismo nombre que el clúster de nombre especificado.

## <a id="ports"></a> Puertos de punto de conexión de actualización

Los puntos de conexión se definen para el plano de control, así como para los grupos individuales. La siguiente parte del archivo de configuración muestra las definiciones de punto de conexión para el plano de control:

```json
"endpoints": [
    {
        "name": "Controller",
        "serviceType": "LoadBalancer",
        "port": 30080
    },
    {
        "name": "ServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30777
    },
    {
        "name": "AppServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30778
    },
    {
        "name": "Knox",
        "serviceType": "LoadBalancer",
        "port": 30443
    }
]
```

En el ejemplo siguiente se usa en línea JSON para cambiar el puerto para el **controlador** punto de conexión:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configurar réplicas de grupo

Las características de cada grupo, por ejemplo, el bloque de almacenamiento, se define en el archivo de configuración. Por ejemplo, en el siguiente fragmento muestra una definición de grupo de almacenamiento:

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "storage": {
                "usePersistentVolume": true,
                "className": "managed-premium",
                "accessMode": "ReadWriteOnce",
                "size": "10Gi"
            }
        }
    }
]
```

Puede configurar el número de instancias de un grupo mediante la modificación de la **réplicas** valor para cada grupo. En el ejemplo siguiente se usa en línea JSON para cambiar estos valores para los grupos de almacenamiento y datos `10` y `4` respectivamente:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4'
```

> [!IMPORTANT]
> En esta versión, no se puede cambiar el número de instancias en el grupo de proceso.

## <a id="storage"></a> Configurar el almacenamiento

También puede cambiar la clase de almacenamiento y las características que se usan para cada grupo. El ejemplo siguiente asigna una clase de almacenamiento personalizado para el grupo de almacenamiento:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec={""replicas"": 2,""storage"": {""className"": ""newStorageClass"",""size"": ""20Gi"",""accessMode"": ""ReadWriteOnce"",""usePersistentVolume"": true},""type"": ""Storage""}"
```

El ejemplo siguiente actualiza solo el tamaño de bloque de almacenamiento para `32Gi`:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.size=32Gi"
```

En el ejemplo siguiente se actualiza el tamaño de todos los grupos a `32Gi`:

```bash
mssqlctl cluster config section set -f custom.json -j "$.spec.pools[?(@.spec.type[*])].spec.storage.size=32Gi"
```

> [!NOTE]
> Un archivo de configuración basado en **kubeadm-dev-test.json** no tiene una definición de almacenamiento para cada grupo, pero esto puede agregarse manualmente si es necesario.

Para obtener más información acerca de la configuración de almacenamiento, consulte [persistencia de datos con SQL Server al clúster de macrodatos en Kubernetes](concept-data-persistence.md).

## <a id="podplacement"></a> Configurar selección de ubicación de pod mediante etiquetas de Kubernetes

Puede controlar la colocación de pod en nodos de Kubernetes que cuente con recursos específicos para dar cabida a varios tipos de requisitos de carga de trabajo. Por ejemplo, es posible que desee garantizar los pods de grupo de almacenamiento se coloquen en nodos con más espacio de almacenamiento o las instancias maestras de SQL Server se colocan en los nodos que tengan recursos de memoria y CPU mayor. En este caso, primero creará un clúster de Kubernetes heterogéneo con diferentes tipos de hardware y, a continuación, [asignar etiquetas de nodo](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) en consecuencia. En el momento de la implementación de clúster de macrodatos, puede especificar las etiquetas de mismas nivel de grupo en el archivo de configuración de implementación de clúster. Kubernetes, a continuación, se encargará de ajustándola los pods en los nodos que coinciden con las etiquetas especificadas.

El ejemplo siguiente muestra cómo editar un archivo de configuración personalizada para incluir un valor de etiqueta de nodo para la instancia principal de SQL Server. Tenga en cuenta que no hay ningún *nodeLabel* clave en las configuraciones integradas, por lo que deberá modificar manualmente un archivo de configuración personalizado o crear un archivo de revisión y se aplican al archivo de configuración personalizada.

Cree un archivo denominado **patch.json** en el directorio actual con el siguiente contenido:

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a id="jsonpatch"></a> Archivos de revisión de JSON

Archivos de revisión de JSON configuran varias opciones de configuración a la vez. Para obtener más información sobre las revisiones JSON, consulte [revisiones de JSON en Python](https://github.com/stefankoegl/python-json-patch) y [JSONPath en línea evaluador](https://jsonpath.com/).

La siguiente **patch.json** archivo lleva a cabo los siguientes cambios:

- Actualiza el puerto del punto de conexión único.
- Actualiza todos los extremos (**puerto** y **serviceType**).
- Actualiza el almacenamiento de plano de control.
- Actualiza el nombre de clase de almacenamiento en el almacenamiento de plano de control.
- Las actualizaciones de grupo de almacenamiento, incluidas las réplicas (bloque de almacenamiento).
- Actualiza la configuración de Spark para un grupo específico (bloque de almacenamiento).

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "ServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "AppServiceProxy"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30443,
            "name": "Knox"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage",
      "value": {
        "usePersistentVolume":true,
        "accessMode":"ReadWriteMany",
        "className":"managed-premium",
        "size":"10Gi"
      }
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.className",
      "value": "default"
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "replicas": 2,
        "type": "Storage",
        "storage": {
          "usePersistentVolume": true,
          "accessMode": "ReadWriteOnce",
          "className": "managed-premium",
          "size": "10Gi"
        }
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
      "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
      }
    }
  ]
}
```

> [!TIP]
> Para obtener más información sobre la estructura y las opciones para cambiar un archivo de configuración de implementación, consulte [referencia del archivo de configuración de implementación para los clústeres de macrodatos](reference-deployment-config.md).

Use **conjunto de sección de configuración de clúster mssqlctl** para aplicar los cambios en el archivo de revisión JSON. El ejemplo siguiente se aplica el **patch.json** archivo a un archivo de configuración de implementación de destino **custom.json**.

```bash
mssqlctl cluster config section set -f custom.json -p ./patch.json
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de archivos de configuración de las implementaciones de clústeres de datos de gran tamaño, vea [de clústeres de cómo implementar grandes de datos de SQL Server en Kubernetes](deployment-guidance.md#configfile).
