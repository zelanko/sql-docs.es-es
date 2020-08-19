---
description: Clase SqlErrorLogFile
title: Clase SqlErrorLogFile
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 63937cb2d7a3aaf3994712aa493097597cd26c53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446470"
---
# <a name="sqlerrorlogfile-class"></a>Clase SqlErrorLogFile
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]
  Proporciona propiedades para ver información sobre un archivo de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>Propiedades  
 La clase SQLErrorLogFile define las siguientes propiedades.  
  
| Propiedad | Descripción |
| -------- | ----------- |
|ArchiveNumber|Tipo de datos: **UInt32**<br /><br /> Tipo de acceso: solo lectura<br /><br /> <br /><br /> El número de archivo para el archivo de registro.|  
|InstanceName|Tipo de datos: **cadena**<br /><br /> Tipo de acceso: solo lectura<br /><br /> Calificadores: clave<br /><br /> <br /><br /> El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde reside el archivo de registro.|  
|LastModified|Tipo de datos: **DateTime**<br /><br /> Tipo de acceso: solo lectura<br /><br /> <br /><br /> Fecha de la última modificación del archivo de registro.|  
|LogFileSize|Tipo de datos: **UInt32**<br /><br /> Tipo de acceso: solo lectura<br /><br /> <br /><br /> El tamaño del archivo de registro en bytes.|  
|Nombre|Tipo de datos: **cadena**<br /><br /> Tipo de acceso: solo lectura<br /><br /> Calificadores: clave<br /><br /> <br /><br /> El nombre del archivo de registro.|  
  
## <a name="remarks"></a>Observaciones  
  
| Tipo | Nombre |
| ---- | ---- |
|MOF|Sqlmgmprovider xpsp2up.mof|  
|Archivo DLL|Sqlmgmprovider.dll|  
|Espacio de nombres|\raíz\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se recupera información sobre todos los archivos de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para ejecutar el ejemplo, reemplace \<*Instance_Name*> por el nombre de la instancia, por ejemplo, ' Instance1 '.  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>Comentarios  
 Cuando no se proporciona *InstanceName* en la instrucción WQL, la consulta devolverá información para la instancia predeterminada. Por ejemplo, la siguiente instrucción WQL devolverá información sobre todos los archivos de registro de la instancia predeterminada (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>Seguridad  
 Para conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo de registro a través de WMI, debe tener los siguientes permisos en los equipos locales y remotos:  
  
-   Acceso de lectura al espacio de nombres WMI **Root\Microsoft\SqlServer\ComputerManagement10** . De forma predeterminada, todos tienen acceso de lectura mediante el permiso Habilitar cuenta.  
  
    > [!NOTE]  
    >  Para obtener información sobre cómo comprobar los permisos de WMI, consulte la sección seguridad del tema [ver archivos de registro sin conexión](../../relational-databases/logs/view-offline-log-files.md).  
  
-   Permiso de lectura a la carpeta que contiene los registros de errores. De forma predeterminada, los registros de errores se encuentran en la siguiente ruta de acceso (donde \<*Drive> * representa la unidad donde se instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y \<*InstanceName*> es el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ):  
  
     ** \<Drive> : \Archivos de Programa\microsoft SQL Server\MSSQL11** **. \<InstanceName> \Mssql\log.**  
  
 Si se conecta a través de un firewall, asegúrese de que se establece una excepción en el firewall para WMI en los equipos de destino remotos. Para obtener más información, consulte [conectarse a WMI de forma remota a partir de Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Consulte también  
 [Clase SqlErrorLogEvent](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogevent-class.md)   
 [Ver archivos del registro sin conexión](../../relational-databases/logs/view-offline-log-files.md)  
  
  
