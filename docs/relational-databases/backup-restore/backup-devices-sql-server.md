---
title: Dispositivos de copia de seguridad (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tape backup devices, about tape backup devices
- backup devices [SQL Server]
- disk backup devices [SQL Server]
- database backups [SQL Server], backup devices
- logical devices [SQL Server]
- backup devices [SQL Server], about backup devices
- backing up [SQL Server], backup devices
- removable media [SQL Server]
- network shares [SQL Server]
- backups [SQL Server], backup devices
- tape backup devices
- physical devices [SQL Server]
- backing up databases [SQL Server], backup devices
- devices [SQL Server]
ms.assetid: 35a8e100-3ff2-4844-a5da-dd088c43cba4
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 1dbf5d00855a498782a65a3ff04e2477a2cb871d
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="backup-devices-sql-server"></a>Dispositivos de copia de seguridad (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En una operación de copia de seguridad en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los datos copiados (la *copia de seguridad*) se escriben en un dispositivo físico de copia de seguridad. Este dispositivo físico de copia de seguridad se inicializa cuando se escribe en él la primera copia de seguridad de un conjunto de medios. Las copias de seguridad de uno o varios dispositivos de copia de seguridad constituyen un solo conjunto de medios.  
   
##  <a name="TermsAndDefinitions"></a> Términos y definiciones  
 disco de copia de seguridad  
 Disco duro u otro medio de almacenamiento en disco que contiene uno o varios archivos de copia de seguridad. Un archivo de copia de seguridad es un archivo normal del sistema operativo.  
  
 conjunto de medios  
 Colección ordenada de medios de copia de seguridad, ya sean cintas o archivos de disco, que usan un tipo y un número fijo de dispositivos de copia de seguridad. Para obtener más información sobre los conjuntos de medios, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
 dispositivo físico de copia de seguridad  
 Unidad de cinta o un archivo de disco proporcionado por el sistema operativo. Una copia de seguridad puede utilizar entre 1 y 64 dispositivos de copia de seguridad. Si una copia de seguridad requiere varios dispositivos de copia de seguridad, estos deben ser de un mismo tipo (disco o cinta).  
  
 Las copias de seguridad de SQL Server también se pueden escribir en un servicio de almacenamiento Blob de Microsoft Azure además de en disco o cinta.  
 
  
##  <a name="DiskBackups"></a> Uso de dispositivos de copia de seguridad en disco  
  
 Si un archivo de disco se llena mientras una operación de copia de seguridad está anexando una copia de seguridad al conjunto de medios, la operación producirá un error. El tamaño máximo de un archivo de copia de seguridad se determina de acuerdo con el espacio disponible en el dispositivo de disco, de modo que el tamaño apropiado para un dispositivo de copia de seguridad en disco dependerá del tamaño de las copias de seguridad.  
  
 Un dispositivo de copia de seguridad en disco puede ser un simple dispositivo de disco; por ejemplo, una unidad ATA. Como alternativa, se puede utilizar una unidad de disco de intercambio en actividad que permita sustituir de forma transparente un disco lleno por uno vacío. Un disco de copia de seguridad puede ser un disco local en el servidor o un disco remoto que sea un recurso de red compartido. Para obtener información acerca de cómo utilizar un disco remoto, vea [Realizar una copia de seguridad en un archivo de un recurso compartido de red](#NetworkShare)más adelante en este mismo tema.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Las herramientas de administración son muy flexibles para el control de los dispositivos de copia de seguridad en disco, ya que generan de forma automática un nombre con marca de tiempo en el archivo de disco.  
  
> **IMPORTANTE:** Se recomienda que el disco de copia de seguridad no sea el disco de datos o del registro de la base de datos. Esto es necesario para garantizar el acceso a las copias de seguridad si el disco de datos o del registro presenta errores. 
>
>Si los archivos de base de datos y los archivos de copia de seguridad están en el mismo dispositivo y este sufre un error, la base de datos y las copias de seguridad no estarán disponibles. Además, al colocar los archivos de base de datos y los archivos de copia de seguridad en dispositivos independientes, mejora el rendimiento de E/S en el uso en producción de la base de datos y en la escritura de las copias de seguridad.
  
##  <a name="BackupFileUsingPhysicalName"></a> Especificar un archivo de copia de seguridad mediante su nombre físico (Transact-SQL)  
 La sintaxis básica de [BACKUP](../../t-sql/statements/backup-transact-sql.md) para especificar un archivo de copia de seguridad mediante su nombre de dispositivo físico es:  
  
 BACKUP DATABASE *database_name*  
  
 TO DISK **=** { **'***nombre_de_dispositivo_de_copia_de_seguridad_física***'** | **@***variable_de_nombre_de_dispositivo_de_copia_de_seguridad_física* }  
  
 Por ejemplo:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';  
GO  
```  
  
 Para especificar un dispositivo de disco físico en una instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) , la sintaxis básica es:  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM DISK **=** { **'***nombre_de_dispositivo_de_copia_de_seguridad_física***'** | **@***variable_de_nombre_de_dispositivo_de_copia_de_seguridad_física* }  
  
 Por ejemplo,  
  
```  
RESTORE DATABASE AdventureWorks2012   
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak';   
```  
  
  
##  <a name="BackupFileDiskPath"></a> Especificar la ruta de acceso del archivo de copia de seguridad en disco 
 Cuando se especifica un archivo de copia de seguridad, se debe especificar ruta de acceso completa y el nombre de archivo. Si especifica solo el nombre de archivo o la ruta de acceso relativa al realizar la copia de seguridad de un archivo, el archivo de copia de seguridad se sitúa en el directorio predeterminado de copias de seguridad. El directorio predeterminado de copias de seguridad es C:\Archivos de programa\Microsoft SQL Server\MSSQL.*n*\MSSQL\Backup, donde *n* es el número de la instancia de servidor. Por lo tanto, para la instancia de servidor predeterminada, el directorio predeterminado de copia de seguridad es C:\Archivos de programa\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Backup.  
  
 Para evitar ambigüedades, particularmente en los scripts, recomendamos especificar de forma explícita la ruta de acceso del directorio de copias de seguridad en cada cláusula DISK. Sin embargo, esto es menos importante cuando se utiliza el Editor de consultas. En ese caso, si está seguro de que el archivo de copia de seguridad reside en el directorio predeterminado de copias de seguridad, puede omitir la ruta de acceso de una cláusula DISK. Por ejemplo, la siguiente instrucción `BACKUP` realiza una copia de seguridad de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en el directorio predeterminado de copias de seguridad.  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = ’AdventureWorks2012.bak’;  
GO  
```  
  
> **NOTA:** La ubicación predeterminada se almacena en la clave del Registro **BackupDirectory** en **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.n\MSSQLServer**.  
  
   
###  <a name="NetworkShare"></a> Copia de seguridad en un archivo de recurso compartido de red  
 Para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueda tener acceso a un archivo de disco remoto, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener acceso al recurso compartido de red. Esto incluye disponer de los permisos necesarios para realizar operaciones de copia de seguridad y restauración, escribiendo y leyendo en el recurso compartido de red. La disponibilidad de las unidades de red y los permisos depende del contexto en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Para realizar una copia de seguridad en una unidad de red cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en ejecución en una cuenta de usuario de dominio, se debe asignar la unidad compartida como una unidad de red en la sesión donde se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si inicia Sqlservr.exe desde la línea de comandos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta todas las unidades de red que ha asignado en la sesión que ha iniciado.  
  
-   Sin embargo, cuando ejecuta Sqlservr.exe como un servicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en una sesión independiente que no tiene relación con la sesión que ha iniciado. La sesión en la que se ejecuta un servicio puede tener sus propias unidades asignadas, aunque normalmente no lo están.  
  
-   Puede conectarse a la cuenta de servicio de red mediante la cuenta del equipo en lugar de un usuario de dominio. Para permitir copias de seguridad desde equipos específicos en una unidad compartida, se debe conceder acceso a las cuentas del equipo. El usuario que envía el comando BACKUP puede o no tener acceso; esto resulta irrelevante siempre que el proceso Sqlservr.exe que está realizando la copia de seguridad disponga de acceso.  
  
    > **IMPORTANTE:** Debido a que la realización de copias de seguridad de datos a través de una red está expuesta a errores, se recomienda que, cuando se utiliza un disco remoto, compruebe la operación de copia de seguridad una vez finalizada. Para obtener más información, vea [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
## <a name="specify-a-universal-naming-convention-unc-name"></a>Especificar un nombre UNC (Convención de nomenclatura universal)  
 Para especificar un recurso compartido de red en un comando de copia de seguridad o restauración, use el nombre UNC (convención de nomenclatura universal) completo del archivo para el dispositivo de copia de seguridad. Un nombre UNC tiene el formato **\\\\***NombreDeSistema***\\***NombDereRecursoCompartido***\\***RutaDeAcceso***\\***NombreDeArchivo*.  
  
 Por ejemplo:  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO DISK = '\\BackupSystem\BackupDisk1\AW_backups\AdventureWorksData.Bak';  
GO  
```  
  
 
##  <a name="TapeDevices"></a> Uso de dispositivos de cinta  
  
> **NOTA:** La compatibilidad con dispositivos de cinta de copia de seguridad se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
   
 Realizar copias de seguridad de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una cinta requiere que las unidades de cinta sean compatibles con el sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Además, es recomendable utilizar solo las cintas que el fabricante recomienda para una unidad de cinta determinada. Para obtener más información acerca de cómo instalar una unidad de cinta, vea la documentación del sistema operativo Windows.  
  
 Cuando se utiliza una unidad de cinta, una operación de copia de seguridad puede llenar una cinta y continuar en otra. Cada cinta contiene un encabezado de medios. El primer medio que se utiliza se denomina *cinta inicial*. Cada cinta sucesiva se denomina *cinta de continuación* y tiene un número de secuencia de medio superior en una unidad a la cinta anterior. Por ejemplo, un conjunto de medios asociado con cuatro dispositivos de cinta contiene al menos cuatro cintas iniciales (y, si no hay capacidad para la base de datos, cuatro series de cintas de continuación). Cuando adjunte un conjunto de copia de seguridad, debe montar la última cinta de la serie. Si no monta la última cinta, [!INCLUDE[ssDE](../../includes/ssde-md.md)] busca hacia adelante hasta el final de la cinta montada y le solicita que cambie la cinta. En ese punto, monte la última cinta.  
  
 Los dispositivos de copia de seguridad en cinta se utilizan como los dispositivos de disco, con las excepciones siguientes:  
  
-   El dispositivo de cinta debe estar conectado físicamente al equipo donde se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No se admite la creación de copias de seguridad en dispositivos de cinta remotos.  
  
-   Si un dispositivo de copia de seguridad en cinta se llena durante la operación de copia de seguridad, pero todavía faltan por escribir más datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pedirá una nueva cinta y continuará con la operación de copia de seguridad una vez que la cinta se haya cargado.  
  
##  <a name="BackupTapeUsingPhysicalName"></a> Especificar una cinta de copia de seguridad mediante su nombre físico (Transact-SQL)  
 La sintaxis básica de [BACKUP](../../t-sql/statements/backup-transact-sql.md) para especificar una cinta de copia de seguridad mediante el nombre de dispositivo físico de la unidad de cinta es:  
  
 BACKUP { DATABASE | LOG } *database_name*  
  
 TO TAPE **=** { **'***nombre_de_dispositivo_de_copia_seguridad_física***'** | **@***variable_de_nombre_de_dispositivo_de_copia_seguridad_física* }  
  
 Por ejemplo:  
  
```  
BACKUP LOG AdventureWorks2012   
   TO TAPE = '\\.\tape0';  
GO  
```  
  
 Para especificar un dispositivo de cinta físico en una instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) , la sintaxis básica es:  
  
 RESTORE { DATABASE | LOG } *database_name*  
  
 FROM TAPE **=** { **'***nombre_de_dispositivo_de_copia_de_seguridad_física***'** | **@***nombre_de_dispositivo_de_copia_de_seguridad_física* }  
  
###  <a name="TapeOptions"></a> Opciones BACKUP y RESTORE específicas de cinta (Transact-SQL)  
 Para facilitar la administración de cintas, la instrucción BACKUP proporciona las siguientes opciones específicas:  
  
-   { NOUNLOAD | **UNLOAD** }  
  
     Se puede controlar si una cinta de copia de seguridad se descargará automáticamente de la unidad de cinta después de una operación de copia de seguridad o restauración. UNLOAD/NOUNLOAD es una configuración de sesión que persiste mientras dure la sesión o hasta que se restablezca especificando la alternativa.  
  
-   { **REWIND** | NOREWIND }  
  
     Se puede controlar si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene abierto el resto de la cinta después de la operación de copia de seguridad o restauración, o si libera y rebobina la cinta una vez se llena. El comportamiento predeterminado es rebobinar la cinta (REWIND).  
  
> **NOTA:** Para obtener más información sobre la sintaxis y los argumentos de BACKUP, consulte [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md). Para obtener más información sobre los argumentos y la sintaxis de RESTORE, vea [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md) y [RESTORE &#40;argumentos, Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md), respectivamente.  
  
###  <a name="OpenTapes"></a> Administración de cintas abiertas  
 Para ver una lista de los dispositivos de cinta abiertos y el estado de las solicitudes de montaje, vea la vista de administración dinámica [sys.dm_io_backup_tapes](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) . En esta vista se muestran todas las cintas abiertas. Se incluyen las cintas en uso que se encuentran temporalmente inactivas mientras esperan a la siguiente operación BACKUP o RESTORE.  
  
 Si deja abierta la cinta accidentalmente, la manera más rápida de liberarla es usar el siguiente comando: RESTORE REWINDONLY FROM TAPE**=***nombre_de_dispositivo_de_copia_de_seguridad*. Para obtener más información, vea [RESTORE REWINDONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-rewindonly-transact-sql.md).  
  
  
## <a name="using-the-windows-azure-blob-storage-service"></a>Uso del servicio Blob Storage de Microsoft Azure  
 Las copias de seguridad de SQL Server se pueden escribir en un servicio de almacenamiento Blob de Windows Azure.  Para obtener más información sobre cómo usar el servicio de almacenamiento de blobs de Windows Azure para las copias de seguridad, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
##  <a name="LogicalBackupDevice"></a> Usar un dispositivo lógico de copia de seguridad  
 Un *dispositivo lógico de copia de seguridad* es un nombre opcional y definido por el usuario que apunta a un dispositivo físico de copia de seguridad específico (un archivo de disco o una unidad de cinta). Un dispositivo lógico de copia de seguridad permite usar el direccionamiento indirecto cuando se hace referencia al dispositivo físico de copia de seguridad correspondiente.  
  
 Definir un dispositivo lógico de copia de seguridad requiere la asignación de un nombre lógico a un dispositivo físico. Por ejemplo, puede definirse el dispositivo lógico AdventureWorksBackups para que apunte al archivo Z:\SQLServerBackups\AdventureWorks2012.bak o a la unidad de cinta \\\\.\tape0. De esta forma, los comandos de copias de seguridad y restauración pueden especificar AdventureWorksBackups como dispositivo de copia de seguridad, en lugar de DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' o TAPE = '\\\\.\tape0'.  
  
 El nombre de dispositivo lógico debe ser único entre todos los dispositivos lógicos de copia de seguridad de la instancia de servidor. Para ver los nombres de los dispositivos lógicos existentes, consulte la vista de catálogo [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) . Esta vista muestra el nombre de cada dispositivo lógico de copia de seguridad y describe el tipo y la ruta de acceso o el nombre de archivo físico del dispositivo de copia de seguridad físico correspondiente.  
  
 Una vez definido el dispositivo lógico de copia de seguridad, en un comando BACKUP o RESTORE, puede especificar el dispositivo lógico de copia de seguridad en lugar del nombre físico del dispositivo. Por ejemplo, la siguiente instrucción realiza una copia de seguridad de la base de datos `AdventureWorks2012` en el dispositivo lógico de copia de seguridad `AdventureWorksBackups` .  
  
```  
BACKUP DATABASE AdventureWorks2012   
   TO AdventureWorksBackups;  
GO  
```  
  
> **NOTA:** En una determinada instrucción BACKUP o RESTORE, el nombre de dispositivo lógico de copia de seguridad y el nombre del dispositivo físico correspondiente son intercambiables.  
  
 Una ventaja de usar un dispositivo lógico de copia de seguridad es que resulta más sencillo de usar que una larga ruta de acceso. Utilizar un dispositivo lógico de copia de seguridad puede ser útil si tiene previsto escribir una serie de copias de seguridad en la misma ruta de acceso o en un dispositivo de cinta. Los dispositivos lógicos de copia de seguridad resultan muy útiles para identificar los dispositivos de copia de seguridad en cinta.  
  
 Se puede escribir un script de copia de seguridad para usar un dispositivo lógico específico. Esto permite cambiar a un nuevo dispositivo de copia de seguridad físico sin actualizar el script. El cambio implica el siguiente proceso:  
  
1.  Quitar el dispositivo lógico de copia de seguridad original.  
  
2.  Definir un nuevo dispositivo lógico de copia de seguridad que utilice el nombre de dispositivo lógico original pero que se asigne a un dispositivo de copia de seguridad físico distinto. Los dispositivos lógicos de copia de seguridad resultan muy útiles para identificar los dispositivos de copia de seguridad en cinta.  
  
  
##  <a name="MirroredMediaSets"></a> Conjuntos de medios de copia de seguridad reflejados  
 La creación de reflejos de los conjuntos de medios de copia de seguridad reduce el efecto de los errores de funcionamiento de los dispositivos de copia de seguridad. Los errores de funcionamiento son especialmente graves porque las copias de seguridad son el último recurso para evitar la pérdida de datos. A medida que aumenta el tamaño de una base de datos, aumentan las posibilidades de que un error de un dispositivo o medio de copia de seguridad provoque que no se pueda restaurar una copia de seguridad. La creación de reflejo de los medios de copia de seguridad aumenta la confiabilidad de las copias de seguridad al proporcionar redundancia para el dispositivo físico. Para obtener más información, vea [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md).  
  
> **NOTA:** Los conjuntos de medios de copia de seguridad reflejados solo se admiten en [!INCLUDE[ssEnterpriseEd2005](../../includes/ssenterpriseed2005-md.md)] y en versiones posteriores.  
  
  
##  <a name="Archiving"></a> Archivar copias de seguridad de SQL Server  
 Se recomienda que use una utilidad de copia de seguridad del sistema de archivos para archivar las copias de seguridad en disco y que guarde los archivos fuera de las instalaciones. El uso de discos tiene la ventaja de poder utilizar la red para escribir las copias de seguridad archivadas en un disco fuera de las instalaciones. El servicio de almacenamiento Blob de Windows Azure se puede utilizar como una opción de archivado externo.  Puede cargar las copias de seguridad en disco, o escribir directamente las copias de seguridad en el servicio de almacenamiento Blob de Windows Azure.  
  
 Otro método común de archivado consiste en escribir las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un disco local de copia de seguridad, archivarlas en cinta y guardar estas cintas fuera de las instalaciones.  

  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para especificar un dispositivo de disco (SQL Server Management Studio)**  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **Para especificar un dispositivo de cinta (SQL Server Management Studio)**  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
 **Para definir un dispositivo lógico de copia de seguridad**  
  
-   [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.BackupDevice> (SMO)  
  
 **Para usar un dispositivo lógico de copia de seguridad**  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
-   [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
 **Para consultar la información acerca de los dispositivos de copia de seguridad**  
  
-   [Historial de copias de seguridad e información de encabezados &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
 **Para eliminar un dispositivo lógico de copia de seguridad**  
  
-   [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)  
  
-   [Eliminar un dispositivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Backup Device (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sys.dm_io_backup_tapes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md)   
 [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)  
  
  
