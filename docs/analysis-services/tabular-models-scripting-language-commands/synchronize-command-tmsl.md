---
title: Comando Synchronize (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4265e6fa1e2214fae53cacdb084e152005eb3647
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033278"
---
# <a name="synchronize-command-tmsl"></a>Comando Synchronize (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Sincroniza una base de datos de Analysis Services con otra base de datos existente.  
  
## <a name="request"></a>Solicitud  
 Comando de sincronización de las propiedades aceptadas por el código JSON son los siguientes.  
  
```  
{   
   "synchronize":{   
      "database":"AdventureWorksDW_Production",  
      "source":"Provider=MSOLAP.7;Data Source=localhost;Integrated Security=SSPI;Initial Catalog=AdventureWorksDW_Dev",  
      "synchronizeSecurity":"copyAll",  
      "applyCompression":true  
   }  
}  
```  
  
 Comando de sincronización de las propiedades aceptadas por el código JSON son los siguientes.  
  
||||  
|-|-|-|  
|**Propiedad**|**Default**|**Descripción**|  
|Base de datos||El nombre del objeto de base de datos se sincronicen.|  
|origen||La cadena de conexión para conectarse al servidor de origen.|  
|synchronizeSecurity|skipMembership|Valor de enumeración que especifica cómo restaurar definiciones de seguridad, incluidos los roles y permisos. Los valores válidos incluyen copyAll, skipMembership, ignoreSecurity.|  
|applyCompression|True|Un valor booleano que, cuando es true, indica que se aplicará la compresión durante la operación de sincronización; en caso contrario, false.|  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se usa en una instrucción de la [Ejecutar método &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto en las siguientes maneras:  
  
-   Como una ventana XMLA de SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para una tarea SSIS o el trabajo del Agente SQL Server  
  
 Puede generar un script ya preparado para este comando desde SSMS, haga clic en el botón de la secuencia de comandos en el cuadro de diálogo Sincronizar base de datos.  
  
 El [ \[SSAS-MS-T\]: QL Server Tabular de Analysis Services (protocolo técnicos de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de JSON de metadatos tabulares y los objetos. Actualmente, ese documento trata los comandos y capacidades que aún no se han implementado en el script TMSL. Consulte el tema [Tabular Model Scripting Language &#40;TMSL&#41; referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para aclarar lo que es compatible  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
