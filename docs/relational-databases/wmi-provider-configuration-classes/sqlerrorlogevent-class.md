---
title: Clase SqlErrorLogEvent | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 35e2af3f371d66ce38df5cb376516d40d01006bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62515490"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent, clase
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Proporciona las propiedades para ver los eventos en un archivo de registro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>Propiedades  
 La clase SQLErrorLogEvent define las siguientes propiedades.  
  
|||  
|-|-|  
|FileName|Tipo de datos: **cadena**<br /><br /> Tipo de acceso: Solo lectura<br /><br /> <br /><br /> El nombre del archivo de registro de errores.|  
|InstanceName|Tipo de datos: **cadena**<br /><br /> Tipo de acceso: Solo lectura<br /><br /> Calificadores: Key<br /><br /> El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] donde reside el archivo de registro.|  
|LogDate|Tipo de datos: **datetime**<br /><br /> Tipo de acceso: Solo lectura<br /><br /> Calificadores: Key<br /><br /> <br /><br /> Fecha y hora en que el evento se grabó en el archivo de registro.|  
|de mensaje|Tipo de datos: **cadena**<br /><br /> Tipo de acceso: Solo lectura<br /><br /> <br /><br /> Mensaje del evento.|  
|ProcessInfo|Tipo de datos: **cadena**<br /><br /> Tipo de acceso: Solo lectura<br /><br /> <br /><br /> Información sobre el identificador del proceso del servidor de origen (SPID) para el evento.|  
  
## <a name="remarks"></a>Comentarios  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Espacio de nombres|\raíz\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se muestra cómo recuperar los valores para todos los eventos anotados en un archivo de registro especificado. Para ejecutar el ejemplo, reemplace \< *Instance_Name*> con el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por ejemplo, 'Instancia1' y reemplace 'File_Name' por el nombre del archivo de registro de errores, como 'ERRORLOG.1'.  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>Comentarios  
 Cuando *nombreDeInstancia* o *FileName* no se proporcionan en la instrucción WQL, la consulta devolverá información para la instancia predeterminada y la actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo de registro. Por ejemplo, la siguiente instrucción WQL devolverá todos los eventos de registro desde el archivo de registro actual (ERRORLOG) en la instancia predeterminada (MSSQLSERVER).  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Seguridad  
 Para conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo de registro a través de WMI, debe tener los permisos siguientes en los equipos locales y remotos:  
  
-   Acceso de lectura a la **Root\Microsoft\SqlServer\ComputerManagement10** espacio de nombres WMI. De forma predeterminada, todos tienen acceso de lectura mediante el permiso Habilitar cuenta.  
  
-   Permiso de lectura a la carpeta que contiene los registros de errores. De forma predeterminada, el error registros se encuentran en la siguiente ruta de acceso (donde \< *unidad >* representa la unidad donde se instaló [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y \< *nombreDeInstancia*> es el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]):  
  
     **\<Unidad >: \Program Files\Microsoft SQL Server\MSSQL13** **.\< NombreDeInstancia > \MSSQL\Log**  
  
 Si se conecta a través de un firewall, asegúrese de que se establece una excepción en el firewall para WMI en los equipos de destino remotos. Para obtener más información, consulte [conectarse a WMI de forma remota comenzando con Windows Vista](https://go.microsoft.com/fwlink/?LinkId=178848).  
  
## <a name="see-also"></a>Vea también  
 [Clase SqlErrorLogFile](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [Ver archivos del registro sin conexión](../../relational-databases/logs/view-offline-log-files.md)  
  
  
