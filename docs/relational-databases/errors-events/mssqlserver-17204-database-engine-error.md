---
title: MSSQLSERVER_17204 | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17204 (Database Engine error)
ms.assetid: 40db66f9-dd5e-478c-891e-a06d363a2552
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 63f8e2729492d66eb498b0634e015a0a3d4638ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780798"
---
# <a name="mssqlserver_17204"></a>MSSQLSERVER_17204
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |
| :-------- | :---- |
|Nombre de producto|SQL Server|  
|Id. de evento|17204|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBLKIO_DEVOPENFAILED|  
|Texto del mensaje|%ls: no se pudo abrir el archivo %ls para el número de archivo %d.  Error del sistema operativo: %ls.|  
  
## <a name="explanation"></a>Explicación  
SQL Server no pudo abrir el archivo especificado debido al error del sistema operativo especificado.  

Es posible que vea el error 17204 en el evento de aplicaciones Windows o en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando SQL Server no puede abrir una base de datos o archivos de registro de transacciones. Este es un ejemplo de cómo podría ser el error:

``` 
Error: 17204, Severity: 16, State: 1.
FCB::Open failed: Could not open file c:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\data\MyDB_Prm.mdf for file number 1.  OS error: 5(Access is denied.).
```

Puede ver estos errores durante el proceso de inicio de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o cualquier operación de base de datos que intente iniciar la base de datos (por ejemplo, ALTER DATABASE). En algunos escenarios, puede ver los errores 17204 y 17207 y, en otras ocasiones, puede que solo vea uno de ellos.

Si una base de datos de usuario se ejecuta con estos errores, esa base de datos se quedará en el estado RECOVERY_PENDING y las aplicaciones no podrán acceder a la base de datos. Si una base de datos del sistema encuentra estos errores, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se iniciará y no podrá conectarse a esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un error con una base de datos del sistema podría dar lugar a que un recurso de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quede sin conexión.

