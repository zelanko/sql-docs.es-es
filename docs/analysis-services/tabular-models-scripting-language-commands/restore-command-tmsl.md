---
title: Restaurar comandos (TMSL) | Documentos de Microsoft
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
ms.assetid: 360a1567-67ae-459d-8865-9a2bef8d4186
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 75c285d9cc6b82d610e4249bb5a26489b4416876
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="restore-command-tmsl"></a>Restaurar comandos (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Restaura una base de datos de Analysis Services desde un archivo de copia de seguridad.  
  
## <a name="request"></a>Solicitud  
  
```  
    {  
"restore": {  
            "description": "Parameters of Restore command of Analysis Services JSON API",  
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
            "dbStorageLocation": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type":boolean  
            },  
            "readWriteMode": {  
                "enum": [  
                "readWrite",  
                "readOnly",  
                "readOnlyExclusive"  
                ]  
. . .   
```  
  
 **Restaurar** tiene varias propiedades.  
  
||||  
|-|-|-|  
|**Propiedad**|**Valor de DB-Library**|**Description**|  
|database|[Required]|El nombre del objeto de base de datos que se restaurarán.|  
|archivo|[Required]|Nombre o ruta de acceso de la copia de seguridad.|  
|password|Vacía|La contraseña que se utilizará para descifrar el archivo de copia de seguridad.|  
|allowOverwrite|False|Un valor booleano que, cuando es true, indica que ya existe un archivo de copia de seguridad se sobrescribirá; lo contrario, false.|  
|readWriteMode|Lectura y escritura|Un valor de enumeración que indica los modos de acceso permitidos a la base de datos.<br /><br /> **Los valores de enumeración son como sigue:**<br /><br /> lectura y escritura: se permite el acceso de lectura y escritura.<br /><br /> readOnly: se permite el acceso de solo lectura.<br /><br /> readOnlyExclusive: se permite el acceso exclusivo de solo lectura.|  
|dbStorageLocation|Vacía|Ubicación de almacenamiento de la base de datos restaurada.|  
  
## <a name="response"></a>Respuesta  
 Cuando el comando se ejecuta correctamente, devuelve un resultado vacío. En caso contrario, se devuelve una excepción de XMLA.  
  
## <a name="example"></a>Ejemplo  
 **Ejemplo 1** -restaurar bases de datos desde una carpeta local.  
  
```  
{   
   "restore": {   
      "database":"AdventureWorksDW2014",  
      "file":"c:\\awdbdwfile.abf",  
      "security":"...",  
      "allowOverwrite":"true",  
      "password":"..",  
      "locations":"d:\\SQL Server Analysis Services\\data\\",  
      "storageLocation":".."  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>Uso (extremos)  
 Este elemento de comando se utiliza en una instrucción de la [Execute Method &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) llamada a través de un punto de conexión XMLA, expuesto de las maneras siguientes:  
  
-   Como una ventana XMLA en SQL Server Management Studio (SSMS)  
  
-   Como un archivo de entrada para el **invoke-ascmd** cmdlet de PowerShell  
  
-   Como entrada para un trabajo de agente SQL Server o de tareas SSIS  
  
 Puede generar un script listos para su uso para este comando de SSMS, haga clic en el botón de secuencia de comandos en el cuadro de diálogo de restauración.  
  
 El [ \[MS-SSAS-T\]: QL Server Tabular de Analysis Services (protocolo técnica de SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento incluye sección 3.1.5.2.2 que describe la estructura de comandos de metadatos tabulares de JSON y objetos. Actualmente, dicho documento tratan comandos y las funciones que aún no implementados en el script de TMSL. Consulte el tema [Tabular Model Scripting Language &#40;TMSL&#41; referencia](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para obtener información sobre lo que es compatible  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
