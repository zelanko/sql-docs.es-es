---
title: "Backup Overview (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "07/15/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tablas [SQL Server], copia de seguridad de datos"
  - "copias de seguridad [SQL Server]"
  - "copias de seguridad de base de datos [SQL Server]"
  - "copia de seguridad, tipos [SQL Server]"
  - "copias de seguridad de datos [SQL Server]"
  - "realizar copias de seguridad de las tablas [SQL Server]"
  - "restauraciones de base de datos [SQL Server], copias de seguridad"
  - "restaurar [SQL Server], sobre la copia de seguridad"
  - "restaurar [SQL Server], tipos de copia de seguridad"
  - "copias de seguridad [SQL Server], acerca de"
  - "backups [SQL Server], table-level backups unsupported"
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
caps.latest.revision: 84
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 84
---
# Backup Overview (SQL Server)
  En este tema se presenta el componente de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La copia de seguridad de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es esencial para proteger los datos. En esta descripción se tratan los tipos y las restricciones de copia de seguridad. En el tema también se presentan los dispositivos y los medios de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
## Términos
 
 **realizar copia de seguridad [verbo]**  
 Copia los datos o las entradas de registro de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o de su registro de transacciones en un dispositivo de copia de seguridad, como un disco, para crear una copia de seguridad de datos o de registros.  
  
**copia de seguridad [nombre]**  
 Copia de los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se puede usar para restaurar y recuperar los datos después de un error. Se crea una copia de seguridad de los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el nivel de una base de datos o de uno o varios de los archivos o grupos de archivos. No pueden crearse copias de seguridad de las tablas. Además de las copias de seguridad de datos, el modelo de recuperación completa requiere crear copias de seguridad del registro de transacciones.  
  
**[modelo de recuperación](../../relational-databases/backup-restore/recovery-models-sql-server.md)**  
 Propiedad de la base de datos que controla el mantenimiento del registro de transacciones de una base de datos. Existen tres modelos de recuperación: simple, completa y por medio de registros de operaciones masivas. El modelo de recuperación de la base de datos determina sus requisitos de copias de seguridad y restauración.  
  
 **[restaurar](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)**  
 Proceso de varias fases que copia todos los datos y páginas del registro desde una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificada a una base de datos especificada y, a continuación, pone al día todas las transacciones registradas en la copia de seguridad mediante la aplicación de los cambios registrados para poner los datos al día.  
  
 ## Tipos de copias de seguridad  
  
 **[copia de seguridad de solo copia](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)**  
 Copia de seguridad de uso especial independiente de la secuencia normal de copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**copia de seguridad de datos**   
 Copia de seguridad de datos de una base de datos completa (copia de seguridad de base de datos), una base de datos parcial (copia de seguridad parcial) o un conjunto de archivos de datos o grupos de archivos (copia de seguridad de archivos).  
  
