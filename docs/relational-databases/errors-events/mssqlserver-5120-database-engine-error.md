---
title: MSSQLSERVER_5228 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5120 (Database Engine error)
ms.assetid: ''
author: PijoCoder
ms.author: mathoma
ms.openlocfilehash: ff8fb262b643390f2914a4a5e6c42dcc887206f8
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81728622"
---
# <a name="mssqlserver_5120"></a>MSSQLSERVER_5120
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|5120|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DSK_FCB_FAILURE|  
|Texto del mensaje|Error de tabla: No se puede abrir el archivo físico "%.*ls". Error del sistema operativo %d: "%ls".|  
  
## <a name="explanation"></a>Explicación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo abrir un archivo de base de datos.  El error del sistema operativo proporcionado en el mensaje apunta a razones subyacentes más específicas para el error. Este error suele aparecer junto con otros errores, como [17204](mssqlserver-17204-database-engine-error.md) o [17207](mssqlserver-17207-database-engine-error.md).
  
## <a name="user-action"></a>Acción del usuario  
  
  Diagnostique y corrija el error del sistema operativo y, después, vuelva a intentar realizar la operación. Hay varios estados que pueden ayudar a Microsoft a reducir el área del producto donde se está produciendo el error. 
  
### <a name="access-is-denied"></a>Acceso denegado 
Si obtiene el error ```Access is Denied``` del sistema operativo = 5, tenga en cuenta estos métodos:
   -  Compruebe los permisos que se establecen en el archivo examinando las propiedades del archivo en el Explorador de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza grupos de Windows para aprovisionar Access Control en los distintos recursos de archivo. Asegúrese de que el grupo adecuado [con nombres como SQLServerMSSQLUser$ComputerName$MSSQLSERVER o SQLServerMSSQLUser$ComputerName$InstanceName] tiene los permisos necesarios en el archivo de base de datos mencionado en el mensaje de error. Vea [Configurar permisos del sistema de archivos para el acceso al motor de base de datos](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md) para obtener más información. Asegúrese de que el grupo de Windows incluye realmente la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el identificador de seguridad del servicio.
   -  Revise la cuenta de usuario en la que se ejecuta actualmente el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede usar el administrador de tareas de Windows para obtener esta información. Busque el valor "Nombre de usuario" para el archivo ejecutable "sqlservr.exe". Además, si ha cambiado recientemente la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe saber que la manera admitida para realizar esta operación es usar la utilidad [Administrador de configuración de SQL Server](../sql-server-configuration-manager.md). 
   -  Dependiendo del tipo de operación, como abrir bases de datos durante el inicio del servidor, adjuntar una base de datos, restaurar una base de datos, etc., la cuenta que se usa para la suplantación y el acceso al archivo de base de datos puede variar. Revise el tema [Proteger archivos de datos y de registro](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) para comprender qué operación establece qué permiso y para qué cuentas. Use una herramienta como [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) de Windows SysInternals para saber si el acceso al archivo se produce en el contexto de seguridad de la cuenta de inicio del servicio de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o el identificador de seguridad del servicio, o una cuenta suplantada.

      Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suplanta las credenciales de usuario del inicio de sesión que ejecuta la operación ALTER DATABASE o CREATE DATABASE, verá la siguiente información en la herramienta Process Monitor (ejemplo):
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL13.SQL2016\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
  
### Attaching Files that Reside on a Network-attached storage  
If you cannot re-attach a database that resides on network-attached storage, a message like this may be logged in the Application log:

```Msg 5120, Level 16, State 101, Line 1 Unable to open the physical file "\\servername\sharename\filename.mdf". Operating system error 5: (Access is denied.).```

This problem occurs because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resets the file permissions when the database is detached. When you try to reattach the database, a failure occurs because of limited share permissions.

To resolve, follow these steps:
1. Use the -T startup option to start [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use this startup option to turn on trace flag 1802 in [SQL Server Configuration Manager](../sql-server-configuration-manager.md) (see [Trace Flags](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md) for information on 1802). For more information about how to change the startup parameters, see [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)

2. Use the following command to detach the database.
```tsql
 exec sp_detach_db DatabaseName
 go 
```

3. Use el siguiente comando para volver a adjuntar la base de datos.
```tsql
exec sp_attach_db DatabaseName, '\\Network-attached storage_Path\DatabaseMDFFile.mdf', '\\Network-attached storage_Path\DatabaseLDFFile.ldf'
go
```
 
