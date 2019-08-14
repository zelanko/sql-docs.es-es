---
title: Configuración de implementaciones
titleSuffix: SQL Server big data clusters
description: Aprenda a personalizar una implementación de clúster de macrodatos con archivos de configuración.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7d04df5bf881f285ab28508443fbf0ce1056fada
ms.sourcegitcommit: 316c25fe7465b35884f72928e91c11eea69984d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2019
ms.locfileid: "68969491"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>Configuración de opciones de implementación para clústeres de macrodatos

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Para personalizar los archivos de configuración de implementación de clústeres, puede usar cualquier editor de formato JSON, como VSCode. Para generar scripts de estas ediciones con fines de automatización, use el comando **azdata bdc config**. En este artículo se explica cómo configurar las implementaciones de clústeres de macrodatos mediante la modificación de los archivos de configuración de implementación. Se proporcionan ejemplos sobre cómo cambiar la configuración de distintos escenarios. Para obtener más información sobre cómo se usan los archivos de configuración en las implementaciones, vea la [guía de implementación](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Requisitos previos

- [Instalación de azdata](deploy-install-azdata.md).

- En cada uno de los ejemplos de esta sección se supone que ha creado una copia de una de las configuraciones estándar. Para obtener más información, vea [Creación de una configuración personalizada](deployment-guidance.md#customconfig). Por ejemplo, el siguiente comando crea un directorio denominado `custom` que contiene dos archivos de configuración de implementación JSON, **cluster.json** y **control.json**, basados en la configuración predeterminada **aks-dev-test**:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Cambio del nombre del clúster

El nombre del clúster es tanto el nombre del clúster de macrodatos como el espacio de nombres de Kubernetes que se van a crear al implementar. Se especifica en la siguiente parte del archivo de configuración de implementación **cluster.json**:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

El comando siguiente envía un par clave-valor al parámetro **--json-values** para cambiar el nombre del clúster de macrodatos a **test-cluster**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> El nombre del clúster de macrodatos debe estar formado solo por caracteres alfanuméricos en minúsculas sin espacios. Todos los artefactos de Kubernetes (contenedores, pods, conjuntos con estado, servicios) para el clúster se crean en un espacio de nombres con el mismo nombre que el nombre de clúster especificado.

## <a id="ports"></a> Actualización de los puertos de puntos de conexión

Los puntos de conexión se definen para el controlador de **control.json** y para la puerta de enlace y la instancia maestra de SQL Server de las secciones correspondientes de **cluster.json**. La siguiente parte del archivo de configuración **control.json** muestra las definiciones de puntos de conexión para el controlador:

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

En el ejemplo siguiente se usa JSON en línea para cambiar el puerto del punto de conexión del **controlador**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configuración de réplicas de grupos

Las características de cada grupo, como el bloque de almacenamiento, se definen en el archivo de configuración **cluster.json**. Por ejemplo, la siguiente parte de **cluster.json** muestra una definición de bloque de almacenamiento:

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

Puede configurar el número de instancias de un grupo si modifica el valor **replicas** de cada grupo. En el ejemplo siguiente se usa JSON en línea para cambiar estos valores para el bloque de almacenamiento y el grupo de datos a `10` y `4` respectivamente:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> Configuración del almacenamiento

También puede cambiar la clase de almacenamiento y las características que se usan para cada grupo. En el ejemplo siguiente se asigna una clase de almacenamiento personalizada al bloque de almacenamiento y se actualiza el tamaño de la notificación de volumen persistente para almacenar datos de hasta 100 GB. En primer lugar, cree un archivo patch.json como el de abajo, que incluye la nueva sección *storage*, además de *type* y *replicas*.

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

Luego puede usar el comando **azdata bdc config patch** para actualizar el archivo de configuración **cluster.json**.
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> Un archivo de configuración basado en **kubeadm-dev-test** no tiene una definición de almacenamiento para cada grupo, pero puede usar el proceso anterior para agregarla si fuese necesario.

Para obtener más información sobre la configuración de almacenamiento, vea [Persistencia de datos con clústeres de macrodatos de SQL Server en Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configuración del bloque de almacenamiento sin Spark

También puede configurar los bloques de almacenamiento para que se ejecuten sin Spark y crear un grupo de Spark independiente. Esto le permite escalar la potencia de proceso de Spark independientemente del almacenamiento. Para ver cómo se configura el grupo de Spark, vea el [ejemplo de archivo de revisión JSON](#jsonpatch) al final de este artículo.



De forma predeterminada, el valor **includeSpark** del bloque de almacenamiento está establecido en true, por lo que debe agregar el campo **includeSpark** a la configuración de almacenamiento para realizar cambios. El siguiente archivo de revisión JSON muestra cómo agregarlo.

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

## <a id="podplacement"></a> Configuración de la ubicación de pods mediante etiquetas de Kubernetes

Puede controlar la ubicación de pods en nodos de Kubernetes con recursos específicos para acomodar varios tipos de requisitos de carga de trabajo. Por ejemplo, es posible que quiera asegurarse de que los pods del bloque de almacenamiento se colocan en nodos con más almacenamiento o de que las instancias maestras de SQL Server se colocan en nodos con más recursos de CPU y memoria. En este caso, primero crea un clúster de Kubernetes heterogéneo con distintos tipos de hardware y luego [asigna etiquetas de nodo](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) en consecuencia. En el momento de implementar el clúster de macrodatos, puede especificar las mismas etiquetas en el nivel de grupo del archivo de configuración de implementación de clúster. Luego Kubernetes se encarga de ajustar los pods en los nodos que coinciden con las etiquetas especificadas. La clave de etiqueta específica que debe agregarse a los nodos del clúster de kubernetes es **MSSQL-Cluster-Wide**. El valor de esta etiqueta puede ser cualquier cadena que elija.

En el ejemplo siguiente se muestra cómo editar un archivo de configuración personalizado para incluir una configuración de etiqueta de nodo para la SQL Server instancia maestra, grupo de procesos, grupo de datos & grupo de almacenamiento. Observe que no hay ninguna clave *nodeLabel* en las configuraciones integradas, por lo que tiene que editar manualmente un archivo de configuración personalizado o crear un archivo de revisión y aplicarlo al archivo de configuración personalizado. El pod de la instancia principal de SQL Server se implementará en un nodo que contenga una etiqueta **MSSQL-Cluster-Wide** con el valor **BDC-Master**. El grupo de proceso y los pods del grupo de datos se implementarán en los nodos que contengan una etiqueta **MSSQL-Cluster-Wide** con valor **BDC-SQL**. Los pods del bloque de almacenamiento se implementarán en los nodos que contengan una etiqueta **MSSQL-Cluster-Wide** con valor **BDC-Storage**.

Cree un archivo denominado **patch.json** en el directorio actual con el siguiente contenido:

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
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Compute')].spec",
      "value": {
    "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Data')].spec",
      "value": {
    "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
    "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage"
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a> Archivos de revisión JSON

Los archivos de revisión JSON configuran varias opciones a la vez. Para obtener más información sobre las revisiones de JSON, vea [Revisiones de JSON en Python](https://github.com/stefankoegl/python-json-patch) y [JSONPath Online Evaluator](https://jsonpath.com/).

El siguiente archivo **patch.json** realiza estos cambios:

- Actualiza el puerto del punto de conexión único de **control.json**.
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

- Actualiza todos los puntos de conexión (**port** y **serviceType**) de **control.json**.
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

- Actualiza la configuración de almacenamiento del controlador de **control.json**. Esta configuración se aplica a todos los componentes del clúster, a menos que se invalide en el nivel de grupo.
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

- Actualiza el nombre de la clase de almacenamiento de **control.json**.
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

- Actualiza la configuración de almacenamiento de grupo del bloque de almacenamiento de **cluster.json**.
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

- Actualiza la configuración de Spark del bloque de almacenamiento de **cluster.json**.
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

- Crea un grupo de Spark con dos instancias en **cluster.json**.
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
> Para obtener más información sobre la estructura y las opciones para cambiar un archivo de configuración de implementación, vea [Referencia del archivo de configuración de implementación para los clústeres de datos de gran tamaño](reference-deployment-config.md).

Use los comandos de **azdata bdc config** para aplicar los cambios al archivo de revisión JSON. En el ejemplo siguiente se aplica el archivo **patch.json** a un archivo de configuración de implementación de destino **custom/cluster.json**.

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de archivos de configuración en implementaciones de clústeres de macrodatos, vea [Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md#configfile).
