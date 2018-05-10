---
title: Objeto de orígenes de datos (TMSL) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 96eb6e72c9bbe6ba63e1c4a2685ecade4e6c7cc8
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="datasources-object-tmsl"></a>Objeto de orígenes de datos (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Define una conexión a un origen de datos utilizado por el modelo durante la importación para agregar datos al modelo o de paso a través de las consultas mediante el modo DirectQuery.  Los modelos en el modo DirectQuery sólo pueden tener una **DataSource** objeto.  
  
 A menos que se va a crear, reemplazar, o modificar el propio objeto de origen de datos, cualquier origen de datos al que hace referencia en la secuencia de comandos (como en la secuencia de comandos de partición) debe ser una existente **DataSource** objeto en el modelo.  
  
## <a name="object-definition"></a>Definición del objeto  
 Todos los objetos tienen un conjunto común de propiedades, incluidos el nombre, tipo, descripción, una colección de propiedades y las anotaciones. **Origen de datos** objetos también tienen las siguientes propiedades.  
  
 Tipo  
 El tipo de objeto DataSource. En la actualidad, el único valor válido es proveedor (1) - cadena de conexión Normal.  
  
 connectionString  
 La cadena de conexión que como mínimo, especifica el servidor y la base de datos, pero también puede incluir otras propiedades compatibles con el RDBMS externo, como una cuenta de usuario o el proveedor de datos. Este valor es necesario. Vea [clase SqlConnectionStringBuilder](https://msdn.microsoft.com/en-us/library/ms254500\(v=vs.110\).aspx) propiedades de la cadena de conexión de base de datos de para obtener más información acerca de SQL Server.  
  
 elemento impersonationMode  
 Especifica si Analysis Services debe suplantar la identidad del usuario que solicita la consulta. Esta propiedad es un valor numérico que especifica las credenciales que se usarán para la suplantación. Los valores de enumeración son los siguientes:  
  
-   Predeterminado (1): el servidor usa el método de suplantación que lo considera apropiado para el contexto en el que se usa la suplantación.  
  
-   ImpersonateAccount (2): el servidor utiliza la cuenta de usuario especificada.  
  
-   ImpersonateAnonymous (3): el servidor utiliza la cuenta de usuario anónimo.  Esta opción no se recomienda, pero a veces se utiliza en escenarios de acceso HTTP en aplicaciones personalizadas que administran la autenticación.  
  
-   ImpersonateCurrentUser (4) - el servidor utiliza la cuenta de usuario que se está conectando el cliente como.  
  
-   ImpersonateServiceAccount (5): el servidor utiliza la cuenta de usuario que el servidor se ejecuta como.  
  
-   ImpersonateUnattendedAccount (6): el servidor usa una cuenta de usuario desatendida. Esto se utiliza para modelos de PowerPivot o Tabular que se ejecutan en un entorno de SharePoint.  
  
 El modo DirectQuery puede usar impersonateCurrentuser si Analysis Services está configurado para delegación de confianza, o  
                      impersonateServiceAccount si la solicitud de consulta se realiza en el contexto de seguridad de la cuenta de servicio de Analysis Services. Vea [la delegación limitada de configurar Analysis Services for Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
 account   
 Utilizar para la suplantación. Una cuenta de Windows o la base de datos que tenga un inicio de sesión válido con permisos de lectura en la base de datos externo.  
  
 password  
 Una cadena cifrada proporcionar la contraseña de la cuenta.  
  
 maxConnections  
 El número máximo de conexiones que se abrirán simultáneamente en el origen de datos.  
  
 isolation  
 El tipo de aislamiento que se usa durante la ejecución de comandos en el origen de datos. Los valores válidos son ReadCommitted (1) o Snapshot (2).  
  
 timeout  
 Un entero que especifica el tiempo de espera en segundos para los comandos que se ejecuta en el origen de datos.  
  
 proveedor  
 Una cadena opcional que identifica el nombre del proveedor de datos administrado utilizado en la conexión a la base de datos relacional, si no se especifica lo contrario en la cadena de conexión.  
  
## <a name="usage"></a>Uso  
 **Origen de datos** objetos se utilizan en [Alter, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [crear comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [comando CreateOrReplace &#40; TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [comando Refresh &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), y [MergePartitions, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 A **DataSource** es una propiedad de un modelo de objeto, pero también se puede especificar como una propiedad de un objeto de base de datos según la asignación uno a uno entre el modelo y la base de datos.  Las particiones basadas en consultas SQL también especifican un **DataSource**, solo con un conjunto reducido de propiedades.  
  
 Al crear, reemplazar o modificar un objeto de origen de datos, especifique todas las propiedades de lectura y escritura de la definición del objeto. Omisión de una propiedad de lectura y escritura se considera una operación de eliminación.  
  
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
 A continuación se muestra la representación de esquema de un objeto de origen de datos de un modelo.  
  
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
 [Configurar el acceso HTTP a Analysis Services de servicios de Internet Information Server & #40; IIS & #41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
