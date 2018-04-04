---
title: Copia de bases de datos con Copias de seguridad y restauración | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], back up and restore
- restoring databases [SQL Server], previous SQL Server versions
- database restores [SQL Server], copying databases
- restoring databases [SQL Server], onto another server instance
- restoring [SQL Server], onto another server instance
- backing up databases [SQL Server], copying databases
- database backups [SQL Server], copying databases
ms.assetid: b93e9701-72a0-408e-958c-dc196872c040
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: f5555b305edf4ac249959e77d4a68c07c72efef5
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="copy-databases-with-backup-and-restore"></a>Copiar bases de datos con Copias de seguridad y restauración
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede crear una base de datos nueva restaurando una copia de seguridad de una base de datos de usuario creada utilizando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior. Sin embargo, las copias de seguridad de las bases de datos **maestra**, **modelo** y **msdb** creadas utilizando una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueden restaurarse con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Asimismo, las copias de seguridad de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se pueden restaurar con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
>**IMPORTANTE:** SQL Server 2016 usa una ruta de acceso predeterminada distinta de la de versiones anteriores. Por lo tanto, para restaurar copias de seguridad de una base de datos creadas en la ubicación predeterminada de versiones anteriores es preciso utilizar la opción MOVE. Para obtener información acerca de la nueva ruta de acceso predeterminada, vea [Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md). Para obtener más información acerca de cómo mover archivos de base de datos, vea el apartado "Mover los archivos de base de datos" que figura más adelante en este tema.  
  
## <a name="general-steps-for-using-backup-and-restore-to-copy-a-database"></a>Pasos generales para usar copias de seguridad y restauración para copiar una base de datos  
 Cuando se usan copias de seguridad y restauración para copiar una base de datos a otra versión de SQL Server, los equipos de origen y de destino pueden ser de cualquier plataforma en la que se ejecute SQL Server.  
  
 Los pasos generales son:  
  
1.  Cree una copia de seguridad de la base de datos de origen que pueda residir en una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior. El equipo en el que se ejecute esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será el **equipo de origen**.  
  
2.  En el equipo al que quiera copiar la base de datos (el **equipo de destino**), conéctese a una sesión de SQL Server en la que tenga previsto restaurar la base de datos. Si es necesario, cree en la instancia de servidor de **destino** los mismos dispositivos de copia de seguridad usados para la copia de seguridad de las bases de datos de **origen** .  
  
3.  Restaure la copia de seguridad de la base de datos de **origen** en el equipo de **destino** . Al restaurar la base de datos se crean automáticamente todos los archivos de la base de datos.  
  
Estos son otros aspectos que pueden afectar al proceso:
  
## <a name="before-you-restore-database-files"></a>Antes de restaurar archivos de base de datos  
 La restauración de una base de datos crea automáticamente los archivos de base de datos necesarios para la base de datos que se restaura. Los archivos que SQL Server crea durante el proceso de restauración usan de forma predeterminada los mismos nombres y las mismas rutas de acceso que los archivos de copia de seguridad de la base de datos original en el equipo de origen.  
  
 Opcionalmente, cuando se restaura la base de datos se pueden especificar la asignación de dispositivos, los nombres de archivo o la ruta de acceso para dicha base de datos. 
 
 Esto puede ser necesario en las situaciones siguientes:  
  
-   La asignación de unidades o la estructura de directorios utilizadas por la base de datos en el equipo original no existen en el otro equipo. Por ejemplo, quizás la copia de seguridad contiene un archivo que se restauraría en la unidad E de forma predeterminada, pero el equipo de destino no tiene una unidad E.  
  
-   Es posible que no haya espacio suficiente en la ubicación de destino.  
  
-   Se está utilizando un nombre de base de datos que existe en el destino de restauración y alguno de los archivos tiene el mismo nombre que un archivo de base de datos del conjunto de copia de seguridad; puede ocurrir lo siguiente:  
  
    -   Si el archivo de base de datos existente se puede sobrescribir, se sobrescribirá (esto no afectaría a un archivo que perteneciese a un nombre de base de datos diferente).  
  
    -   Si el archivo existente no se puede sobrescribir, se producirá un error de restauración.  
  
 Para evitar errores y consecuencias no deseadas, antes de la operación de restauración puede usar la tabla de historial [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md) para buscar los archivos de base de datos y de registro en la copia de seguridad que va a restaurar.  
  
## <a name="moving-the-database-files"></a>Mover los archivos de base de datos  
 Si no se pueden restaurar los archivos de la copia de seguridad de la base de datos en el equipo de destino, es necesario mover los archivos a una nueva ubicación a medida que se restauran. Por ejemplo:  
  
