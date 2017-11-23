---
title: Copia de seguridad de comando (TMSL) | Documentos de Microsoft
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
ms.assetid: fae1b267-0750-4dc5-9bf0-80ac4d8487a3
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ba078752949c491b017ceb75546ac694eab67765
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="backup-command-tmsl"></a>Comando de copia de seguridad (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Realiza una copia de una base de datos de Analysis Services en un archivo de copia de seguridad de abf.  
  
## <a name="request"></a>Solicitud  
  
```  
    {  
        "backup": {  
            "description": "Parameters of Backup command of Analysis Services JSON API",  
            "properties": {  
            "database": {  
                "type": "string"  
            },  
            "file": {  
                "type": "string"  
            },  
            "password": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type": "boolean"  
            },  
            "applyCompression": {  
                "type": "boolean"  
            }  
            },  
. . .   
```  
  
 **Copia de seguridad** tiene varias propiedades.  
  
||||  
|-|-|-|  
|**Propiedad**|**Default**|**Description**|  
|database|[Required]|El nombre del objeto de base de datos para realizar copias de seguridad.|  
|archivo|[Required]|Nombre o ruta de acceso de la copia de seguridad.|  
|password|Vacía|La contraseña que se utilizará para cifrar el archivo de copia de seguridad.|  
|allowOverwrite|False|Un valor booleano que, cuando es true, indica que ya existe un archivo de copia de seguridad se sobrescribirá; lo contrario, false.|  
|applyCompression|True|Un valor booleano que, cuando es true, indica que los archivos de copia de seguridad están comprimidos; lo contrario, false.|  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="examples"></a>Ejemplos  
 **Ejemplo 1** -copia de seguridad de un archivo en la carpeta de copia de seguridad predeterminada.  
  
```  
{   
   "backup": {   
      "database":"AS_AdventureWorksDW2014",  
      "file":"AS_AdventureWorksDW2014.abf",  
      "password":"secret"  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS, haga clic en el botón de secuencia de comandos en el cuadro de diálogo de la base de datos de copia de seguridad.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema [Tabular Model Scripting Language &#40; TMSL &#41; Referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para aclarar lo que es compatible  

## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
