---
title: Clase SqlErrorLogFile | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5e23c4512f04370fa24b3eb4ff3b74a072f6a2e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198413"
---
# <a name="sqlerrorlogfile-class"></a>Clase SqlErrorLogFile
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
  
|||  
|-|-|  
|ArchiveNumber|Tipo de datos: `uint32`<br /><br /> Tipo de acceso: solo lectura<br /><br /> <br /><br /> El número de archivo para el archivo de registro.|  
|InstanceName|Tipo de datos: `string`<br /><br /> Tipo de acceso: solo lectura<br /><br /> Calificadores: clave<br /><br /> <br /><br /> El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde reside el archivo de registro.|  
|LastModified|Tipo de datos: `datetime`<br /><br /> Tipo de acceso: solo lectura<br /><br /> <br /><br /> Fecha de la última modificación del archivo de registro.|  
|LogFileSize|Tipo de datos: `uint32`<br /><br /> Tipo de acceso: solo lectura<br /><br /> <br /><br /> El tamaño del archivo de registro en bytes.|  
|Nombre|Tipo de datos: `string`<br /><br /> Tipo de acceso: solo lectura<br /><br /> Calificadores: clave<br /><br /> <br /><br /> El nombre del archivo de registro.|  
  
## <a name="remarks"></a>Notas  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Espacio de nombres|\raíz\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se recupera información sobre todos los archivos de registro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una instancia especificada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para ejecutar el ejemplo, reemplace \< *Instance_Name*> con el nombre de la instancia, por ejemplo, 'instancia1'.  
  
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
 Cuando *nombreDeInstancia* no se proporciona en la instrucción WQL, la consulta devolverá información para la instancia predeterminada. Por ejemplo, la siguiente instrucción WQL devolverá información sobre todos los archivos de registro de la instancia predeterminada (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>Seguridad  
 Para conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo de registro a través de WMI, debe tener los permisos siguientes en los equipos locales y remotos:  
  
-   Acceso de lectura a la **Root\Microsoft\SqlServer\ComputerManagement10** espacio de nombres WMI. De forma predeterminada, todos tienen acceso de lectura mediante el permiso Habilitar cuenta.  
  
    > [!NOTE]  
    >  Para obtener información sobre cómo comprobar los permisos de WMI, vea la sección seguridad del tema [ver sin conexión archivos de registro](../logs/view-offline-log-files.md).  
  
-   Permiso de lectura a la carpeta que contiene los registros de errores. De forma predeterminada el error registros se encuentran en la ruta de acceso siguiente (donde \< *unidad >* representa la unidad donde se instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y \< *nombreDeInstancia*> es el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Unidad >: \Program SQL Server\MSSQL11** **.\< NombreDeInstancia > \MSSQL\Log**  
  
 Si se conecta a través de un firewall, asegúrese de que se establece una excepción en el firewall para WMI en los equipos de destino remotos. Para obtener más información, consulte [conectar con WMI de forma remota comenzando con Windows Vista](http://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Vea también  
 [Sqlerrorlogevent, clase](sqlerrorlogevent-class.md)   
 [Ver archivos del registro sin conexión](../logs/view-offline-log-files.md)  
  
  