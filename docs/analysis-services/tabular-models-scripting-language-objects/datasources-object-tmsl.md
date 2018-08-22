---
title: Objeto DataSources (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a83ac3429a3012269a35c64ba5fdcbec18b2d4c
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393305"
---
# <a name="datasources-object-tmsl"></a>Objeto DataSources (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Define una conexión a un origen de datos utilizado por el modelo, ya sea durante la importación para agregar datos al modelo, o en el paso a través de consultas mediante el modo DirectQuery.  Solo pueden tener modelos en el modo DirectQuery **DataSource** objeto.  
  
 A menos que se va a crear, reemplazar, o modificar el propio objeto de origen de datos, cualquier origen de datos al que hace referencia en la secuencia de comandos (como en la secuencia de comandos de partición) debe ser una existente **DataSource** objeto en el modelo.  
  
## <a name="object-definition"></a>Definición del objeto  
 Todos los objetos tienen un conjunto común de propiedades, incluidos el nombre, tipo, descripción, una colección de propiedades y las anotaciones. **Origen de datos** objetos también tienen las siguientes propiedades.  
  
 Tipo  
 El tipo de objeto DataSource. En la actualidad, el único valor válido es proveedor (1) - cadena de conexión Normal.  
  
 connectionString  
 La cadena de conexión que especifica el servidor y base de datos como mínimo, pero también puede incluir otras propiedades admitidas por el RDBMS externo, como una cuenta de usuario o el proveedor de datos. Este valor es necesario. Consulte [clase SqlConnectionStringBuilder](/dotnet/framework/data/adonet/connection-string-syntax) para obtener más información acerca de SQL Server las propiedades de la cadena de conexión de base de datos.  
  
 elemento impersonationMode  
 Especifica si Analysis Services debe suplantar la identidad del usuario que solicita la consulta. Esta propiedad es un valor numérico que especifica las credenciales que se usarán para la suplantación. Los valores de enumeración son los siguientes:  
  
-   Predeterminado (1): el servidor usa el método de suplantación que lo considera apropiado para el contexto en el que se utiliza la suplantación.  
  
-   ImpersonateAccount (2): el servidor usa la cuenta de usuario especificado.  
  
-   ImpersonateAnonymous (3): el servidor usa la cuenta de usuario anónimo.  Esta opción no se recomienda, pero a veces se usa en escenarios de acceso HTTP en aplicaciones personalizadas que controlan la autenticación.  
  
-   ImpersonateCurrentUser (4): el servidor utiliza la cuenta de usuario que se está conectando el cliente como.  
  
-   ImpersonateServiceAccount (5): el servidor utiliza la cuenta de usuario que el servidor se está ejecutando como.  
  
-   ImpersonateUnattendedAccount (6): el servidor utiliza una cuenta de usuario desatendido. Esto se utiliza para modelos de PowerPivot o Tabular que se ejecutan en un entorno de SharePoint.  
  
 El modo DirectQuery puede usar impersonateCurrentuser si Analysis Services está configurada para delegación de confianza, o  
                      impersonateServiceAccount si se realiza la solicitud de consulta en el contexto de seguridad de la cuenta de servicio de Analysis Services. Consulte [delegación limitada de configurar Analysis Services for Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
 account   
 Se usa para la suplantación. Una cuenta de Windows o la base de datos que tenga un inicio de sesión válido con permisos de lectura en la base de datos externo.  
  
 password  
 Una cadena cifrada proporcionando la contraseña de la cuenta.  
  
 maxConnections  
 El número máximo de conexiones que se abrirán simultáneamente en el origen de datos.  
  
 isolation  
 El tipo de aislamiento que se utiliza al ejecutar comandos contra el origen de datos. Los valores válidos son ReadCommitted (1) o una instantánea (2).  
  
 timeout  
 Un entero que especifica el tiempo de espera en segundos para los comandos ejecutados en el origen de datos.  
  
 proveedor  
 Una cadena opcional que identifica el nombre del proveedor de datos administrado utilizado en la conexión a la base de datos relacional, si no se especifica en la cadena de conexión.  
  
## <a name="usage"></a>Uso  
 **Origen de datos** objetos se usan en [comando Alter &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [crear comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [comando CreateOrReplace &#40; TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [comando Refresh &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), y [comando MergePartitions &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 Un **DataSource** es una propiedad de un modelo de objeto, pero también se puede especificar como una propiedad de un objeto de base de datos según la asignación uno a uno entre el modelo y la base de datos.  Las particiones basadas en consultas SQL también especifican una **DataSource**, solo con un conjunto reducido de propiedades.  
  
 Al crear, reemplazar o modificar un objeto de origen de datos, especifique todas las propiedades de lectura y escritura de la definición del objeto. Omisión de una propiedad de lectura y escritura se considera una eliminación.  
  
## <a name="examples"></a>Ejemplos  
 **Ejemplo 1** -una conexión a un *FoodMart* base de datos en un instancia con nombre de control remoto *ventas* en un servidor de red denominado *Server01*.  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>Sintaxis completa  
 A continuación es la representación de esquema de un objeto de origen de datos de un modelo.  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
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
        },  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