## <a name="cause"></a>Causa
Antes de que se pueda usar cualquier base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es necesario iniciar la base de datos. El proceso de inicio de la base de datos conlleva: 
1. Inicializar varias estructuras de datos que representan la base de datos y los archivos de base de datos
1. Abrir todos los archivos que pertenecen a la base de datos
1. Ejecutar la recuperación en la base de datos 

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la función de la API de Windows [CreateFile](https://docs.microsoft.com/windows/win32/api/fileapi/nf-fileapi-createfilea) para abrir los archivos que pertenecen a una base de datos.
 
Los mensajes 17204 y 17207 indican que se ha producido un error mientras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intentaba abrir los archivos de base de datos durante el proceso de inicio.
 
Estos mensajes de error contienen la siguiente información:
1. Nombre de la función de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que intenta abrir el archivo. El nombre de la función que se observa normalmente en estos mensajes de error es uno de los siguientes:
   - FCB::Open: el archivo ha detectado un error cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta abrirlo.
   - FileMgr::StartPrimaryDataFiles: un archivo de datos principal o un archivo perteneciente al grupo de archivos principal.
   - FileMgr::StartSecondaryDataFiles: un archivo perteneciente a un grupo de archivos secundario.
   - FileMgr::StartLogFiles: un archivo de registro de transacciones.
   - STREAMFCB::Startup: contenedor de SQL FileStream.
   - FCB::RemoveAlternateStreams
  
      
1. La información de estado distingue varias ubicaciones dentro de una función que puede generar este mensaje de error.
1. La ruta de acceso física completa del archivo.
1. El id. de archivo que corresponde al archivo.
1. El código de error del sistema operativo y la descripción del error. En algunos casos, solo verá el código de error.
 
La información de error del sistema operativo que se imprime en estos mensajes de error es la causa principal del error 17204. Las causas comunes de estos mensajes de error son un problema de permisos o una ruta de acceso incorrecta al archivo.


## <a name="user-action"></a>Acción del usuario  
1. La resolución del error 17204 implica la comprensión del código de error del sistema operativo asociado y el diagnóstico del error. Una vez que se resuelva la condición de error del sistema operativo, puede intentar reiniciar la base de datos (con ALTER DATABASE SET ONLINE, por ejemplo) o la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para poner en línea la base de datos afectada. En algunos casos, es posible que no pueda resolver el error del sistema operativo. A continuación, tendrá que realizar acciones correctivas específicas. Trataremos estas acciones en esta sección.
1. Si el mensaje de error 17204 solo contiene un código de error y no una descripción del error, puede intentar resolver el código de error mediante el comando desde un shell del sistema operativo: net helpmsg <error code>. Si obtiene un código de estado de 8 dígitos como código de error, puede hacer referencia a las fuentes de información como [¿Cómo convertir un valor HRESULT en un código de error de Win32?](https://devblogs.microsoft.com/oldnewthing/20061103-07/?p=29133) para descodificar los códigos de estado en errores del sistema operativo.
1. Si obtiene el error `Access is Denied` del sistema operativo = 5, tenga en cuenta estos métodos:
   -  Compruebe los permisos que se establecen en el archivo examinando las propiedades del archivo en el Explorador de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza grupos de Windows para aprovisionar Access Control en los distintos recursos de archivo. Asegúrese de que el grupo adecuado [con nombres como SQLServerMSSQLUser$ComputerName$MSSQLSERVER o SQLServerMSSQLUser$ComputerName$InstanceName] tiene los permisos necesarios en el archivo de base de datos mencionado en el mensaje de error. Vea [Configurar permisos del sistema de archivos para el acceso al motor de base de datos](../../2014/database-engine/configure-windows/configure-file-system-permissions-for-database-engine-access.md) para obtener más información. Asegúrese de que el grupo de Windows incluye realmente la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el identificador de seguridad del servicio.
   -  Revise la cuenta de usuario en la que se ejecuta actualmente el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede usar el administrador de tareas de Windows para obtener esta información. Busque el valor "Nombre de usuario" para el archivo ejecutable "sqlservr.exe". Además, si ha cambiado recientemente la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe saber que la manera admitida para realizar esta operación es mediante la utilidad Administrador de configuración de SQL Server. Hay más información disponible en [Administrador de configuración de SQL Server](../sql-server-configuration-manager.md). 
   -  Dependiendo del tipo de operación, como abrir bases de datos durante el inicio del servidor, adjuntar una base de datos, restaurar una base de datos, etc., la cuenta que se usa para la suplantación y el acceso al archivo de base de datos puede variar. Revise el tema [Proteger archivos de datos y de registro](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms189128(v=sql.105)?redirectedfrom=MSDN) para comprender qué operación establece qué permiso y para qué cuentas. Use una herramienta como [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) de Windows SysInternals para saber si el acceso al archivo se produce en el contexto de seguridad de la cuenta de inicio del servicio de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o el identificador de seguridad del servicio, o una cuenta suplantada.

      Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suplanta las credenciales del usuario que ejecuta la operación ALTER DATABASE o CREATE DATABASE, verá la siguiente información en la herramienta Process Monitor (ejemplo):
        ```Date & Time:      3/27/2010 8:26:08 PM
        Event Class:        File System
        Operation:          CreateFile
        Result:                ACCESS DENIED
        Path:                  C:\Program Files\Microsoft SQL Server\MSSQL10.SQL2008\MSSQL\DATA\attach_test.mdf
        TID:                   4288
        Duration:             0.0000366
        Desired Access:Generic Read/Write
        Disposition:        Open
        Options:            Synchronous IO Non-Alert, Non-Directory File, Open No Recall
        Attributes:          N
        ShareMode:       Read
        AllocationSize:   n/a
        Impersonating: DomainName\UserName```
  
1. If you are getting `The system cannot find the file specified` OS error = 3:
   - Review the complete path from the error message
   - Ensure the disk drive and the folder path is visible and accessible from Windows Explorer
   - Review the Windows Event log to find out if any problems exist with this disk drive
   - If the path is incorrect and if this database already exists in the system, you can change the database file paths using the methods explained in the topic [Move Database Files](../databases/move-database-files.md). You may have to use this procedure, especially for system database files that encounter 17204 or 17207 and you are working through a disaster recovery scenario where the specified disk drives are unavailable. This topic also explains how you can identify the current location of the various system databases [master, model, tempdb, msdb and mssqlsystemresource].
   - If you see this error because the database files are missing, you have to restore the database from a valid backup.
     - If the database file associated with the error belongs to a secondary filegroup, then you can optionally mark that filegroup offline, bring the database online and then perform a restore of that filegroup alone. For more information, refer to the OFFLINE section of the topic [ALTER DATABASE File and Filegroup Options (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).
     - If the file that produced the error is a transaction log file, review the information under the sections "FOR ATTACH" and "FOR ATTACH_REBUILD_LOG" of the topic [CREATE DATABASE (Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md) to understand how you can recreate the missing transaction log files.
   - Ensure that any disk or network location [like iSCSI drive] is available before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attempts to access the database files on these locations. If needed create the required dependencies in Cluster Administrator or Service Control Manager.
1. If you're getting the `The process cannot access the file because it is being used by another process` operating system error = 32:
   - Use a tool like [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) or [Handle](https://docs.microsoft.com/sysinternals/downloads/handle) from Windows Sysinternals to find out if another process or service has acquired exclusive lock on this database file
   - Stop that process from accessing [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Database files. Common examples include anti-virus programs (see guidance for file exclusions in the following [KB article](https://support.microsoft.com/help/309422/choosing-antivirus-software-for-computers-that-run-sql-server) )
   - In a cluster environment, make sure that the sqlservr.exe process from the previous owning node has actually released the handles to the database files. Normally, this doesn't occur, but misconfigurations of the cluster or I/O paths can lead to such issues.
  
