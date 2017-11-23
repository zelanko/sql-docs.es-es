---
title: Objeto de particiones (TMSL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: df1da0d2-d824-42ba-b9dc-47fbd8edc10f
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6ea3c1f7486caa923bcf5cfc07d83a65e76578e5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="partitions-object-tmsl"></a>Objeto de particiones (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Define una partición, o una segmentación lógica del conjunto de filas de tabla. Una partición está formada por una consulta SQL usada para la importación de datos para datos de ejemplo en el entorno de modelado, o como una consulta de datos completa para pasar a través de la ejecución de consultas mediante DirectQuery.  
  
 Las propiedades de la partición determinan cómo se generan los datos de la tabla.  En la jerarquía de objetos, el objeto primario de una partición es un objeto de tabla.  
  
## <a name="object-definition"></a>Definición del objeto  
 Todos los objetos tienen un conjunto común de propiedades, incluidos el nombre, tipo, descripción, una colección de propiedades y las anotaciones. **Partición** objetos también tienen las siguientes propiedades.  
  
 Tipo  
 El tipo de partición. Los valores válidos son numéricos e incluyen lo siguiente:  
  
-   Consulta (1): datos de esta partición se recupera al ejecutar una consulta en un **DataSource**. El **DataSource** debe ser un origen de datos definido en el archivo model.bim.  
  
-   Calculado (2): los datos en esta partición se rellenan mediante la ejecución de una expresión calculada.  
  
-   Ninguno (3) – datos en esta partición se rellena mediante la inserción de un conjunto de filas de datos al servidor como parte de la operación de actualización.  
  
 mode  
 Define el modo de consulta de la partición. Los valores válidos son **importar**, **DirectQuery**, o **predeterminado** (heredado). Este valor es necesario.  
  
|||  
|-|-|  
|**Importar**|Indica que las solicitudes se emiten en el motor de análisis en memoria almacenar los datos importados de consulta.|  
|**DirectQuery**|Pasar a través de la ejecución de la consulta a una base de datos relacional externa. El modo DirectQuery utiliza particiones para proporcionar datos de ejemplo utilizados durante el diseño del modelo. Cuando se implementa en un servidor de producción, debe cambiar a vista de datos completa. Recuerde que el modo DirectQuery requiere una partición por tabla y un origen de datos por el modelo.|  
|**valor predeterminado**|Establezca esto si desea cambiar los modos superiores del árbol de objetos, en el nivel de modelo o base de datos. Cuando se elige de forma predeterminada, el modo de consulta será import o DirectQuery.|  
  
 origen  
 Identifica la ubicación de los datos que se va a consultar. Los valores válidos son **consulta, calculado**, o **ninguno**. Este valor es necesario.  
  
|||  
|-|-|  
|**Ninguno**|Se utiliza para el modo de importación, donde los datos se cargan y almacenan en la memoria.|  
|**consulta**|Para el modo DirectQuery, trata de una consulta SQL que se ejecuta en la base de datos relacional especificado en el modelo **DataSource**. Vea [orígenes de datos de objeto &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md).|  
|**calcula**|Las tablas calculadas se obtienen de una expresión que se especificó cuando se creó la tabla. Esta expresión se considera el origen de la partición creada para la tabla calculada.|  
  
 DataView  
 Para las particiones de DirectQuery, una propiedad de dataView adicionales más especifica si la consulta que recupera los datos es un ejemplo o el conjunto de datos completo. Los valores válidos son **completa**, **ejemplo**, o **predeterminado** (heredado). Como se indicó, ejemplos se utilizan solo durante el modelado de datos y pruebas. Vea [agregar datos de ejemplo con un modelo de DirectQuery en modo de diseño](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) para obtener más información.  
  
## <a name="usage"></a>Uso  
 Objetos de partición se usan en [Alter comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [Crear comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [Eliminar comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [Actualizar comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), y [MergePartitions comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 Al crear, reemplazar o modificar un objeto de partición, especifique todas las propiedades de lectura y escritura de la definición del objeto. Omisión de una propiedad de lectura y escritura se considera una operación de eliminación. Propiedades de lectura y escritura incluyen nombre, descripción, modo y origen.  
  
## <a name="examples"></a>Ejemplos  
 **Ejemplo 1** -una estructura de partición simple de una tabla (no una tabla de hechos).  
  
```  
"partitions": [  
          {  
            "name": "Customer",  
            "source": {  
              "query": "SELECT [dbo].[Customer].* FROM [dbo].[Customer]",  
              "dataSource": "SqlServer localhost FoodmartDB"  
            }  
]  
```  
  
 **Ejemplo 2** : con particiones datos de hechos normalmente se basan en una cláusula WHERE que crea particiones no superpuestas para los datos de la misma tabla.  
  
```  
"partitions": [  
          {  
            "name": "sales_fact_2015",  
            "source": {  
              "query": "SELECT [dbo].[sales_fact_2015].* FROM [dbo].[sales_fact_2015] WHERE [dbo].[sales_fact_2015].[Quarter]=4",                                                                                          
              "dataSource": "SqlServer localhost FoodmartDB"  
            },  
          }  
        ]  
```  
  
 **Ejemplo 3** -una tabla calculada en función de una expresión de DAX.  
  
```  
"partitions": [  
          {  
            "name": "CalcTable1",  
            "source": {  
              "type": "calculated",  
              "expression": "'Product Class'"  
            },  
            }  
]  
```  
  
## <a name="full-syntax"></a>Sintaxis completa  
 A continuación se muestra la representación de esquema de un objeto de partición.  
  
```  
"partitions": {  
                "type": "array",  
                "items": {  
                  "description": "Partition object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
                      "anyOf": [  
                        {  
                          "type": "string"  
                        },  
                        {  
                          "type": "array",  
                          "items": {  
                            "type": "string"  
                          }  
                        }  
                      ]  
                    },  
                    "mode": {  
                      "enum": [  
                        "import",  
                        "directQuery",  
                        "default"  
                      ]  
                    },  
                    "dataView": {  
                      "enum": [  
                        "full",  
                        "sample",  
                        "default"  
                      ]  
                    },  
                    "source": {  
                      "anyOf": [  
                        {  
                          "description": "QueryPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "query": {  
                              "anyOf": [  
                                {  
                                  "type": "string"  
                                },  
                                {  
                                  "type": "array",  
                                  "items": {  
                                    "type": "string"  
                                  }  
                                }  
                              ]  
                            },  
                            "dataSource": {  
                              "type": "string"  
                            }  
                          },  
                          "additionalProperties": false  
                        },  
                        {  
                          "description": "CalculatedPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "expression": {  
                              "anyOf": [  
                                {  
                                  "type": "string"  
                                },  
                                {  
                                  "type": "array",  
                                  "items": {  
                                    "type": "string"  
                                  }  
                                }  
                              ]  
                            }  
                          },  
                          "additionalProperties": false  
                        }  
                      ]  
                    },  
                    "annotations": {  
                      "type": "array",  
                      "items": {  
                        "description": "Annotation object of Tabular Object Model (TOM)",  
                        "type": "object",  
                        "properties": {  
                          "name": {  
                            "type": "string"  
                          },  
                          "value": {  
                            "anyOf": [  
                              {  
                                "type": "string"  
                              },  
                              {  
                                "type": "array",  
                                "items": {  
                                  "type": "string"  
                                }  
                              }  
                            ]  
                          }  
                        },  
                        "additionalProperties": false  
                      }  
                    }  
                  },  
                  "additionalProperties": false  
                }  
              },  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
