---
title: Secuencia de comandos (TMSL) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bfdfd96ed2368d4f0900ffb70363f1a38201035f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34043419"
---
# <a name="sequence-command-tmsl"></a>Comando Sequence (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Use la **secuencia** comando para ejecutar un conjunto de operaciones consecutivo en modo por lotes en una instancia de Analysis Services.  El comando completo y todos sus componentes se deben completar en orden de la transacción sea correcta.  
  
 Se pueden ejecutar los siguientes comandos de forma secuencial, excepto para la **actualizar** comando que se ejecuta en paralelo para procesar varios objetos al mismo tiempo.  
  
-   [Crear un comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)  
  
-   [El comando CreateOrReplace &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)  
  
-   [ALTER, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)  
  
-   [Comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)  
  
-   [Comando Refresh &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)  
  
-   [Comando de copia de seguridad &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)  
  
-   [Comando restore &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)  
  
-   [El comando Attach &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)  
  
-   [Detach, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)  
  
## <a name="request"></a>Solicitud  
 **maxParallelism** es una propiedad opcional que determina si **actualizar** las operaciones se ejecutan secuencialmente o en paralelo.  
  
 El comportamiento predeterminado consiste en usar el paralelismo de tantos como sea posible. Incrustando **actualizar** en **secuencia**, puede controlar el número exacto de subprocesos que se utilizan durante el procesamiento, incluida la limitación de la operación de un solo subproceso.  
  
> [!NOTE]  
>  El entero asignado a **maxParallelism** determina el número máximo de subprocesos que se utilizan durante el procesamiento. Los valores válidos son cualquier número entero positivo. Establecer el valor en 1 es igual a no paralela (utiliza un subproceso).  
  
 Solo **actualizar** se ejecuta en paralelo. Si modifica **maxParallelism** para utilizar un número fijo de subprocesos, no olvide revisar las propiedades en el [comando Refresh &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md) para entender el impacto potencial. Es posible establecer las propiedades de una manera que incluso cuando se haya realizado varios subprocesos disponibles, se elimina el paralelismo. La siguiente secuencia de tipos de actualización le proporcionará el mejor grado de paralelismo:  
  
-   En primer lugar, especifica que se actualice para todos los objetos con ClearValues  
  
-   A continuación, especifica que se actualice para todos los objetos mediante DataOnly  
  
-   Última especifica que se actualice para todos los objetos con total, Calculate, automático o un complemento  
  
 Cualquier variación en el objeto interrumpirá el paralelismo.  
  
```  
{   
  "sequence":    
    {   
      "maxParallelism": 3,   
      "operations": [   
        {   
          "mergepartitions": {   
            "sources": [   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition1"   
              },   
              {   
                "database": "salesdatabase",   
                "table": "Sales",   
                "partition": "partition2"   
              }   
            ]   
          }   
        },   
        {   
          "refresh": {   
            "type": "calculate",   
            "objects": {   
             "database": "salesdatabase"   
            }   
          }   
        }   
      ]   
    }      
}   
```  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 No se puede generar un script listos para su uso para este comando de SSMS. En su lugar, puede comenzar con un ejemplo o escribir el suyo propio.  
  
 El [ \[MS-SSAS-T\]: Analysis Services Tabular de SQL Server (SQL Server técnica protocolo)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de JSON metadatos tabulares comandos y objetos . Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema ([Tabular Model Scripting Language &#40;TMSL&#41; referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para obtener información sobre lo que es compatible.  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
