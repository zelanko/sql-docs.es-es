---
title: Configuración de implementaciones
titleSuffix: SQL Server big data clusters
description: Aprenda a personalizar una implementación de clúster de macrodatos con archivos de configuración.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 31c745a585adf26b521054cbcd0234fd4087a114
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542173"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>Configurar las opciones de implementación de los recursos y servicios de clúster

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

A partir de un conjunto predefinido de perfiles de configuración que se integran en la herramienta de administración de azdata, puede modificar fácilmente la configuración predeterminada para satisfacer mejor sus requisitos de carga de trabajo de BDC. A partir de la versión Release Candidate, la estructura de los archivos de configuración se actualizó para permitir la actualización granular de la configuración de cada servicio del recurso. 

También puede establecer configuraciones de nivel de recurso o actualizar las configuraciones de todos los servicios de un recurso. A continuación se muestra un resumen de la estructura de **BDC. JSON**:

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

Para actualizar las configuraciones de nivel de recurso como las instancias de un grupo, actualizará la especificación de recursos. Por ejemplo, para actualizar el número de instancias en el grupo de proceso, se modificará esta sección en el archivo de configuración **BDC. JSON** :
```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

De igual forma, para cambiar la configuración de un único servicio dentro de un recurso específico. Por ejemplo, si desea cambiar la configuración de memoria de Spark solo para el componente de Spark en el grupo de almacenamiento, actualizará el recurso **Storage-0** con una sección de **configuración** para el servicio **Spark** en el archivo de configuración **BDC. JSON.** .
```json
"resources":{
    ...
     "storage-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "settings": {
                "spark": {
                    "driverMemory": "2g",
                    "driverCores": "1",
                    "executorInstances": "3",
                    "executorMemory": "1536m",
                    "executorCores": "1"
                }
            }
        }
    }
    ...
}
```

Si desea aplicar la misma configuración a un servicio asociado a varios recursos, actualizará los **valores** correspondientes en la sección **servicios** . Por ejemplo, si desea establecer la misma configuración para Spark en el grupo de almacenamiento y en los grupos de Spark, actualizará la sección de **configuración** en la sección servicio **Spark** del archivo de configuración **BDC. JSON** .

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "driverMemory": "2g",
            "driverCores": "1",
            "executorInstances": "3",
            "executorMemory": "1536m",
            "executorCores": "1"
        }
    }
    ...
}
```


