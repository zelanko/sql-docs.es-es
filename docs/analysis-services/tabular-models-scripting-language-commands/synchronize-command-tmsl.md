---
title: Synchronize, comando (TMSL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2017
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
ms.assetid: a32ff053-f38f-49d7-afdc-e19f59c88135
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2904954269f32dc80d603c3c0b045685d58bc2d5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="synchronize-command-tmsl"></a>Synchronize, comando (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later](../../includes/ssas-appliesto-sql2016-later.md)]

  Sincroniza una base de datos de Analysis Services con otra base de datos existente.  
  
## <a name="request"></a>Solicitud  
 Comando de sincronización de las propiedades que acepta el JSON son las siguientes.  
  
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
  
 Comando de sincronización de las propiedades que acepta el JSON son las siguientes.  
  
||||  
|-|-|-|  
|**Propiedad**|**Default**|**Description**|  
|database||El nombre del objeto de base de datos que se sincronizarán.|  
|origen||Cadena de conexión que se va a usar para conectarse al servidor de origen.|  
|synchronizeSecurity|skipMembership|Un valor de enumeración que especifica cómo restaurar definiciones de seguridad, incluidos los roles y permisos. Los valores válidos incluyen copyAll, skipMembership, e ignoreSecurity.|  
|applyCompression|True|Un valor booleano que, cuando es true, indica que se aplicará la compresión durante la operación de sincronización; lo contrario, false.|  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS, haga clic en el botón de secuencia de comandos en el cuadro de diálogo Sincronizar base de datos.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema [Tabular Model Scripting Language &#40; TMSL &#41; Referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para aclarar lo que es compatible  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

