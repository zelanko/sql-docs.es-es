---
title: Configurar implementaciones
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo personalizar la implementación de un clúster de Big Data con archivos de configuración.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7559ecf9c7b17ca21c088ed531a347f88e89ee2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419438"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Configuración de las opciones de implementación de clústeres de Big Data

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar los archivos de configuración de implementación de clústeres, puede usar cualquier editor de formato JSON, como VSCode. Para generar scripts para estas ediciones con fines de automatización, use el comando **azdata de configuración de BDC** . En este artículo se explica cómo configurar las implementaciones de clúster de Big Data mediante la modificación de los archivos de configuración de implementación. Proporciona ejemplos sobre cómo cambiar la configuración de distintos escenarios. Para obtener más información sobre cómo se usan los archivos de configuración en las implementaciones, vea la [Guía de implementación](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Requisitos previos

- [Instale azdata](deploy-install-azdata.md).

- En cada uno de los ejemplos de esta sección se supone que ha creado una copia de una de las configuraciones estándar. Para obtener más información, consulte [crear una configuración personalizada](deployment-guidance.md#customconfig). Por ejemplo, el siguiente comando crea un directorio denominado `custom` que contiene dos archivos de configuración de implementación JSON, **cluster. JSON** y **control. JSON**, basados en la configuración predeterminada de **AKS-dev-test** :

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a>Cambiar el nombre del clúster

El nombre del clúster es el nombre del clúster de Big Data y el espacio de nombres Kubernetes que se creará en la implementación. Se especifica en la siguiente parte del archivo de configuración de implementación **cluster. JSON** :

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

El comando siguiente envía un par clave-valor al parámetro **--JSON-** Values para cambiar el nombre del clúster de Big Data a **Test-Cluster**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> El nombre del clúster de Big Data debe ser solo caracteres alfanuméricos en minúsculas, sin espacios. Todos los artefactos de Kubernetes (contenedores, pods, conjuntos de con estado, servicios) para el clúster se crearán en un espacio de nombres con el mismo nombre que el nombre de clúster especificado.

## <a id="ports"></a>Actualizar puertos de extremo

Los puntos de conexión se definen para el controlador en el archivo **control. JSON** y para la puerta de enlace y SQL Server instancia maestra en las secciones correspondientes en **cluster. JSON**. La siguiente parte del archivo de configuración **control. JSON** muestra las definiciones de punto de conexión para el controlador:

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
    }
]
```

En el ejemplo siguiente se usa JSON en línea para cambiar el puerto del punto de conexión del **controlador** :

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a>Configurar réplicas de grupo

Las características de cada grupo, como el grupo de almacenamiento, se definen en el archivo de configuración de **cluster. JSON** . Por ejemplo, la siguiente parte de **cluster. JSON** muestra una definición de grupo de almacenamiento:

```json
"pools": [
   {
       "metadata": {
           "kind": "Pool",
           "name": "default"
       },
       "spec": {
           "type": "Storage",
           "replicas": 2
       }
   }
]
```

Puede configurar el número de instancias de un grupo modificando el valor de  las réplicas de cada grupo. En el ejemplo siguiente se usa JSON en línea para cambiar estos valores para el almacenamiento y los `10` grupos `4` de datos a y, respectivamente:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a>Configurar el almacenamiento

También puede cambiar la clase de almacenamiento y las características que se usan para cada grupo. En el ejemplo siguiente se asigna una clase de almacenamiento personalizada al bloque de almacenamiento y se actualiza el tamaño de la demanda de volumen persistente para almacenar los datos en 100 GB. En primer lugar, cree un archivo patch. JSON como el que se muestra a continuación, que incluye la nueva sección de *almacenamiento* , además del *tipo* y las *réplicas* .

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
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
                },
        "type":"Storage",
        "replicas":2
      }
    }
  ]
}
```

Después, puede usar el comando azdata de configuración de **BDC** para actualizar el archivo de configuración de **cluster. JSON** .
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> Un archivo de configuración basado en **kubeadm-dev-test** no tiene una definición de almacenamiento para cada grupo, pero puede usar el proceso anterior para agregarlo si es necesario.

