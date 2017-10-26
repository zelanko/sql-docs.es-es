---
title: Detach, comando (TMSL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 413b49cb-ea8f-415c-a059-ce692b7771a1
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dfa0440270971b80d6cd1f6789534cedb6f976ad
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="detach-command-tmsl"></a>Detach, comando (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Separa una base de datos de Analysis Services desde un servidor.  
  
## <a name="request"></a>Solicitud  
  
```  
{   
   "detach": {    
      "database":"AdventureWorksDW2014",  
      "password": "secret"  
   }  
}  
```  
  
 Las propiedades que acepta el JSON detach, comando son los siguientes.  
  
||||  
|-|-|-|  
|**Propiedad**|**Default**|**Description**|  
|database|[Required]|El nombre del objeto de base de datos que se va a desasociar.|  
|password|Vacía|La contraseña que se utilizará para cifrar secretos en la base de datos separada.|  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS, haga clic en el botón de secuencia de comandos en el cuadro de diálogo separar.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema ([Tabular Model Scripting Language &#40; TMSL &#41; Hacer referencia a](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para obtener información sobre lo que es compatible.  

## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  

