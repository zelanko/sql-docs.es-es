---
title: Actualización de comandos (TMSL) | Documentos de Microsoft
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
ms.assetid: 97ff6ba8-c236-4ba6-8220-b0fcb9e1dc5c
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e3bf58b33d8e0fe72264d50e177cd6678200c006
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="refresh-command-tmsl"></a>Actualización de comandos (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Procesa los objetos en la base de datos actual.   
**Actualizar** siempre se ejecuta en paralelo, a menos que limitar con [de secuencia de comandos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md).  
  
 Puede invalidar algunas de las propiedades de algunos objetos durante una operación de actualización de datos:  
  
-   Cambiar el **QueryDefinition** propiedad de un **partición** objeto que se va a importar datos mediante una expresión de filtro sobre la marcha.  
  
-   Proporcione las credenciales de origen de datos como parte de un **actualizar** comando, en la **ConnectionString** propiedad de un **DataSource** objeto. Este enfoque podría se considera más seguro, como las credenciales se proporcionan y usar temporalmente para la duración de la operación, en lugar de almacenado.  
  
 Vea los ejemplos de este tema para ver una ilustración de estos reemplazos de propiedad.  
  
> [!NOTE]  
>  A diferencia del procesamiento multidimensional, no hay ningún control especial de procesamiento de errores para su procesamiento Tabular.  

  
## <a name="request"></a>Solicitud  
 **Actualizar** toma una definición de parámetro y el objeto de tipo.  
  
```  
    {  
        "refresh": {  
            "description": "Parameters of Refresh command of Analysis Services JSON API",  
            "properties": {  
            "type": {  
                "enum": [  
                "full",  
                "clearValues",  
                "calculate",  
                "dataOnly",  
                "automatic",  
                "add",  
                "defragment"  
                ]  
            },  
            "objects": {  
. . .   
```  
  
 El **tipo** parámetro establece un ámbito de la operación de procesamiento.  
  
||||  
|-|-|-|  
|**Tipo de actualización**|**Se aplica a**|**Description**|  
|completas|Base de datos,<br />Tabla,<br />Partición|Para todas las particiones en la partición, tabla o base de datos especificada, actualice los datos y actualice todos los elementos dependientes. Para una partición de cálculo, actualice la partición y todos sus elementos dependientes.|  
|clearValues|Base de datos,<br />Tabla,<br />Partición|Borre los valores de este objeto y todos los dependientes.|  
|calcular|Base de datos,<br />Tabla,<br />Partición|Actualice este objeto y todos sus elementos dependientes, pero solo si es necesario. Este valor no fuerza la actualización, excepto en el caso de fórmulas volátiles.|  
|dataOnly|Base de datos,<br />Tabla,<br />Partición|Actualice los datos de este objeto y borre todos los dependientes.|  
|automatic|Base de datos,<br />Tabla,<br />Partición|Si el objeto se debe actualizar, actualice el objeto y todos sus elementos dependientes. Se aplica si la partición se encuentra en un estado que no sea Ready.|  
|add|Partición|Anexe datos a esta partición y vuelva a calcular todos los dependientes. Este comando es válido solo para particiones normales y no para particiones de cálculo.|  
|desfragmentar|Base de datos,<br />Table|Desfragmente los datos de la tabla especificada. Ya que los datos se agregan a una tabla o se quitan de ella, los diccionarios de cada columna pueden contaminarse con valores que ya no existen en los valores de columna reales. La opción de desfragmentar limpiará los valores de los diccionarios que ya no se usan.|  
  
 Puede actualizar los objetos siguientes:  
  
 [Objeto de base de datos &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) procesar una base de datos.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200"  
      }  
    ]  
  }  
}  
```  
  
 [Tables, objeto &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) procesar una única tabla.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "Date"  
      }  
    ]  
  }  
}  
```  
  
 [Objeto de particiones &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) procesar una partición única dentro de una tabla.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota"  
      },  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota - 2011"  
      }  
    ]  
  }  
}  
```  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="examples"></a>Ejemplos  
 Invalidar tanto la **ConnectionString** y definición de una partición de la consulta.  
  
```  
{   
    "refresh": {   
        "type": "data",   
        "objects": [   
            {   
                "database": "tmtestdb",   
                "table": "sales"   
            },   
            {   
                "database": "tmtestdb",   
                "table": "customer"   
            }   
        ],   
        "overrides": [   
            {   
                "dataSources": [ // Bindings for Data Sources   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "dataSource": "contoso"   
                        },   
                        "dataSource": {   
                        "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=contoso;Integrated Security=SSPI;Persist Security Info=false"   
"   
                        }   
                    }   
                ],   
                "partitions": [ // Bindings for Partitions   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "table": "sales",   
                            "partition": "2015"   
                        },   
                        "partition": {   
                            "source": {   
                                "query": [  
                                     "SELECT sales.salesamount, customer.customername FROM sales",  
                                     "JOIN customer on custKey = sales.custkey",  
                                     "JOIN date on date.DateKey = customer.OrderDate",  
                                     "WHERE date.CalendarYear='2015'"  
                                  ],  
                            }   
                        }   
                    }   
                ]   
            }   
        ]   
    }   
}   
```  
  
 Invalidaciones de ámbito concreto estableciendo el parámetro de tipo en un **dataOnly** metadatos de actualización, permanece intacto.  
  
```  
{   
        "refresh" : {   
            "type" : "dataOnly",   
            "objects" : [   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Customer"   
                },   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                }   
            ],   
            "overrides" : [{   
                "scope" : {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                },   
                "dataSources" : [{   
                    "originalObject" : {   
                        "dataSource" : "SqlServer sqlcldb2 AS_foodmart_2000"   
                    },   
                    "connectionString" : "Provider=SQLNCLI11;Data Source=sqlcldb2;Initial Catalog=AS_foodmart_2000;Integrated Security=SSPI;Persist Security Info=false"   
                }]   
            }]   
        }   
    }   
```  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS.  Por ejemplo, puede hacer clic en el **Script** en un cuadro de diálogo de procesamiento.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema ([Tabular Model Scripting Language &#40;TMSL&#41; referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para obtener información sobre lo que es compatible.  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Configuración y opciones de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)  
  
  