**[copia de seguridad de base de datos](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 Copia de seguridad de una base de datos. Las copias de seguridad completas representan la base de datos completa en el momento en que finalizó la copia de seguridad. Las copias de seguridad diferenciales solo contienen los cambios realizados en la base de datos desde la copia de seguridad completa más reciente.  
  
 **[copia de seguridad diferencial](../../relational-databases/backup-restore/full-database-backups-sql-server.md)**  
 Copia de seguridad de datos basada en la última copia de seguridad completa de una base de datos completa o parcial o de un conjunto de archivos de datos o grupos de archivos (*base diferencial*) y que solo incluye las extensiones de datos que han cambiado desde la última base diferencial.  
  
 Una copia de seguridad diferencial parcial únicamente registra las extensiones de datos que han cambiado en grupos de archivos desde la copia de seguridad parcial anterior, que se conoce como la base para la diferencial.  
  
**copia de seguridad completa**  
 Copia de seguridad completa que incluye todos los datos de una base de datos determinada o un conjunto de grupos de archivos o archivos, así como una cantidad suficiente del registro como para permitir la recuperación de datos.  
  
**[copia de seguridad de registros](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)**  
 Copia de seguridad de los registros de transacciones que incluye todos los registros no guardados en una copia de seguridad de registros anterior. (modelo de recuperación completa)  
  
 **[copia de seguridad de archivos](../../relational-databases/backup-restore/full-file-backups-sql-server.md)**  
 Copia de seguridad de uno o varios archivos de base de datos o grupos de archivos.  
  
 **[copia de seguridad parcial](../../relational-databases/backup-restore/partial-backups-sql-server.md)**  
 Contiene datos de algunos de los grupos de archivos de una base de datos, incluidos los datos del grupo de archivos principal, todos los grupos de archivos de lectura/escritura, y los archivos de solo lectura opcionalmente especificados.  
  
## Términos y definiciones de medios de copia de seguridad  
  
 **[dispositivo de copia de seguridad](../../relational-databases/backup-restore/backup-devices-sql-server.md)**  
 Disco o dispositivo de cinta en el que se escriben las copias de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y del que se pueden restaurar. Las copias de seguridad de SQL Server también se pueden escribir en un servicio de Almacenamiento de blobs de Microsoft Azure y el formato de **URL** se usa para especificar el destino y el nombre del archivo de copia de seguridad. Para obtener más información, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 **[medio de copia de seguridad](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Una o varias cintas o archivos de disco en los que se han escrito una o varias copias de seguridad.  
  
 **[conjunto de copia de seguridad](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Contenido de la copia de seguridad que se agrega a un conjunto de medios mediante una operación de copia de seguridad correcta.  
  
 **[familia de medios](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Copias de seguridad creadas en un único dispositivo no reflejado o en un conjunto de dispositivos reflejados en un conjunto de medios.  
  
 **[conjunto de medios](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)**  
 Colección ordenada de medios de copia de seguridad, cintas o archivos de disco en la que se han escrito una o varias operaciones de copia de seguridad mediante un tipo y número fijo de dispositivos de copia de seguridad.  
  
 **[conjunto de medios reflejado](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)**  
 Varias copias (reflejos) de un conjunto de medios.  
  
##  <a name="BackupCompression"></a> Compresión de copia de seguridad  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] y versiones posteriores admiten la compresión de copias de seguridad, y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores pueden restaurar una copia de seguridad comprimida. Para obtener más información, vea [Compresión de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).  
  
##  <a name="Restrictions"></a>  Restricciones en las operaciones de copia de seguridad 
 Se puede realizar la copia de seguridad mientras la base de datos está en línea y en uso. Sin embargo, existen las siguientes restricciones.  
  
### No se pueden realizar copias de seguridad de datos sin conexión  
 Cualquier operación de copia de seguridad en la que se haga referencia de forma implícita o explícita a datos sin conexión provocará un error. A continuación, se exponen algunos ejemplos habituales:  
  
-   Se solicita una copia de seguridad de base de datos completa, pero un grupo de archivos de la base de datos está sin conexión. Puesto que todos los grupos de archivos se incluyen de forma implícita en las copias de seguridad de base de datos completas, esta operación provocará un error.  
  
     Para realizar una copia de seguridad de esta base de datos, se puede utilizar una copia de seguridad de archivos y especificar solo los grupos de archivos que estén en línea.  
  
-   Se solicita una copia de seguridad parcial, pero un grupo de archivos de lectura/escritura está sin conexión. Puesto que todos los grupos de archivos de lectura/escritura son obligatorios para las copias de seguridad parciales, esta operación provocará un error.  
  
-   Se solicita una copia de seguridad de determinados archivos, pero uno de ellos no está en línea. Se produce un error en la operación. Para realizar una copia de seguridad de los archivos en línea, puede omitir el archivo sin conexión de la lista y repetir la operación.  
  
 Normalmente, la copia de seguridad de registros será correcta aunque uno o varios de los archivos de datos no estén disponibles. Sin embargo, si algún archivo incluye cambios registrados de forma masiva realizados en el modelo de recuperación optimizado para cargas masivas de registros, todos los archivos deberán estar en línea para que la copia de seguridad sea correcta.  
  
### Restricciones de simultaneidad   
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el proceso de copia de seguridad en línea para permitir que se realice la copia de seguridad de una base de datos mientras se está utilizando. Durante la copia de seguridad, se pueden realizar la mayoría de las operaciones (por ejemplo, las instrucciones INSERT, UPDATE o DELETE están permitidas durante la operación de copia de seguridad). Sin embargo, si intenta iniciar una operación de copia de seguridad durante la creación o eliminación de un archivo de la base de datos, la operación de copia de seguridad esperará hasta que la creación o eliminación haya terminado o hasta que se agote el tiempo de espera de la copia de seguridad.  
  
 Las operaciones que no se pueden ejecutar durante la copia de seguridad de la base de datos o del registro de transacciones son las siguientes:  
  
-   Operaciones de administración de archivos, como la instrucción ALTER DATABASE con la opción ADD FILE o la opción REMOVE FILE.  
  
-   Operaciones de reducción de la base de datos o de reducción de un archivo. Esto incluye las operaciones de reducción automática.  
  
-   Si intenta crear o eliminar un archivo de la base de datos durante la operación de copia de seguridad, se producirá un error en la operación de creación o eliminación.  
  
 Si una operación de copia de seguridad se superpone a una operación de administración de archivos o de reducción, surge un conflicto. Con independencia de la operación en conflicto que empieza en primer lugar, la segunda operación espera a que se agote el tiempo de espera del bloqueo establecido por la primera operación. (El tiempo de espera se controla mediante un valor de tiempo de espera de sesión). Si el bloqueo se libera durante el tiempo de espera, la segunda operación continúa. Si se agota el tiempo de espera del bloqueo, la segunda operación no se realiza correctamente.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Dispositivos y medios de copia de seguridad**  
  
-   [Definir un dispositivo lógico de copia de seguridad para un archivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar un disco o una cinta como destino de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Eliminar un dispositivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Establecer la fecha de expiración de una copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Ver los archivos de datos y de registro en un conjunto de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
-   [Tutorial: copias de seguridad y restauración de SQL Server en el servicio de almacenamiento Blob de Windows Azure](../Topic/Tutorial:%20SQL%20Server%20Backup%20and%20Restore%20to%20Windows%20Azure%20Blob%20Storage%20Service.md)  
  
 **Crear una copia de seguridad**  
  
> [!NOTE]  
>  En el caso de copias de seguridad parciales o de solo copia, debe usar la instrucción [BACKUP](../../t-sql/statements/backup-transact-sql.md) de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la opción PARTIAL o COPY_ONLY, respectivamente.  
  
-   [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Realizar una copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Realizar copias de seguridad de archivos y grupos de archivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Crear una copia de seguridad diferencial de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Habilitar o deshabilitar sumas de comprobación de copia de seguridad durante copia de seguridad o restauración &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Especificar si una operación de copia de seguridad o restauración continúa o se detiene después de encontrar un error &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify if backup or restore continues or stops after error.md)  
  
-   [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Tutorial: copias de seguridad y restauración de SQL Server en el servicio de almacenamiento Blob de Windows Azure](../Topic/Tutorial:%20SQL%20Server%20Backup%20and%20Restore%20to%20Windows%20Azure%20Blob%20Storage%20Service.md)  
  
## Y más. 
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
  