Para más información sobre la configuración del almacenamiento, consulte [persistencia de datos con SQL Server clúster de macrodatos en Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a>Configuración del bloque de almacenamiento sin Spark

También puede configurar los grupos de almacenamiento para que se ejecuten sin Spark y crear un grupo de Spark independiente. Esto le permite escalar la potencia de proceso de Spark independientemente del almacenamiento. Para ver cómo configurar el grupo de Spark, consulte el [ejemplo de archivo de revisión de JSON](#jsonpatch) al final de este artículo.



De forma predeterminada, la configuración **includeSpark** para el grupo de almacenamiento está establecida en true, por lo que debe agregar el campo **includeSpark** a la configuración de almacenamiento para realizar cambios. El siguiente archivo de revisión JSON muestra cómo agregar este.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "includeSpark":false
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

## <a id="podplacement"></a>Configuración de la selección de ubicación Pod mediante etiquetas Kubernetes

Puede controlar la colocación de Pod en nodos de Kubernetes que tienen recursos específicos para acomodar varios tipos de requisitos de carga de trabajo. Por ejemplo, puede que desee asegurarse de que los pods del grupo de almacenamiento se colocan en los nodos con más almacenamiento o SQL Server instancias maestras se colocan en los nodos que tienen más recursos de CPU y memoria. En este caso, primero creará un clúster de Kubernetes heterogéneo con distintos tipos de hardware y, a continuación, [asignará etiquetas de nodo](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) en consecuencia. En el momento de implementar el clúster de Big Data, puede especificar las mismas etiquetas en el nivel de grupo del archivo de configuración de implementación de clúster. A continuación, Kubernetes se encargará de estableciendo los pods en los nodos que coincidan con las etiquetas especificadas.

En el ejemplo siguiente se muestra cómo editar un archivo de configuración personalizado para incluir una configuración de etiqueta de nodo para la instancia de SQL Server Master. Tenga en cuenta que no hay ninguna clave *nodeLabel* en las configuraciones integradas, por lo que tendrá que editar manualmente un archivo de configuración personalizado o crear un archivo de revisión y aplicarlo al archivo de configuración personalizada.

Cree un archivo denominado **patch. JSON** en el directorio actual con el siguiente contenido:

```json
{
  "patch": [
     {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
           "type": "Master",
         "replicas": 1,
         "hadrEnabled": false,
         "endpoints": [
            {
             "name": "Master",
             "serviceType": "NodePort",
             "port": 31433
            }
          ],
         "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a>Archivos de revisión de JSON

Los archivos de revisión de JSON configuran varias opciones a la vez. Para obtener más información sobre las revisiones de JSON, consulte [revisiones de JSON en Python](https://github.com/stefankoegl/python-json-patch) y el [evaluador en línea de JSONPath](https://jsonpath.com/).

El archivo **patch. JSON** siguiente realiza los siguientes cambios:

- Actualiza el puerto del punto de conexión único en **control. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.endpoints[?(@.name=='Controller')].port",
          "value": 30000
        }   
      ]
    }
    ```

- Actualiza todos los puntos de conexión (**Port** y **serviceType**) en **control. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.endpoints",
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
        }
          ]
        }
      ]
    }
    ```

- Actualiza la configuración de almacenamiento del controlador en **control. JSON**. Esta configuración se aplica a todos los componentes del clúster, a menos que se invalide en el nivel de grupo.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage",
          "value": {
          "data": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
        }   
      ]
    }
    ```

- Actualiza el nombre de la clase de almacenamiento en **control. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage.data.className",
          "value": "managed-premium"
        }   
      ]
    }
    ```

- Actualiza la configuración de almacenamiento del grupo de almacenamiento en **cluster. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
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

- Actualiza la configuración de Spark para el grupo de almacenamiento en **cluster. JSON**.
    ```json
    {
      "patch": [
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

- Crea un grupo de Spark con dos instancias en **cluster. JSON**.
    ```json
    {
      "patch": [
        {
          "op": "add",
          "path": "spec.pools/-",
          "value":
          {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": 12288,
              "vcores": 6
            },
            "schedulerMax": {
              "memory": 12288,
              "vcores": 6
            },
            "capacityScheduler": {
              "maxAmPercent": 0.3
            }
          },
          "spark": {
            "driverMemory": "2g",
            "driverCores": 1,
            "executorInstances": 2,
            "executorMemory": "2g",
            "executorCores": 1
          }
        }
          }
        } 
      ]
    }
    ```



> [!TIP]
> Para obtener más información sobre la estructura y las opciones para cambiar un archivo de configuración de implementación, vea [Referencia del archivo de configuración de implementación para clústeres de Big Data](reference-deployment-config.md).

Use los comandos de **configuración de BDC de azdata** para aplicar los cambios en el archivo de revisión de JSON. En el ejemplo siguiente se aplica el archivo **patch. JSON** a un archivo de configuración de implementación de destino **Custom/cluster. JSON**.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de archivos de configuración en implementaciones de clúster de Big Data, consulte [cómo implementar clústeres de macrodatos SQL Server en Kubernetes](deployment-guidance.md#configfile).