Para personalizar los archivos de configuración de implementación de clústeres, puede usar cualquier editor de formato JSON, como VSCode. Para generar scripts de estas ediciones con fines de automatización, use el comando **azdata bdc config**. En este artículo se explica cómo configurar las implementaciones de clústeres de macrodatos mediante la modificación de los archivos de configuración de implementación. Se proporcionan ejemplos sobre cómo cambiar la configuración de distintos escenarios. Para obtener más información sobre cómo se usan los archivos de configuración en las implementaciones, vea la [guía de implementación](deployment-guidance.md#configfile).

## <a name="prerequisites"></a>Prerequisites

- [Instalación de azdata](deploy-install-azdata.md).

- En cada uno de los ejemplos de esta sección se supone que ha creado una copia de una de las configuraciones estándar. Para obtener más información, vea [Creación de una configuración personalizada](deployment-guidance.md#customconfig). Por ejemplo, el siguiente comando crea un directorio denominado `custom` que contiene dos archivos de configuración de implementación JSON, **BDC. JSON** y **control. JSON**, basados en la configuración predeterminada de **AKS-dev-test** :

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> Cambio del nombre del clúster

El nombre del clúster es tanto el nombre del clúster de macrodatos como el espacio de nombres de Kubernetes que se van a crear al implementar. Se especifica en la siguiente parte del archivo de configuración de implementación de **BDC. JSON** :

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

El comando siguiente envía un par clave-valor al parámetro **--json-values** para cambiar el nombre del clúster de macrodatos a **test-cluster**:

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> El nombre del clúster de macrodatos debe estar formado solo por caracteres alfanuméricos en minúsculas sin espacios. Todos los artefactos de Kubernetes (contenedores, pods, conjuntos con estado, servicios) para el clúster se crean en un espacio de nombres con el mismo nombre que el nombre de clúster especificado.

## <a id="ports"></a> Actualización de los puertos de puntos de conexión

Los puntos de conexión se definen para el controlador en el archivo **control. JSON** y para la puerta de enlace y SQL Server instancia maestra en las secciones correspondientes de **BDC. JSON**. La siguiente parte del archivo de configuración **control.json** muestra las definiciones de puntos de conexión para el controlador:

```json
{
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
}
```

En el ejemplo siguiente se usa JSON en línea para cambiar el puerto del punto de conexión del **controlador**:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> Configuración de réplicas de grupos

Las configuraciones de cada recurso, como el grupo de almacenamiento, se definen en el archivo de configuración **BDC. JSON** . Por ejemplo, la siguiente parte del archivo **BDC. JSON** muestra una definición de recursos **Storage-0** :

```json
"storage-0": {
    "metadata": {
        "kind": "Pool",
        "name": "default"
    },
    "spec": {
        "type": "Storage",
        "replicas": 2,
        "settings": {
            "spark": {
                "driverMemory": "2g",
                "driverCores": "1",
                "executorInstances": "3",
                "executorMemory": "1536m",
                "executorCores": "1"
            }
        }
    }
}
```

Puede configurar el número de instancias de un grupo si modifica el valor **replicas** de cada grupo. En el ejemplo siguiente se usa JSON en línea para cambiar estos valores para el bloque de almacenamiento y el grupo de datos a `10` y `4` respectivamente:

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

## <a id="storage"></a> Configuración del almacenamiento

También puede cambiar la clase de almacenamiento y las características que se usan para cada grupo. En el ejemplo siguiente se asigna una clase de almacenamiento personalizada al almacenamiento y a los grupos de datos y se actualiza el tamaño de la demanda de volumen persistente para almacenar datos en 500 GB para HDFS (bloque de almacenamiento) y 100 GB para el grupo de datos. En primer lugar, cree un archivo patch.json como el de abajo, que incluye la nueva sección *storage*, además de *type* y *replicas*.

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "500Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myHDFSStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myDataStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

Después, puede usar el comando azdata de configuración de **BDC** para actualizar el archivo de configuración de **BDC. JSON** .
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json
```

> [!NOTE]
> Un archivo de configuración basado en **kubeadm-dev-test** no tiene una definición de almacenamiento para cada grupo, pero puede usar el proceso anterior para agregarla si fuese necesario.

Para obtener más información sobre la configuración de almacenamiento, vea [Persistencia de datos con clústeres de macrodatos de SQL Server en Kubernetes](concept-data-persistence.md).

## <a id="sparkstorage"></a> Configuración del bloque de almacenamiento sin Spark

También puede configurar los bloques de almacenamiento para que se ejecuten sin Spark y crear un grupo de Spark independiente. Esto le permite escalar la potencia de proceso de Spark independientemente del almacenamiento. Para ver cómo se configura el grupo de Spark, vea el [ejemplo de archivo de revisión JSON](#jsonpatch) al final de este artículo.


De forma predeterminada, el valor **includeSpark** para el recurso del grupo de almacenamiento se establece en true, por lo que debe editar el campo **includeSpark** en la configuración del almacenamiento para realizar cambios. El siguiente comando muestra cómo editar este valor mediante JSON en línea.

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="podplacement"></a> Configuración de la ubicación de pods mediante etiquetas de Kubernetes

Puede controlar la ubicación de pods en nodos de Kubernetes con recursos específicos para acomodar varios tipos de requisitos de carga de trabajo. Por ejemplo, puede que desee asegurarse de que los pods de recursos del grupo de almacenamiento se colocan en los nodos con más almacenamiento o SQL Server instancias maestras se colocan en los nodos que tienen más recursos de CPU y memoria. En este caso, primero crea un clúster de Kubernetes heterogéneo con distintos tipos de hardware y luego [asigna etiquetas de nodo](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/) en consecuencia. En el momento de implementar el clúster de macrodatos, puede especificar las mismas etiquetas en el nivel de grupo del archivo de configuración de implementación de clúster. Luego Kubernetes se encarga de ajustar los pods en los nodos que coinciden con las etiquetas especificadas. La clave de etiqueta específica que debe agregarse a los nodos del clúster de kubernetes es **MSSQL-Cluster-Wide**. El valor de esta etiqueta puede ser cualquier cadena que elija.

En el ejemplo siguiente se muestra cómo editar un archivo de configuración personalizado para incluir una configuración de etiqueta de nodo para la SQL Server instancia maestra, grupo de procesos, grupo de datos & grupo de almacenamiento. No hay ninguna clave *nodeLabel* en las configuraciones integradas, por lo que tendrá que editar manualmente un archivo de configuración personalizado o crear un archivo de revisión y aplicarlo al archivo de configuración personalizado. El pod de la instancia principal de SQL Server se implementará en un nodo que contenga una etiqueta **MSSQL-Cluster-Wide** con el valor **BDC-Master**. El grupo de proceso y los pods del grupo de datos se implementarán en los nodos que contengan una etiqueta **MSSQL-Cluster-Wide** con valor **BDC-SQL**. Los pods del bloque de almacenamiento se implementarán en los nodos que contengan una etiqueta **MSSQL-Cluster-Wide** con valor **BDC-Storage**.

Cree un archivo denominado **patch.json** en el directorio actual con el siguiente contenido:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.master.spec",
      "value": {
        "type": "Master",
        "replicas": 1,
        "endpoints": [
          {
            "name": "Master",
            "serviceType": "NodePort",
            "port": 31433
          }
        ],
        "settings": {
          "sql": {
            "hadr.enabled": "false"
          }
        },
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.compute-0.spec",
      "value": {
        "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage",
        "settings": {
          "spark": {
            "includeSpark": "true"
          }
        }
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
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

- Actualiza la configuración de almacenamiento del grupo de almacenamiento en **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- Actualiza la configuración de Spark para el grupo de almacenamiento en **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
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

- Crea un grupo de Spark con dos instancias en **BDC. JSON**.
```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.resources.spark-0",
      "value": {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        }
      }
    },
    {
      "op": "add",
      "path": "spec.services.spark.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.hdfs.resources/-",
      "value": "spark-0"
    }
   }
  ]
}
```

> [!TIP]
> Para obtener más información sobre la estructura y las opciones para cambiar un archivo de configuración de implementación, vea [Referencia del archivo de configuración de implementación para los clústeres de datos de gran tamaño](reference-deployment-config.md).

Use los comandos de **azdata bdc config** para aplicar los cambios al archivo de revisión JSON. En el ejemplo siguiente se aplica el archivo **patch. JSON** a un archivo de configuración de implementación de destino **Custom/BDC. JSON**.

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>Deshabilitar ElasticSearch para que se ejecute en modo privilegiado
De forma predeterminada, el contenedor ElasticSearch se ejecuta en modo de privilegio en el clúster de Big Data. Esto se hace para asegurarse de que, en el momento de la inicialización del contenedor, el contenedor tiene permisos suficientes para actualizar una configuración en el host necesaria cuando ElasticSearch procesa una mayor cantidad de registros. Puede encontrar más información sobre este tema en [este artículo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html). 

Para deshabilitar el contenedor que ejecuta ElasticSearch para que se ejecute en modo privilegiado, debe actualizar la sección de **configuración** en **control. JSON** y especificar el valor de **VM. Max _map_count** en **-1**. Este es un ejemplo de cómo sería esta sección:
```json
"settings": {
    "ElasticSearch": {
        "vm.max_map_count": "-1"
      }
}
```

Puede modificar manullly edite el archivo **control. JSON** y agregar la sección anterior a la **especificación**, o bien puede crear un archivo **de revisión elasticsearch-patch. JSON** como el siguiente y usar la CLI de **azdata** para revisar el archivo **control. JSON** :

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec",
      "value": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-RC1-ubuntu",
            "imagePullPolicy": "Always"
        },
        "storage": {
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
        },
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
        ],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
             }
        }
       }
    }
  ]
}
```

Ejecute este comando para aplicar una revisión al archivo de configuración:
```
azdata bdc config patch --config-file control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> Se recomienda como procedimiento recomendado actualizar manualmente el valor de **max_map_count** en cada host del clúster de Kubernetes según las instrucciones de [este artículo](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html).
## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de archivos de configuración en implementaciones de clúster de Big Data, consulte [cómo implementar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md#configfile).