-   Suponga que desea restaurar una base de datos a partir de las copias de seguridad creadas en la ubicación predeterminada de la versión anterior.  
  
-   Puede ser necesario restaurar algunos archivos de base de datos de la copia de seguridad en una unidad diferente debido a consideraciones de capacidad. Se trata de un hecho frecuente, porque la mayor parte de los equipos de una organización no tienen el mismo número y tamaño de unidades de disco o idénticas configuraciones de software.  
  
-   Puede ser necesario crear una copia de una base de datos existente en el mismo equipo para realizar pruebas. En este caso, los archivos de la base de datos original ya existen, por lo que hay que especificar diferentes nombres de archivo al crear la copia de la base de datos durante la operación de restauración.  
  
 Para obtener más información, vea el apartado "Para restaurar archivos y grupos de archivos en una nueva ubicación" que figura más adelante en este mismo tema.  
  
## <a name="changing-the-database-name"></a>Cambiar el nombre de la base de datos  
 Se puede cambiar el nombre de la base de datos cuando se restaura en el equipo de destino, sin necesidad de restaurar primero la base de datos y después cambiar manualmente el nombre. Por ejemplo, es posible que sea necesario cambiar el nombre de la base de datos de **Sales** a **SalesCopy** para indicar que se trata de una copia de la base de datos.  
  
 El nombre de base de datos que se proporciona explícitamente al restaurar una base de datos se usa de forma automática como el nuevo nombre de la base de datos. Debido a que el nombre de la base de datos no existe, se crea uno nuevo con los archivos de la copia de seguridad.  
  
## <a name="when-upgrading-a-database-by-using-restore"></a>Actualizar una base de datos por medio de la restauración  
 Al restaurar copias de seguridad de una versión anterior, es útil conocer de antemano si la ruta de acceso (unidad y directorio) de cada uno de los catálogos de texto completo de una copia de seguridad existe en el equipo de destino. Para obtener una lista de los nombres lógicos y físicos, la ruta de acceso y el nombre de archivo de todos los archivos de una copia de seguridad, incluidos los archivos de catálogo, use una instrucción RESTORE FILELISTONLY FROM *<backup_device>*. Para obtener más información, vea [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md).  
  
 Si no existe la misma ruta de acceso en el equipo de destino, son dos las alternativas válidas:  
  
-   Cree la asignación de unidades/directorios equivalente en el equipo de destino.  
  
-   Mueva los archivos de catálogo a una ubicación nueva durante la operación de restauración con la cláusula WITH MOVE de la instrucción RESTORE DATABASE. Para obtener más información, vea [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
 Para obtener más información sobre las opciones alternativas para actualizar índices de texto completo, vea [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
## <a name="database-ownership"></a>Propiedad de la base de datos  
 Cuando se restaura una base de datos en otro equipo, el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el usuario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que inicia la operación de restauración se convierte automáticamente en el propietario de la nueva base de datos. Una vez restaurada la base de datos, el administrador del sistema o el nuevo propietario de la base de datos pueden cambiar la propiedad de la base de datos. Para evitar restauraciones no autorizadas de una base de datos, utilice contraseñas en los medios o en el conjunto de copia de seguridad.  
  
## <a name="managing-metadata-when-restoring-to-another-server-instance"></a>Administrar metadatos al restaurar una base de datos en otra instancia de servidor  
 Al restaurar una base de datos en otra instancia de servidor, para proporcionar una experiencia coherente a los usuarios y las aplicaciones, puede que tenga que volver a crear algunos o todos los metadatos de la base de datos, por ejemplo los inicios de sesión y los trabajos, en la otra instancia de servidor. Para obtener más información, vea [Administrar los metadatos cuando una base de datos pasa a estar disponible en otra instancia del servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
 **Ver los archivos de datos y de registro en un conjunto de copia de seguridad**  
  
-   [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)  
  
 **Restaurar archivos y grupos de archivos en una nueva ubicación**  
  
-   [Restaurar archivos en una nueva ubicación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Restaurar archivos y grupos de archivos en archivos existentes**  
  
-   [Restaurar archivos y grupos de archivos en archivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
 **Restaurar una base de datos con un nuevo nombre**  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **Reiniciar una operación de restauración interrumpida**  
  
-   [Reiniciar una operación de restauración interrumpida &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
 **Cambiar el propietario de la base de datos**  
  
-   [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)  
  
 **Copiar una base de datos con objetos de administración de SQL Server (SMO)**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.RelocateFiles%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReplaceDatabase%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
## <a name="see-also"></a>Vea también  
 [Copiar bases de datos en otros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
