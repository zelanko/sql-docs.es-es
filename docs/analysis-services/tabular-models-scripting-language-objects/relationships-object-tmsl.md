---
title: Objeto de relaciones (TMSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 7588565f-ea34-4402-8be9-331188bdb8c2
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 77fc17b6a92976452b3f94a88aafbb115a3167ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="relationships-object-tmsl"></a>Objeto de relaciones (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Define una relación entre una tabla de origen y de destino, con la capacidad de especificar la cardinalidad y la dirección de los filtros de consulta y seguridad.  
  
## <a name="object-definition"></a>Definición del objeto  
 Todos los objetos tienen un conjunto común de propiedades, incluidos el nombre, tipo, descripción, una colección de propiedades y las anotaciones. **Relación** objetos también tienen las siguientes propiedades.  
  
 isActive  
 Un valor booleano que indica si la relación se marca como activo o inactivo. Se usa automáticamente una relación activa para filtrar entre tablas. Las relaciones inactivas se pueden usar expresamente en los cálculos de DAX con la función USERELATIONSHIP.  
  
 crossFilteringBehavior  
 Indica cómo influyen las relaciones en el filtrado de datos. Vea [bidireccional entre los filtros para los modelos tabulares en SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) para obtener más información. Los valores válidos son los siguientes:  
  
-   OneDirection (1): las filas seleccionadas en el extremo "To" de la relación filtran automáticamente recorridos de la tabla en el extremo "From" de la relación.  
  
-   BothDirections (2): los filtros en cualquiera de los extremos de la relación filtran automáticamente la otra tabla.  
  
-   Automático (3): el motor analizará las relaciones y elegir uno de los comportamientos mediante heurística.  
  
 joinOnDateBehavior  
 Al combinar dos columnas de fecha y hora, indica si se deben unir en partes de fecha y hora o solo la parte de fecha.  
  
-   DateAndTime (1): al unir dos columnas fecha y hora, combine partes de fecha y hora.  
  
-   DatePartOnly (2): al unir dos columnas fecha y hora, combine solo la parte de fecha.  
  
 relyOnReferentialIntegrity  
 Unused: reservado para uso futuro.  
  
 securityFilteringBehavior  
 Una enumeración que indica cómo influyen las relaciones en el filtrado de datos al evaluar expresiones de seguridad de nivel de fila. Los valores válidos son los siguientes:  
  
-   OneDirection (1): las filas seleccionadas en el extremo "To" de la relación filtran automáticamente recorridos de la tabla en el extremo "From" de la relación.  
  
-   BothDirections (2): los filtros en cualquiera de los extremos de la relación filtran automáticamente la otra tabla.  
  
## <a name="usage"></a>Uso  
 Objetos de la relación se utilizan en [Alter, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [crear comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [comando CreateOrReplace &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), y [comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md).  
  
 Al crear, reemplazar o modificar un objeto de relación, especifique todas las propiedades de lectura y escritura de la definición del objeto. Omisión de una propiedad de lectura y escritura se considera una operación de eliminación.  
  
## <a name="full-syntax"></a>Sintaxis completa  
 A continuación se muestra la representación de esquema de un objeto de relación.  
  
```  
"relationships": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "SingleColumnRelationship object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "isActive": {  
                    "type": "boolean"  
                  },  
                  "type": {  
                    "enum": [  
                      "singleColumn"  
                    ]  
                  },  
                  "crossFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections",  
                      "automatic"  
                    ]  
                  },  
                  "joinOnDateBehavior": {  
                    "enum": [  
                      "dateAndTime",  
                      "datePartOnly"  
                    ]  
                  },  
                  "relyOnReferentialIntegrity": {  
                    "type": "boolean"  
                  },  
                  "securityFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections"  
                    ]  
                  },  
                  "fromCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "toCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "fromColumn": {  
                    "type": "string"  
                  },  
                  "fromTable": {  
                    "type": "string"  
                  },  
                  "toColumn": {  
                    "type": "string"  
                  },  
                  "toTable": {  
                    "type": "string"  
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
            ]  
          }  
        }  
```  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Creación de relaciones](../../integration-services/data-flow/transformations/create-relationships.md)  
  
  
