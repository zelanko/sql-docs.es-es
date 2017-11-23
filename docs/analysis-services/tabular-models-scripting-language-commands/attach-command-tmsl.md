---
title: Attach, comando (TMSL) | Documentos de Microsoft
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
ms.assetid: 7a12d148-eac9-4e6c-a222-1439e0817c64
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 995e77345c2770f59db620afb1ced2085eaeefa2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="attach-command-tmsl"></a>Attach, comando (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Adjunta un archivo de Analysis Services en un servidor.  
  
  
## <a name="request"></a>Solicitud  
  
```  
{   
   "attach":{   
      "folder":"C:\\Program Files\\Microsoft SQL Server\\MSAS13.Tabular\\OLAP\\Data\\",  
      "readWriteMode":"readOnly",  
      "password":"secret"  
   }  
}  
```  
  
 Las propiedades que acepta el JSON attach, comando son los siguientes.  
  
||||  
|-|-|-|  
|**Propiedad**|**Default**|**Description**|  
|database|[Required]|El nombre del objeto de base de datos que se adjuntará.|  
|folder|[Required]|La carpeta que contiene la base de datos adjunta.|  
|password|Vacía|La contraseña que se utilizará para cifrar secretos en la base de datos adjunta.|  
|readWriteMode|Lectura y escritura|Un valor de enumeración que indica los modos de acceso permitidos a la base de datos.<br /><br /> **Los valores de enumeración son como sigue:**<br /><br /> lectura y escritura: se permite el acceso de lectura y escritura.<br /><br /> readOnly: se permite el acceso de solo lectura.<br /><br /> readOnlyExclusive: se permite el acceso exclusivo de solo lectura.|  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS, haga clic en el botón de secuencia de comandos en el cuadro de diálogo Adjuntar base de datos.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema [Tabular Model Scripting Language &#40; TMSL &#41; Referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para aclarar lo que es compatible  

## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)  
  
  
