---
title: Copia de seguridad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BACKUP_TSQL
- BACKUP
- BACKUP_DATABASE_TSQL
- BACKUP_LOG_TSQL
- BACKUP LOG
- BACKUP DATABASE
dev_langs: TSQL
helpviewer_keywords:
- backup media [SQL Server], BACKUP statement
- backing up filegroups [SQL Server]
- backup file formats [SQL Server]
- backups [SQL Server]
- database backups [SQL Server], BACKUP statement
- multifamily media sets [SQL Server]
- mirrored media sets [SQL Server]
- backing up files [SQL Server]
- backup sets [SQL Server], BACKUP statement
- backup compression [SQL Server], BACKUP statement
- BACKUP statement
- backups [SQL Server], BACKUP statement
- backup history tables [SQL Server]
- transaction log backups [SQL Server], BACKUP LOG statement
- READ_WRITE_FILEGROUPS option
- BACKUP DATABASE statement
- concurrency [SQL Server], backups
- backing up databases [SQL Server]
- passwords [SQL Server], backups
- security [SQL Server], backups
- media families [SQL Server]
- BACKUP LOG statement
- backing up transaction logs [SQL Server]
- stripe sets [SQL Server]
- cross-platform backups
ms.assetid: 89a4658a-62f1-4289-8982-f072229720a1
caps.latest.revision: "275"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1b3cdba9ffe5b8020a0e3d7c64c766cc54d89c71
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="backup-transact-sql"></a>BACKUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Realiza una copia de seguridad completa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos para crear una copia de seguridad de base de datos, o uno o más archivos o grupos de archivos de la base de datos para crear una copia de seguridad de archivos (copia de seguridad de base de datos). Además, con el modelo de recuperación completa o con el modelo de recuperación optimizado para cargas masivas de registros, realiza la copia de seguridad del registro de transacciones de la base de datos para crear una copia de seguridad de registros (BACKUP LOG).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
``` 
Backing Up a Whole Database   
BACKUP DATABASE { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up Specific Files or Filegroups  
BACKUP DATABASE { database_name | @database_name_var }   
 <file_or_filegroup> [ ,...n ]   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Creating a Partial Backup  
BACKUP DATABASE { database_name | @database_name_var }   
 READ_WRITE_FILEGROUPS [ , <read_only_filegroup> [ ,...n ] ]  
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { DIFFERENTIAL | <general_WITH_options> [ ,...n ] } ]  
[;]  
  
Backing Up the Transaction Log (full and bulk-logged recovery models)  
BACKUP LOG { database_name | @database_name_var }   
  TO <backup_device> [ ,...n ]   
  [ <MIRROR TO clause> ] [ next-mirror-to ]  
  [ WITH { <general_WITH_options> | \<log-specific_optionspec> } [ ,...n ] ]  
[;]  
  
<backup_device>::=   
 {  
   { logical_device_name | @logical_device_name_var }   
 | { DISK | TAPE | URL} =   
     { 'physical_device_name' | @physical_device_name_var | NUL }  
 }   
  
<MIRROR TO clause>::=  
 MIRROR TO <backup_device> [ ,...n ]  
  
<file_or_filegroup>::=  
 {  
   FILE = { logical_file_name | @logical_file_name_var }   
 | FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
 }   
  
<read_only_filegroup>::=  
FILEGROUP = { logical_filegroup_name | @logical_filegroup_name_var }  
  
<general_WITH_options> [ ,...n ]::=   
--Backup Set Options  
   COPY_ONLY   
 | { COMPRESSION | NO_COMPRESSION }   
 | DESCRIPTION = { 'text' | @text_variable }   
 | NAME = { backup_set_name | @backup_set_name_var }   
 | CREDENTIAL  
 | ENCRYPTION  
 | FILE_SNAPSHOT  
 | { EXPIREDATE = { 'date' | @date_var }   
        | RETAINDAYS = { days | @days_var } }   
  
--Media Set Options  
   { NOINIT | INIT }   
 | { NOSKIP | SKIP }   
 | { NOFORMAT | FORMAT }   
 | MEDIADESCRIPTION = { 'text' | @text_variable }   
 | MEDIANAME = { media_name | @media_name_variable }   
 | BLOCKSIZE = { blocksize | @blocksize_variable }   
  
--Data Transfer Options  
   BUFFERCOUNT = { buffercount | @buffercount_variable }   
 | MAXTRANSFERSIZE = { maxtransfersize | @maxtransfersize_variable }  
  
--Error Management Options  
   { NO_CHECKSUM | CHECKSUM }  
 | { STOP_ON_ERROR | CONTINUE_AFTER_ERROR }  
  
--Compatibility Options  
   RESTART   
  
--Monitoring Options  
   STATS [ = percentage ]   
  
--Tape Options  
   { REWIND | NOREWIND }   
 | { UNLOAD | NOUNLOAD }   
  
--Log-specific Options  
   { NORECOVERY | STANDBY = undo_file_name }  
 | NO_TRUNCATE  
  
--Encryption Options  
 ENCRYPTION (ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY } , encryptor_options ) <encryptor_options> ::=   
   SERVER CERTIFICATE = Encryptor_Name | SERVER ASYMMETRIC KEY = Encryptor_Name   
```  
  
## <a name="arguments"></a>Argumentos  
 DATABASE  
 Especifica una copia de seguridad completa de la base de datos. Si se especifica una lista de archivos y grupos de archivos, solo se realiza la copia de seguridad de esos archivos o grupos de archivos. Durante una copia de seguridad completa o diferencial de una base de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza la copia de seguridad de una parte suficiente del registro de transacciones para producir una base de datos coherente cuando se restaure la base de datos.  
  
 Al restaurar una copia de seguridad creado por la copia de seguridad de la base de datos (un *copia de seguridad de datos*), se restaura la copia de seguridad completa. Solo una copia de seguridad del registro se puede restaurar hasta un momento o transacción concretos dentro de la copia de seguridad.  
  
> [!NOTE]  
>  Solo una copia de seguridad completa de la base de datos se pueden realizar en el **maestro** base de datos.  
  
 LOG  
 Especifica que solo se realizará la copia de seguridad del registro de transacciones. Se realiza la copia de seguridad del registro desde la última copia de seguridad del registro ejecutada correctamente hasta el final actual del registro. Para poder crear la primera copia de seguridad de registros, debe crear una copia de seguridad completa.  
  
 Puede restaurar una copia de seguridad de registro a un momento o transacción concretos dentro de la copia de seguridad especificando WITH STOPAT, STOPATMARK o STOPBEFOREMARK en su [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md) instrucción.  
  
> [!NOTE]  
>  Después de una copia de seguridad del registro típica, algunas entradas del registro de transacciones se quedan inactivas, a menos que se especifique WITH NO_TRUNCATE o COPY_ONLY. El registro se trunca después de que todos los registros de uno o varios archivos del registro virtual se queden inactivos. Si el registro no se trunca después de las copias de seguridad del registro rutinarias, algo podría estar retrasando el truncamiento de los registros. Para obtener más información, vea:  
  
 { *database_name* | **@**database_name_var *}   
 Es la base de datos para la que se realiza la copia de seguridad del registro de transacciones, de una parte de la base de datos o de la base de datos completa. Si se proporciona como una variable (**@***database_name_var*), este nombre se puede especificar como una constante de cadena ( **@**   *database_name_var***=***nombre de base de datos*) o como una variable de tipo de datos de cadena de caracteres, excepto para la **ntext** o **texto** tipos de datos.  
  
> [!NOTE]  
>  No se puede hacer una copia de seguridad de la base de datos reflejada en una asociación de creación de reflejo de la base de datos.  
  
\<file_or_filegroup > [ **,**... *n* ]  
 Se utiliza solo con BACKUP DATABASE, especifica un grupo de archivos o un archivo de copia de seguridad que se va a incluir en una copia de seguridad de archivos, o especifica un grupo de archivos o un archivo de solo lectura que se va a incluir en una copia de seguridad parcial.  
  
 ARCHIVO  **=**  { *nombre_de_archivo_lógico*| **@***varDeNombreLógicoDeArchivo* }  
 Es el nombre lógico de un archivo o una variable cuyo valor equivale al nombre lógico de un archivo que se va a incluir en la copia de seguridad.  
  
 Grupo de archivos  **=**  { *nombreLógicoDeGrupoDeArchivos*| **@***varDeNombreLógicoDeGrupoDeArchivos* }  
 Es el nombre lógico de un grupo de archivos o una variable cuyo valor equivale al nombre lógico de un grupo de archivos que se va a incluir en la copia de seguridad. En el modelo de recuperación simple, se permite la copia de seguridad de un grupo de archivos solo si se trata de un grupo de archivos de solo lectura.  
  
> [!NOTE]  
>  Considere la posibilidad de utilizar copias de seguridad de archivos cuando el tamaño y los requisitos de rendimiento de la base de datos no permitan realizar una copia de seguridad completa de la base de datos. El dispositivo NUL puede utilizarse para probar el rendimiento de las copias de seguridad, pero no debe usarse en entornos de producción.
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar varios archivos y grupos de archivos en una lista separada por comas. El número es ilimitado. 
  
 Para obtener más información, consulte: [copias de seguridad de archivos completas &#40; SQL Server &#41; ](../../relational-databases/backup-restore/full-file-backups-sql-server.md) y [copia de seguridad de archivos y grupos de archivos &#40; SQL Server &#41; ](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md).  
  
 READ_WRITE_FILEGROUPS [ **,** FILEGROUP = { *nombreLógicoDeGrupoDeArchivos*| **@***varDeNombreLógicoDeGrupoDeArchivos* } [ **,**... *n* ] ]  
 Especifica una copia de seguridad parcial. Una copia de seguridad parcial incluye todos los archivos de lectura/escritura en una base de datos: el grupo de archivos principal y los grupos de archivos secundarios de lectura/escritura, así como los grupos de archivos o archivos de solo lectura especificados.  
  
 READ_WRITE_FILEGROUPS  
 Especifica que en la copia de seguridad parcial se copiarán todos los grupos de archivos de lectura/escritura. Si la base de datos es de solo lectura, READ_WRITE_FILEGROUPS incluye tan solo el grupo de archivos principal.  
  
> [!IMPORTANT]  
>  Si se enumeran de forma explícita los grupos de archivos de lectura/escritura con FILEGROUP en vez de READ_WRITE_FILEGROUPS, se crea una copia de seguridad de archivos.  
  
 FILEGROUP = { *nombreLógicoDeGrupoDeArchivos*| **@***varDeNombreLógicoDeGrupoDeArchivos* }  
Es el nombre lógico de un grupo de archivos de solo lectura o una variable cuyo valor equivale al nombre lógico de un grupo de archivos de solo lectura que se va a incluir en la copia de seguridad parcial. Para obtener más información, vea "\<file_or_filegroup >," anteriormente en este tema.
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar varios grupos de archivos de solo lectura en una lista separada por comas.  
  
 Para obtener más información acerca de copias de seguridad parciales, consulte [copias de seguridad parciales &#40; SQL Server &#41; ](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
PARA \<dispositivodecopiadeseguridad > [ **,**...  *n*  ] Indica que el conjunto de [dispositivos de copia de seguridad](../../relational-databases/backup-restore/backup-devices-sql-server.md) es un conjunto de medios no reflejado o el primero de los reflejos de un conjunto (por qué uno o más MIRROR TO de medios reflejado las cláusulas se declaran).  
  
\<backup_device > especifica un dispositivo de copia de seguridad físico o lógico que se usará para la operación de copia de seguridad.  
  
 { *logical_device_name* | **@***logical_device_name_var* }  
 Es el nombre lógico del dispositivo de copia de seguridad en que se hace la copia de seguridad de la base de datos. El nombre lógico debe seguir las reglas definidas para los identificadores. Si se proporciona como una variable (@*logical_device_name_var*), el nombre del dispositivo de copia de seguridad se pueden especificar como una constante de cadena (@*logical_device_name_var*  **=**  nombre de dispositivo lógico de copia de seguridad) o como una variable de cualquier tipo de datos de cadena de caracteres excepto para la **ntext** o **texto** tipos de datos.  
  
 {DISCO | CINTA | Dirección URL}  **=**  { **'***physical_device_name***'**  |   **@**  *physical_device_name_var* | NUL}  
 Especifica un archivo de disco o un dispositivo de cinta, o un servicio de almacenamiento Blob de Windows Azure. El formato de dirección URL se usa para crear copias de seguridad para el servicio de almacenamiento de Windows Azure. Para obtener más información y ejemplos, vea [SQL Server Backup and Restore con el servicio de almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Para obtener un tutorial, vea [Tutorial: SQL Server Backup and Restore a Windows Azure Blob Storage Service](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md). 

[!NOTE] 
 El dispositivo de disco NUL descartará toda la información que se le envíen y solo debe usarse para realizar pruebas. Esto no es para su uso en producción.
  
> [!IMPORTANT]  
>  Con [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 hasta [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], solo una copia de seguridad en un único dispositivo cuando copias de seguridad en dirección URL. Para varios dispositivos de copia de seguridad cuando copias de seguridad en dirección URL, debe utilizar [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y deben utilizar tokens de firma de acceso compartido (SAS). Para obtener ejemplos de creación de una firma de acceso compartido, consulte [copias de seguridad de SQL Server a URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md) y [simplificar la creación de credenciales de SQL con tokens de firma de acceso compartido (SAS) en el almacenamiento de Azure con Powershell](http://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx).  
  
**Dirección URL que se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 No es necesario que exista un dispositivo de disco antes de que se especifique en una instrucción BACKUP. Si el dispositivo físico existe y no se especifica la opción INIT en la instrucción BACKUP, la copia de seguridad se anexa al dispositivo.  
 
 El dispositivo NUL descartará todas las entradas que se envíen a este archivo, sin embargo, la copia de seguridad todavía marcará todas las páginas como copia de seguridad.
  
 Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
> [!NOTE]  
>  La opción TAPE se quitará en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan.  
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar hasta 64 dispositivos de copia de seguridad en una lista separada por comas.  
  
MIRROR TO \<dispositivodecopiadeseguridad > [ **,**...  *n*  ] Especifica un conjunto de hasta tres dispositivos de copia de seguridad secundarios, cada uno de los reflejos los dispositivos de las copias de seguridad especificados en la cláusula TO. La cláusula MIRROR TO debe especificar el mismo tipo y número de los dispositivos de copia de seguridad como la cláusula TO. El número máximo de cláusulas MIRROR TO es tres.  
  
 Esta opción solo está disponible en la edición Enterprise de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Para MIRROR TO = DISK, BACKUP determina automáticamente el tamaño de bloque apropiado de los dispositivos de disco. Para obtener más información acerca del tamaño de bloque, vea "BLOCKSIZE" más adelante en esta tabla.  
  
\<backup_device > vea "\<backup_device >," anteriormente en esta sección.
  
 *n*  
 Es un marcador de posición que indica que se pueden especificar hasta 64 dispositivos de copia de seguridad en una lista separada por comas. El número de dispositivos de la cláusula MIRROR TO debe ser igual al número de dispositivos de la cláusula TO.  
  
 Para obtener más información, vea "Familias de medios en conjuntos de medios reflejados" en la sección "Comentarios", posteriormente en este tema.  
  
 [ *siguiente mirror to* ]  
 Es un marcador de posición que indica que una sola instrucción BACKUP puede contener hasta tres cláusulas MIRROR TO, además de una sola cláusula TO.  
  
### <a name="with-options"></a>Opciones de WITH  
 Especifica las opciones que se van a utilizar con una operación de copia de seguridad.  
  
 CREDENTIAL  
 Solo se usa al crear una copia de seguridad en el servicio de almacenamiento Blob de Windows Azure.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 CU2 hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 FILE_SNAPSHOT  
 Se utiliza para crear una instantánea de los archivos de base de datos de Azure cuando todos los archivos de base de datos de SQL Server se almacenan con el servicio de almacenamiento de blobs de Azure. Para obtener más información, consulte [archivos de datos de SQL Server en Microsoft Azure](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Copia de seguridad de instantánea tiene instantáneas de Azure de los archivos de base de datos (archivos de datos y de registro) en un estado coherente. Un conjunto coherente de las instantáneas de Azure forman una copia de seguridad y se registran en el archivo de copia de seguridad. La única diferencia entre **copia de seguridad de base de datos a direcciones URL con FILE_SNAPSHOT** y **copia de seguridad de registro a dirección URL con FILE_SNAPSHOT** es que este último también trunca el registro de transacciones mientras que el primero no. Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instantánea de copia de seguridad, después de la copia de seguridad completa inicial que requiere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para establecer la cadena de copia de seguridad, solo una copia de seguridad de registro de transacciones solo se requiere para restaurar una base de datos hasta el momento en el tiempo de la copia de seguridad del registro de transacciones. Además, solo dos copias de seguridad de registro de transacciones son necesarias para restaurar una base de datos a un punto en el tiempo entre el momento de las copias de seguridad del registro de transacciones de dos.  
  
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
 DIFFERENTIAL  
 Se utiliza solo con BACKUP DATABASE. Especifica que la copia de seguridad de la base de datos o el archivo solo debe estar compuesta por las partes de la base de datos o el archivo que hayan cambiado desde la última copia de seguridad completa. Una copia de seguridad diferencial suele ocupar menos espacio que una copia de seguridad completa. Utilice esta opción para que no tenga que aplicar todas las copias de seguridad del registro individuales efectuadas desde que se realizó la última copia de seguridad completa.  
  
> [!NOTE]  
>  De forma predeterminada, BACKUP DATABASE crea una copia de seguridad completa.  
  
 Para obtener más información, vea [Copias de seguridad diferenciales &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  
  
 ENCRYPTION  
 Se utiliza para especificar el cifrado para una copia de seguridad. Puede especificar un algoritmo de cifrado para cifrar la copia de seguridad o especificar “NO_ENCRYPTION” para no hacer que la copia de seguridad se cifre. El cifrado es una práctica recomendada para ayudar a proteger los archivos de copia de seguridad. La lista de algoritmos que puede especificar son:  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 Si elige cifrar, tendrá que especificar el sistema cifrado mediante las opciones de cifrado:  
  
-   SERVER CERTIFICATE = Encryptor_Name  
  
-   SERVER ASYMMETRIC KEY = Encryptor_Name  
  
    > [!WARNING]  
    >  Cuando se utiliza el cifrado junto con el argumento FILE_SNAPSHOT, el propio archivo de metadatos se cifra mediante el algoritmo de cifrado especificado y el sistema comprueba que TDE se ha completado para la base de datos. Se produce sin cifrado adicional para los datos en Sí. Se produce un error en la copia de seguridad si no se cifró la base de datos o si el cifrado no se completó antes de emitir la instrucción de copia de seguridad.  
  
**Opciones de copia de seguridad**  
  
Estas opciones funcionan en el conjunto de copia de seguridad que se crea con esta operación de copia de seguridad.  
  
> [!NOTE]  
>  Para especificar una copia de seguridad para una operación de restauración, utilice el archivo  **=**   *\<backup_set_file_number >* opción. Para obtener más información sobre cómo especificar un conjunto de copia de seguridad, vea "Especificar de un conjunto copia de seguridad" en [argumentos RESTORE &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-arguments-transact-sql.md).
  
 COPY_ONLY  
 Especifica que la copia de seguridad es un *copia de seguridad solo*, que no afecta a la secuencia normal de las copias de seguridad. Se crea una copia de seguridad de solo copia independientemente de las copias de seguridad convencionales programadas regularmente. Una copia de seguridad de solo copia no afecta a los procedimientos de copias de seguridad y restauración generales de la base de datos.  
  
 Las copias de seguridad de solo copia deben utilizarse en situaciones en las que se realiza una copia de seguridad con un fin específico, por ejemplo al hacer la copia de seguridad del registro antes de una restauración de archivos en línea. Normalmente, una copia de seguridad de solo copia se usa una vez y se elimina.  
  
-   Cuando se usa con BACKUP DATABASE, la opción COPY_ONLY crea una copia de seguridad completa que no se puede utilizar como una base diferencial. El mapa de bits diferencial no se actualiza y las copias de seguridad diferenciales se comportan como si no existiera la copia de seguridad de solo copia. Las copias de seguridad diferenciales posteriores usarán la copia de seguridad completa convencional más reciente como base.  
  
    > [!IMPORTANT]  
    >  Si DIFFERENTIAL y COPY_ONLY se usan juntas, COPY_ONLY se omite y se crea una copia de seguridad diferencial.  
  
-   Cuando se usa con BACKUP LOG, la opción COPY_ONLY crea una *copia de seguridad de registros de solo copia*, que no trunca el registro de transacciones. La copia de seguridad del registro de solo copia no afecta a la cadena de registros y otras copias de seguridad del registro se comportan como si no existiera la copia de seguridad de solo copia.  
  
Para obtener más información, vea [Copias de seguridad de solo copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
{ COMPRESSION | NO_COMPRESSION }  
En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] y versiones posteriores únicamente, especifica si [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md) se lleva a cabo en esta copia de seguridad, invalida la configuración predeterminada de nivel de servidor.  
  
Durante la instalación, el comportamiento predeterminado es que no se realice la compresión de copia de seguridad. Pero se puede cambiar este comportamiento predeterminado estableciendo la [copia de seguridad predeterminada de compresión](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md) opción de configuración del servidor. Para obtener información acerca de cómo ver el valor actual de esta opción, vea [ver o cambiar propiedades del servidor &#40; SQL Server &#41; ](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md).  
  
COMPRESSION  
Habilita de forma explícita la compresión de copia de seguridad.  
  
NO_COMPRESSION  
Deshabilita de forma explícita la compresión de copia de seguridad.  
  
DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
Especifica el texto de forma libre que describe el conjunto de copia de seguridad. La cadena puede tener un máximo de 255 caracteres.  
  
NOMBRE  **=**  { *nombreDeConjuntoDeCopia*| **@***backup_set_var* }  
Especifica el nombre del conjunto de copia de seguridad. Los nombres pueden tener un máximo de 128 caracteres. Si no se especifica NAME, está en blanco.  
  
{EXPIREDATE **='***fecha***'**| RETAINDAYS  **=**  *días* }  
Especifica cuándo se puede sobrescribir el conjunto de copia de seguridad para esta copia de seguridad. Si se usan las dos opciones, RETAINDAYS tiene precedencia sobre EXPIREDATE.  
  
Si se especifica ninguna opción, la fecha de expiración está determinada por la **mediaretention** de configuración. Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
> [!IMPORTANT]  
>  Estas opciones solo impiden que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobrescriba un archivo. Las cintas se pueden borrar utilizando otros métodos, y los archivos de disco se pueden eliminar usando el sistema operativo. Para obtener más información acerca de la comprobación de la expiración, vea SKIP y FORMAT en este tema.  
  
EXPIREDATE  **=**  { **'***fecha***'** |   **@**  *date_var* }  
 Especifica cuándo expira el conjunto de copia de seguridad y se puede sobrescribir. Si se proporciona como una variable (@*date_var*), esta fecha debe seguir el sistema configurado **datetime** dar formato y se pueden especificar uno de los siguientes:  
  
-   Una constante de cadena (@*date_var*  **=**  fecha)  
-   Una variable de tipo de datos de cadena de caracteres (excepto el **ntext** o **texto** tipos de datos)  
-   Un **smalldatetime**  
-   A **datetime** variable  
  
Por ejemplo:  
  
-   `'Dec 31, 2020 11:59 PM'`  
-   `'1/1/2021'`  
  
Para obtener información sobre cómo especificar **datetime** valores, consulte [tipos de fecha y hora](../../t-sql/data-types/date-and-time-types.md).  
  
> [!NOTE]  
>  Para omitir la fecha de caducidad, use la opción SKIP.  
  
RETAINDAYS  **=**  { *días*| **@***days_var* }  
 Especifica el número de días que deben transcurrir antes de que se pueda sobrescribir este conjunto de medios de copia de seguridad. Si se proporciona como una variable (**@***days_var*), debe especificarse como un entero.  
  
**Opciones del conjunto de medios**  
  
Estas opciones funcionan para todo el conjunto de medios.  
  
{ **NOINIT** | INIT}  
 Controla si la operación de copia de seguridad anexa o sobrescribe los conjuntos de copias de seguridad existentes en el medio. El valor predeterminado es anexar al conjunto de copias de seguridad más reciente en el medio (NOINIT).  
  
> [!NOTE]  
>  Para obtener información acerca de las interacciones entre { **NOINIT** | INIT} y { **NOSKIP** | SKIP}, vea "Comentarios", más adelante en este tema.  
  
NOINIT  
 Indica que el conjunto de copia de seguridad se anexa al conjunto de medios especificado, conservando así los conjuntos de copia de seguridad existentes. Si se ha definido una contraseña para el conjunto de medios, debe proporcionarla. NOINIT es el valor predeterminado.  
  
Para obtener más información, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
INIT  
 Especifica que se deben sobrescribir todos los conjuntos de copia de seguridad, pero conserva el encabezado de medios. Si se especifica INIT, se sobrescriben todos los conjuntos de copia de seguridad existentes en el dispositivo, si las condiciones lo permiten. De forma predeterminada, BACKUP comprueba las siguientes condiciones y no sobrescribe los medios de copia de seguridad en caso de existir alguna de las condiciones siguientes:  
  
-   Aún no ha expirado ningún conjunto de copia de seguridad. Para obtener más información, vea las opciones EXPIREDATE y RETAINDAYS.  
-   El nombre del conjunto de copia de seguridad proporcionado en la instrucción BACKUP, si se especificó, no coincide con el nombre de los medios de copia de seguridad. Para obtener más información, vea la opción NAME, descrita anteriormente de esta sección.  
  
Para invalidar estas comprobaciones, utilice la opción SKIP.  
  
Para obtener más información, vea [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
{ **NOSKIP** | SKIP}  
Controla si una operación de copia de seguridad comprueba la fecha y la hora de expiración de los conjuntos de copia de seguridad en el medio antes de sobrescribirlos.  
  
> [!NOTE]  
>  Para obtener información acerca de las interacciones entre { **NOINIT** | INIT} y { **NOSKIP** | SKIP}, vea "Comentarios", más adelante en este tema.  
  
NOSKIP  
Indica a la instrucción BACKUP que compruebe la fecha de expiración de todos los conjuntos de copia de seguridad de los medios antes de permitir que se sobrescriban. Éste es el comportamiento predeterminado.  
  
SKIP  
Deshabilita la comprobación de la expiración y el nombre del conjunto de copia de seguridad que suele realizar la instrucción BACKUP para impedir que se sobrescriban los conjuntos de copia de seguridad. Para obtener más información acerca de las interacciones entre { INIT | NOINIT } y { NOSKIP | SKIP }, vea "Comentarios", más adelante en este tema.  
Para ver las fechas de caducidad de los conjuntos de copia de seguridad, consulte el **expiration_date** columna de la [backupset](../../relational-databases/system-tables/backupset-transact-sql.md) tabla de historial.  
  
{ **NOFORMAT** | FORMATO}  
Especifica si debe escribirse el encabezado de medios en los volúmenes usados en esta operación de copia de seguridad, con lo que se sobrescribirán los conjuntos de copias de seguridad y el encabezado de medios existentes.  
  
NOFORMAT  
Especifica que la operación de copia de seguridad conservará los conjuntos de copias de seguridad y el encabezado de medios existentes en los volúmenes de medios usados en esta operación de copia de seguridad. Éste es el comportamiento predeterminado.  
  
FORMAT  
Especifica que se debe crear un conjunto de medios nuevo. FORMAT hace que la operación de copia de seguridad escriba un nuevo encabezado de medios en todos los volúmenes de medios usados en la operación de copia de seguridad. El contenido existente del volumen no será válido porque se sobrescribirán los conjuntos de copias de seguridad y el encabezado de medios existentes.  
  
> [!IMPORTANT]  
>  Utilice FORMAT con precaución. Al dar formato a cualquier volumen de un conjunto de medios, todo el conjunto de medios se convierte en inutilizable. Por ejemplo, si inicializa una cinta que pertenece a un conjunto de medios distribuido, queda inutilizable todo el conjunto de medios.  
  
La especificación de FORMAT implica SKIP y no es necesario especificar SKIP de forma explícita.  
  
MEDIADESCRIPTION  **=**  { *texto* | **@***text_variable* }  
Especifica la descripción de texto de forma libre, con un máximo de 255 caracteres, del conjunto de medios.  
  
MEDIANAME  **=**  { *nombreDeMedio* | **@***media_name_variable* }  
Especifica el nombre del medio para el conjunto completo de medios de copia de seguridad. El nombre del medio no puede tener más de 128 caracteres y, si se especifica MEDIANAME, debe coincidir con el nombre de medio especificado que ya existe en los volúmenes de copia de seguridad. Si no se especifica o se especifica la opción SKIP, no se realiza la comprobación del nombre del medio.  
  
BLOCKSIZE  **=**  { *blocksize* | **@***blocksize_variable* }  
Especifica el tamaño de bloque físico, en bytes. Los tamaños admitidos son 512, 1024, 2048, 4096, 8192, 16384, 32768 y 65536 (64 KB) bytes. El valor predeterminado es 65536 para dispositivos de cinta y 512 para otros dispositivos. Normalmente, esta opción no es necesaria, ya que BACKUP selecciona automáticamente un tamaño de bloque apropiado para el dispositivo. La especificación explícita de un tamaño de bloque invalida la selección automática del tamaño de bloque.  
  
Si va a realizar una copia de seguridad en CD-ROM que pretende utilizar para copiar y restaurar, especifique BLOCKSIZE=2048.  
  
> [!NOTE]  
>  Normalmente, esta opción solo afecta al rendimiento al escribir en dispositivos de cinta.  
  
**Opciones de transferencia de datos**  
  
BUFFERCOUNT  **=**  { *buffercount* | **@***buffercount_variable* }  
Especifica el número total de búferes de E/S que se van a utilizar para la operación de copia de seguridad. Puede especificar cualquier entero positivo; no obstante, un número de búferes demasiado grande podría provocar errores de "memoria insuficiente" a causa de un espacio de direcciones virtuales inadecuado en el proceso Sqlservr.exe.  
  
El espacio total utilizado por los búferes está determinado por: *buffercount***\****maxtransfersize*.  
  
> [!NOTE]  
>  Para obtener información importante sobre el uso de la opción BUFFERCOUNT, vea el [opción de transferencia de datos BufferCount incorrecta puede dar lugar a una condición OOM](http://blogs.msdn.com/b/sqlserverfaq/archive/2010/05/06/incorrect-buffercount-data-transfer-option-can-lead-to-oom-condition.aspx) blog.  
  
MAXTRANSFERSIZE  **=**  { *maxtransfersize* | **@***maxtransfersize_variable* }  
 Especifica la unidad de transferencia mayor (en bytes) que se debe usar entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el medio de copia de seguridad. Los valores posibles son múltiplos de 65536 bytes (64 KB), hasta un máximo de 4194304 bytes (4 MB).  
> [!NOTE]  
>  Al crear copias de seguridad mediante el servicio SQL Writer, si la base de datos configurada FILESTREAM o incluye grupos de archivos de OLTP en memoria, la `MAXTRANSFERSIZE` en el momento de restauración debe ser mayor o igual que el `MAXTRANSFERSIZE` que estaba se usa cuando el se creó la copia de seguridad. 
  
**Opciones de administración de errores**  
  
Estas opciones permiten determinar si se habilitan las sumas de comprobación de copia de seguridad para la operación de copia de seguridad y si la operación se detiene al encontrar un error.  
  
{ **NO_CHECKSUM** | SUMA DE COMPROBACIÓN}  
 Controla si las sumas de comprobación de copia de seguridad están habilitadas.  
  
NO_CHECKSUM  
Deshabilita de forma explícita la generación de sumas de comprobación de copia de seguridad (y la validación de sumas de comprobación de página). Éste es el comportamiento predeterminado.  
  
CHECKSUM  
Especifica que la operación de copia de seguridad comprueba cada página si la suma de comprobación y página rasgada, si está habilitada y disponible y generar una suma de comprobación para la copia de seguridad completa.  
  
El uso de sumas de comprobación de copia de seguridad puede afectar a la carga de trabajo y al rendimiento de la copia de seguridad.  
  
Para obtener más información, vea [posibles medios errores durante la copia de seguridad y restauración &#40; SQL Server &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
{ **STOP_ON_ERROR** | CONTINUE_AFTER_ERROR}  
Controla si una operación de copia de seguridad se detiene o continúa después de encontrar un error en la suma de comprobación de página.  
  
STOP_ON_ERROR  
Indica a BACKUP que dé error si no se comprueba una suma de comprobación de página. Éste es el comportamiento predeterminado.  
  
CONTINUE_AFTER_ERROR  
Indica a BACKUP que continúe a pesar de la detección de errores como sumas de comprobación no válidas o páginas rasgadas.  
  
Si no puede hacer copia de seguridad del final del registro con la opción NO_TRUNCATE opción cuando la base de datos está dañada, puede intentar una [copia del final del registro del registro](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) especificando CONTINUE_AFTER_ERROR en vez de NO_TRUNCATE.  
  
Para obtener más información, vea [posibles medios errores durante la copia de seguridad y restauración &#40; SQL Server &#41; ](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
**Opciones de compatibilidad**  
  
RESTART  
A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], no tiene ningún efecto. La versión acepta esta opción por compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Opciones de supervisión**  
  
ESTADÍSTICAS [  **=**  *porcentaje* ]  
 Muestra un mensaje cada vez que otro *porcentaje* completa y se usa para medir el progreso. Si *porcentaje* se omite, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra un mensaje después de completar cada 10 por ciento.  
  
La opción STATS informa del porcentaje completado desde el umbral para informar del próximo intervalo. Éste es aproximadamente el porcentaje especificado; por ejemplo, con STATS=10, si la cantidad completada equivale al 40 por ciento, la opción puede mostrar el 43 por ciento. En el caso de los conjuntos de copia de seguridad de gran tamaño, esto no representa ningún problema porque el porcentaje completado se mueve muy lentamente entre las llamadas de E/S.  
  
**Opciones de cinta**  
  
Estas opciones solo se utilizan para dispositivos de cinta. Se omitirán si se utiliza otro tipo de dispositivo.  
  
{ **REWIND** | NOREWIND }  
REWIND  
 Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si libera y rebobina la cinta. REWIND es la opción predeterminada.  
  
NOREWIND  
Especifica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantendrá la cinta abierta tras la operación de copia de seguridad. Puede utilizar esta opción como ayuda para mejorar el rendimiento al realizar varias operaciones de copia de seguridad en una cinta.  
  
NOREWIND implica NOUNLOAD, y estas opciones son incompatibles en una sola instrucción BACKUP.  
  
> [!NOTE]  
>  Si utiliza NOREWIND, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conserva la propiedad de la unidad de cinta hasta que una instrucción BACKUP o RESTORE que se ejecuta en el mismo proceso utiliza la opción REWIND o UNLOAD, o bien se cierra la instancia del servidor. Mantener abierta la cinta evita que otros procesos obtengan acceso a la misma. Para obtener información acerca de cómo mostrar una lista de cintas abiertas y cómo cerrar una cinta abierta, vea [dispositivos de copia de seguridad &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-devices-sql-server.md).  
  
{ **UNLOAD** | NOUNLOAD}  
> [!NOTE]  
>  UNLOAD/NOUNLOAD es una configuración de sesión que persiste mientras dure la sesión o hasta que se restablezca especificando la alternativa.  
  
UNLOAD  
 Especifica que la cinta se rebobina y descarga automáticamente al terminar la copia de seguridad. UNLOAD es el valor predeterminado cuando se inicia una sesión. 
  
NOUNLOAD  
 Especifica que tras la operación de copia de seguridad de la cinta permanecerá cargada en la unidad de cinta.  
  
> [!NOTE]  
>  Para una copia de seguridad de un dispositivo de cinta, la opción BLOCKSIZE afecta al rendimiento de la operación de copia de seguridad. Normalmente, esta opción solo afecta al rendimiento al escribir en dispositivos de cinta.  
  
**Opciones específicas del registro**  
  
Estas opciones solo se usan con BACKUP LOG.  
  
> [!NOTE]  
>  Si no desea hacer copias de seguridad del registro, use el modelo de recuperación simple. Para obtener más información, vea [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md).  
  
{NORECOVERY | STANDBY  **=**  *nombreArchivoParaDeshacer* }  
  NORECOVERY  
  Realiza una copia de seguridad del registro después del error y deja la base de datos en el estado RESTORING. NORECOVERY resulta útil cuando, en caso de error, se conmuta a una base de datos secundaria y al guardar los registros después del error antes de una operación RESTORE.  
  
  Para hacer una copia de seguridad del registro óptima que omita el truncamiento de los registros y, a continuación, establecer la base de datos en el estado RESTORING de forma atómica, utilice las opciones NO_TRUNCATE y NORECOVERY conjuntamente.  
  
  STANDBY  **=**  *standby_file_name*  
  Realiza una copia de seguridad del final del registro y deja la base de datos en modo de solo lectura y en el estado STANDBY. La cláusula STANDBY escribe datos en espera (realiza la reversión, pero con la posibilidad de recuperaciones posteriores). El uso de la opción STANDBY es equivalente a BACKUP LOG WITH NORECOVERY seguido de RESTORE WITH STANDBY.  
  
  Uso de modo de espera requiere un archivo en espera, especificado por *standby_file_name*, cuya ubicación se almacena en el registro de la base de datos. Si el archivo especificado ya existe, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] lo sobrescribe; si no existe, [!INCLUDE[ssDE](../../includes/ssde-md.md)] lo crea. El archivo en espera pasa a formar parte de la base de datos.  
  
  Este archivo contiene los cambios revertidos, que se deben invertir si las operaciones RESTORE LOG se van a aplicar posteriormente. Debe haber suficiente espacio en disco para permitir el crecimiento del archivo en espera de manera que pueda contener todas las páginas distintas de la base de datos que se modificaron al revertir las transacciones sin confirmar.  
  
NO_TRUNCATE  
Especifica que el no es truncado el registro y provoca la [!INCLUDE[ssDE](../../includes/ssde-md.md)] a intentar la copia de seguridad con independencia del estado de la base de datos. Por consiguiente, una copia de seguridad realizada con NO_TRUNCATE puede tener metadatos incompletos. Esta opción permite realizar copias de seguridad del registro cuando la base de datos está dañada.  
  
La opción NO_TRUNCATE de BACKUP LOG es equivalente a la especificación de COPY_ONLY y CONTINUE_AFTER_ERROR.  
  
Sin la opción NO_TRUNCATE, la base de datos debe estar en el estado ONLINE. Si la base de datos está en el estado SUSPENDED, podría poder crear una copia de seguridad especificando NO_TRUNCATE. Pero si la base de datos se encuentra en el estado OFFLINE o EMERGENCY, no se admite BACKUP, ni siquiera con NO_TRUNCATE. Para obtener información acerca de los Estados de base de datos, vea [Estados de base de datos](../../relational-databases/databases/database-states.md).  
  
## <a name="about-working-with-sql-server-backups"></a>Cómo trabajar con copias de seguridad de SQL Server  
 En esta sección se presentan los siguiente conceptos esenciales de la copia de seguridad:  
  
 [Tipos de copia de seguridad](#Backup_Types)  
 [Truncamiento del registro de transacciones](#Tlog_Truncation)  
 [Aplicar formato a los medios de copia de seguridad](#Formatting_Media)  
 [Trabajar con dispositivos de copia de seguridad y conjuntos de medios](#Backup_Devices_and_Media_Sets)  
 [Restaurar copias de seguridad SQL Server](#Restoring_Backups)  
  
> [!NOTE]  
>  Para obtener una introducción a la copia de seguridad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [información general de copia de seguridad &#40; SQL Server &#41; ](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Backup_Types"></a>Tipos de copia de seguridad  
 Los tipos de copia de seguridad admitidos dependen del modelo de recuperación de la base de datos y son los siguientes:  
  
-   Todos los modelos de recuperación admiten copias de seguridad de datos completas y diferenciales.  
  
    |Ámbito de la copia de seguridad|Tipos de copia de seguridad|  
    |---------------------|------------------|  
    |Base de datos completa|[Las copias de seguridad de base de datos](../../relational-databases/backup-restore/full-database-backups-sql-server.md) abarcan toda la base de datos.<br /><br /> Opcionalmente, cada copia de seguridad de base de datos puede servir como base de una serie de uno o varios [copias de seguridad de base de datos diferencial](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Base de datos parcial|[Copias de seguridad parciales](../../relational-databases/backup-restore/partial-backups-sql-server.md) portada de lectura o escritura los grupos de archivos y, posiblemente, uno o más archivos de solo lectura o grupos de archivos.<br /><br /> Opcionalmente, cada copia de seguridad parcial puede servir como base de una serie de uno o varios [copias de seguridad diferenciales parciales](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
    |Archivo o grupo de archivos|[Las copias de seguridad de archivos](../../relational-databases/backup-restore/full-file-backups-sql-server.md) cubrir uno o más archivos o grupos de archivos y solo son relevantes para las bases de datos que contienen varios grupos de archivos. En el modelo de recuperación simple, las copias de seguridad de archivos se limitan básicamente a los archivos secundarios de solo lectura.<br /> Opcionalmente, cada copia de seguridad de archivos puede servir como base de una serie de uno o varios [copias de seguridad diferenciales de archivos](../../relational-databases/backup-restore/differential-backups-sql-server.md).|  
  
-   En el modelo de recuperación completa o el modelo de recuperación optimizado para cargas masivas, copias de seguridad convencionales también incluyen secuencial *copias de seguridad de registro de transacciones* (o *copias de seguridad de registro*), que son necesarios. Cada copia de seguridad del registro cubre la parte del registro de transacciones que estaba activa al crear la copia de seguridad e incluye todos los registros que no se copiaron en una copia de seguridad del registro anterior.  
  
     Para reducir lo máximo posible el riesgo de perder trabajo, lo que supondría una sobrecarga de trabajo administrativo, debería programar copias de seguridad del registro frecuentes. La programación de copias de seguridad diferenciales entre copias de seguridad completas puede reducir el tiempo de restauración al disminuir el número de copias de seguridad del registro que se deben restaurar después de restaurar los datos.  
  
     Recomendamos que coloque las copias de seguridad del registro en un volumen que no sea el de las copias de seguridad de la base de datos.  
  
    > [!NOTE]  
    >  Para poder crear la primera copia de seguridad de registros, debe crear una copia de seguridad completa.  
  
-   A *copia de seguridad solo* es una copia de seguridad completa de propósito especial o una copia de seguridad del registro que es independiente de la secuencia normal de copias de seguridad convencionales. Para crear una copia de seguridad de solo copia, especifique la opción COPY_ONLY en la instrucción BACKUP. Para obtener más información, vea [Copias de seguridad de solo copia &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
###  <a name="Tlog_Truncation"></a>Truncamiento del registro de transacciones  
 Para evitar llenar el registro de transacciones de una base de datos, las copias de seguridad rutinarias son esenciales. Normalmente, el truncamiento se produce automáticamente bajo el modelo de recuperación simple cuando se realiza una copia de seguridad de la base de datos y bajo el modelo de recuperación completa cuando se realiza una copia de seguridad del registro de transacciones. Sin embargo, en ocasiones se puede retrasar el proceso de truncamiento. Para obtener información sobre los factores que pueden retrasar el truncamiento del registro, vea [Registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
> [!NOTE]  
>  Las opciones BACKUP LOG WITH NO_LOG y WITH TRUNCATE_ONLY ya no se incluyen. Si usa el modelo de recuperación completa o el optimizado para cargas masivas de registros y debe quitar la cadena de copia de seguridad de registros de una base de datos, cambie al modelo de recuperación simple. Para obtener más información, vea [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
###  <a name="Formatting_Media"></a>Aplicar formato a los medios de copia de seguridad  
 Con una instrucción BACKUP se dan formato a los medios de copia de seguridad si y solo si se cumple alguna de las siguientes condiciones:  
  
-   Se especifica la opción FORMAT.  
-   El medio está vacío.  
-   En la operación se está escribiendo una cinta de continuación.  
  
###  <a name="Backup_Devices_and_Media_Sets"></a>Trabajar con dispositivos de copia de seguridad y conjuntos de medios  
  
#### <a name="backup-devices-in-a-striped-media-set-a-stripe-set"></a>Dispositivos de copia de seguridad en un conjunto de medios seccionado (conjunto seccionado)  
 A *un conjunto de bandas* es un conjunto de archivos de disco en el que los datos se dividen en bloques y distribuidas en un orden fijo. El número de dispositivos de copia de seguridad utilizados en un conjunto de franjas debe ser siempre el mismo (a menos que el medio se reinicialice con FORMAT).  
  
 En el siguiente ejemplo se escribe una copia de seguridad de la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] en un nuevo conjunto de medios distribuido que utiliza tres archivos de disco.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3.bak'  
WITH FORMAT,  
   MEDIANAME = 'AdventureWorksStripedSet0',  
   MEDIADESCRIPTION = 'Striped media set for AdventureWorks2012 database;  
GO  
```  
  
 Después de definir un dispositivo de copia de seguridad como parte de un conjunto de franjas, no se puede utilizar para realizar copias de seguridad en un único dispositivo a menos que se especifique FORMAT. De forma similar, un dispositivo de copia de seguridad que contenga copias de seguridad sin franjas no se puede utilizar en un conjunto de franjas a menos que se especifique FORMAT. Para dividir un conjunto de copia de seguridad distribuido, utilice FORMAT.  
  
 Si se especifica ni MEDIANAME o MEDIADESCRIPTION al escribe un encabezado de medios, el campo de encabezado de medios correspondiente al elemento en blanco está vacío.  
  
#### <a name="working-with-a-mirrored-media-set"></a>Trabajar con un conjunto de medios reflejado  
 Normalmente, las copias de seguridad no se reflejan, y las instrucciones BACKUP simplemente incluyen una cláusula TO. No obstante, puede haber hasta cuatro reflejos en total por cada conjunto de medios. En un conjunto de medios reflejado, la operación copia de seguridad escribe en varios grupos de dispositivos de copia de seguridad. Cada grupo de dispositivos de copia de seguridad contiene un único reflejo en el conjunto de medios reflejado. Cada reflejo debe usar la misma cantidad y tipo de dispositivos de copia de seguridad físicos, y todos deben tener las mismas propiedades.  
  
 Para hacer una copia de seguridad de un conjunto de medios reflejado, deben estar presentes todos los reflejos. Para realizar una copia de seguridad en un conjunto de medios reflejado, especifique la cláusula TO para indicar el primer reflejo y la cláusula MIRROR TO para cada reflejo adicional.  
  
 En el caso de un conjunto de medios reflejado, cada cláusula MIRROR TO debe incluir el mismo número y tipo de dispositivos que la cláusula TO. En el siguiente ejemplo se escribe en un conjunto de medios reflejado que contiene dos reflejos y usa tres dispositivos por reflejo:  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO DISK='X:\SQLServerBackups\AdventureWorks1a.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2a.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3a.bak'  
MIRROR TO DISK='X:\SQLServerBackups\AdventureWorks1b.bak',   
DISK='Y:\SQLServerBackups\AdventureWorks2b.bak',   
DISK='Z:\SQLServerBackups\AdventureWorks3b.bak';  
GO  
```  
  
> [!IMPORTANT]  
>  Este ejemplo se ha creado de modo que pueda probarlo en su sistema local. En la práctica, realizar una copia de seguridad en varios dispositivos de la misma unidad afectaría el rendimiento y eliminaría la redundancia para la que se diseñaron los conjuntos de medios reflejados.  
  
##### <a name="media-families-in-mirrored-media-sets"></a>Familias de medios en conjuntos de medios reflejados  
 Cada dispositivo de copia de seguridad especificado en la cláusula TO de una instrucción BACKUP corresponde a una familia de medios. Por ejemplo, si la cláusula TO incluye tres dispositivos, BACKUP escribe los datos en tres familias de medios. En un conjunto de medios reflejado, cada reflejo debe contener una copia de cada familia de medios. Esto se debe a que el número de dispositivos debe ser idéntico en cada reflejo.  
  
 Si se incluyen varios dispositivos para cada reflejo, el orden determina qué familia de medios se escribe en cada dispositivo. Por ejemplo, en cada lista de dispositivos, el segundo dispositivo corresponde a la segunda familia de medios. En la tabla siguiente se muestra la correspondencia entre los dispositivos y las familias de medios para los dispositivos del ejemplo anterior.  
  
|Reflejo|Familia de medios 1|Familia de medios 2|Familia de medios 3|  
|------------|--------------------|--------------------|--------------------|  
|0|`Z:\AdventureWorks1a.bak`|`Z:\AdventureWorks2a.bak`|`Z:\AdventureWorks3a.bak`|  
|1|`Z:\AdventureWorks1b.bak`|`Z:\AdventureWorks2b.bak`|`Z:\AdventureWorks3b.bak`|  
  
 Siempre debe realizarse la copia de seguridad de una familia de medios en el mismo dispositivo dentro de un reflejo específico. Por tanto, cada vez que use un conjunto de medios existente, enumere los dispositivos de cada reflejo en el mismo orden que se especificaron al crear el conjunto de medios.  
  
 Para obtener más información sobre los conjuntos de medios reflejados, vea [Conjuntos de medios de copia de seguridad reflejados &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md). Para obtener más información sobre los conjuntos de medios y familias de medios en general, vea [conjuntos de medios, familias de medios y conjuntos de copia de seguridad &#40; SQL Server &#41; ](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
###  <a name="Restoring_Backups"></a>Restaurar copias de seguridad SQL Server  
 Para restaurar una base de datos y, opcionalmente, recuperarla para ponerla en línea, o para restaurar un archivo o grupo de archivos, use la [!INCLUDE[tsql](../../includes/tsql-md.md)] [restaurar](../../t-sql/statements/restore-statements-transact-sql.md) instrucción o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **restaurar** tareas. Para obtener más información consulte [restauración y recuperación de información general sobre &#40; SQL Server &#41; ](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md).  
  
##  <a name="Additional_Considerations"></a>Consideraciones adicionales sobre las opciones de copia de seguridad  
  
###  <a name="Interactions_SKIP_etc"></a>Interacción de SKIP, NOSKIP, INIT y NOINIT  
 Esta tabla describen las interacciones entre el { **NOINIT** | INIT} y { **NOSKIP** | Opciones de omitir}.  
  
> [!NOTE]  
>  Si el medio de cinta está vacío o el archivo de copia de seguridad en disco no existe, todas estas interacciones escriben un encabezado de medios y continúan. Si el medio no está vacío y no contiene ningún encabezado de medios válido, estas operaciones proporcionan un comentario que indica que no se trata de un medio MTF válido y terminan la operación de copia de seguridad.  
  
||NOINIT|INIT|  
|------|------------|----------|  
|NOSKIP|Si el volumen contiene un encabezado de medios válido, se comprueba que el nombre del medio coincida con la opción MEDIANAME, si se proporcionó. Si coincide, se anexa el conjunto de copia de seguridad y se mantienen todos los conjuntos de copia de seguridad existentes.<br /> Si el volumen no contiene un encabezado de medios válido, se produce un error.|Si el volumen contiene un encabezado de medios válido, se realizan las siguientes comprobaciones:<br /> -Si se especificó MEDIANAME, comprueba que el nombre del medio proporcionado coincide con multimedia name.* * el encabezado de medios<br /> -Comprueba que no hay ningún conjunto de copia de seguridad vigente en el medio. Si los hay, se finaliza la copia de seguridad.<br /> Si las comprobaciones son correctas, se sobrescriben los conjuntos de copia de seguridad de los medios y solo se mantiene el encabezado de medios.<br /> Si el volumen no contiene ningún encabezado de medios válido, se genera uno utilizando las opciones MEDIANAME y MEDIADESCRIPTION especificadas, si se especificó alguna.|  
|SKIP|Si el volumen contiene un encabezado de medios válido, se anexa el conjunto de copia de seguridad, conservándose todos los conjuntos de copia de seguridad existentes.|Si el volumen contiene válido * encabezado de medios, sobrescribe los conjuntos de copia de seguridad de los medios, conservando el encabezado de medios.<br /> Si el medio está vacío, se genera un encabezado de medios utilizando las opciones MEDIANAME y MEDIADESCRIPTION, si se especificó alguna.|  
  
 * La validez incluye el número de versión MTF y otra información del encabezado. Si la versión especificada no se admite o se trata de un valor no esperado, se produce un error.  
  
 ** El usuario debe pertenecer a los roles de servidor o base de datos correspondientes fijos para realizar una operación de copia de seguridad.  
  
## <a name="compatibility"></a>Compatibilidad  
  
> [!CAUTION]  
>  Las copias de seguridad que se crean en una versión más reciente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se pueden restaurar en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 BACKUP admite la opción RESTART para proporcionar compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pero RESTART no tiene ningún efecto.  
  
## <a name="general-remarks"></a>Notas generales  
 Se pueden anexar copias de seguridad de la base de datos o de registros a cualquier dispositivo de disco o cinta, lo que permite mantener la base de datos y sus registros de transacciones en la misma ubicación física.  
  
 La instrucción BACKUP no se permite en una transacción explícita o implícita.  
  
 Se pueden realizar operaciones de copia de seguridad entre plataformas, incluso entre diferentes tipos de procesador, siempre que el sistema operativo admita la intercalación de la base de datos.  
  
> [!NOTE]  
>  De forma predeterminada, cada operación de copia de seguridad correcta agrega una entrada en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de eventos del sistema. Si hace una copia de seguridad del registro de transacciones con frecuencia, estos mensajes que indican la corrección de la operación pueden acumularse rápidamente, con lo que se crean registros de errores muy grandes que pueden dificultar la búsqueda de otros mensajes. En esos casos, puede suprimir estas entradas de registro utilizando la marca de seguimiento 3226 si ninguno de los scripts depende de esas entradas. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
## <a name="interoperability"></a>Interoperabilidad  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza un proceso de copia de seguridad en línea para permitir que se realice la copia de seguridad de una base de datos mientras se está utilizando. Durante la copia de seguridad, se pueden realizar la mayoría de las operaciones (por ejemplo, las instrucciones INSERT, UPDATE o DELETE están permitidas durante la operación de copia de seguridad).  
  
 Las operaciones que no se pueden ejecutar durante la copia de seguridad de la base de datos o los registros de transacciones son:  
  
-   Operaciones de administración de archivos como la instrucción ALTER DATABASE con las opciones ADD FILE o REMOVE FILE.  
  
-   Operaciones de reducción de la base de datos o de reducción de un archivo. Esto incluye las operaciones de reducción automática.  
  
Si una operación de copia de seguridad se solapa con una operación de administración de archivos o de reducción, surge un conflicto. Con independencia de la operación en conflicto que empieza en primer lugar, la segunda operación espera a que se agote el tiempo de espera del bloqueo establecido por la primera operación (el tiempo de espera se controla mediante un valor de tiempo de espera de sesión). Si el bloqueo se libera durante el tiempo de espera, la segunda operación continúa. Si se agota el tiempo de espera del bloqueo, la segunda operación no se realiza correctamente.  
  
## <a name="metadata"></a>Metadatos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye las siguientes tablas del historial de copias de seguridad que realizan un seguimiento de la actividad de copia de seguridad:  
  
-   [backupfile &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)  
-   [backupfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)  
-   [backupmediafamily &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)  
-   [backupmediaset &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)  
-   [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)  
  
Cuando se realiza una restauración, si el conjunto de copia de seguridad no se ha registrado en el **msdb** la base de datos, el historial de copia de seguridad puede modificar las tablas.  
  
## <a name="security"></a>Seguridad  
 A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], **contraseña** y **MEDIAPASSWORD** opciones se suspenden para crear copias de seguridad. Todavía es posible restaurar copias de seguridad creadas con contraseñas.  
  
### <a name="permissions"></a>Permissions  
 De forma predeterminada, los permisos BACKUP DATABASE y BACKUP LOG corresponden a los miembros del rol fijo de servidor **sysadmin** y de los roles fijos de base de datos **db_owner** y **db_backupoperator** .  
  
 Los problemas de propiedad y permisos del archivo físico del dispositivo de copia de seguridad pueden interferir con una operación de copia de seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe poder leer y escribir en el dispositivo y la cuenta en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos de escritura. En cambio, [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), que agrega una entrada para un dispositivo de copia de seguridad en las tablas del sistema, no comprueba los permisos de acceso a los archivos. Es posible que estos problemas con el archivo físico del dispositivo de copia de seguridad no aparezcan hasta que se tenga acceso al recurso físico, al intentar la copia de seguridad o la restauración.  
  
##  <a name="examples"></a> Ejemplos  
 Esta sección contiene los siguientes ejemplos:  
  
-   A. [Realizar una copia de seguridad completa de la base de datos](#backing_up_db)  
-   B. [Copia de seguridad de la base de datos y el registro](#backing_up_db_and_log)  
-   C. [Crear una copia de seguridad completa de los grupos de archivos secundarios](#full_file_backup)  
-   D. [Crear una copia de seguridad diferencial de archivos secundarios](#differential_file_backup)  
-   E. [Crear y copias de seguridad en un sola familia de medios reflejado conjunto](#create_single_family_mirrored_media_set)  
-   F. [Crear y copias de seguridad en un varias familias de medios reflejado conjunto](#create_multifamily_mirrored_media_set)  
-   G [conjunto de medios reflejado de copia de seguridad en una existente](#existing_mirrored_media_set)  
-   H. [Crear una copia de seguridad comprimida en un conjunto de medios](#creating_compressed_backup_new_media_set)  
-   I.  [Copia de seguridad en el servicio de almacenamiento de blobs de Microsoft Azure](#url)  
  
> [!NOTE]  
>  Los temas de procedimientos de copia de seguridad contienen más ejemplos. Para obtener más información, vea [Información general de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="backing_up_db"></a> A. Realizar una copia de seguridad completa de la base de datos  
 En el ejemplo siguiente se realiza una copia de la [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] base de datos a un archivo de disco.  
  
```sql  
BACKUP DATABASE AdventureWorks2012   
 TO DISK = 'Z:\SQLServerBackups\AdvWorksData.bak'  
   WITH FORMAT;  
GO  
```  
  
###  <a name="backing_up_db_and_log"></a> B. Realizar una copia de seguridad de la base de datos y el registro  
 En el ejemplo siguiente se realiza la copia de seguridad de la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], que usa de forma predeterminada un modelo de recuperación simple. Para admitir las copias de seguridad del registro, la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] se ha modificado para usar el modelo de recuperación completa.  
  
 A continuación, en el ejemplo se utiliza [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) para crear un valor lógico [dispositivo de copia de seguridad](../../relational-databases/backup-restore/backup-devices-sql-server.md) para realizar una copia de seguridad de los datos, `AdvWorksData`y crea otro dispositivo lógico de copia de seguridad para realizar una copia de seguridad del registro, `AdvWorksLog`.  
  
 A continuación, en el ejemplo se crea una copia de seguridad de base de datos completa en `AdvWorksData` y, tras un periodo de actividad de actualización, se copia el registro en `AdvWorksLog`.  
  
```sql  
-- To permit log backups, before the full database backup, modify the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
   SET RECOVERY FULL;  
GO  
-- Create AdvWorksData and AdvWorksLog logical backup devices.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksData',   
'Z:\SQLServerBackups\AdvWorksData.bak';  
GO  
EXEC sp_addumpdevice 'disk', 'AdvWorksLog',   
'X:\SQLServerBackups\AdvWorksLog.bak';  
GO  
  
-- Back up the full AdventureWorks2012 database.  
BACKUP DATABASE AdventureWorks2012 TO AdvWorksData;  
GO  
-- Back up the AdventureWorks2012 log.  
BACKUP LOG AdventureWorks2012  
   TO AdvWorksLog;  
GO  
```  
  
> [!NOTE]  
>  En el caso de una base de datos de producción, haga una copia de seguridad del registro periódicamente. Las copias de seguridad del registro se deben realizar con una frecuencia suficiente para ofrecer la protección necesaria frente a la pérdida de datos.  
  
###  <a name="full_file_backup"></a> C. Crear una copia de seguridad de archivos completa de los grupos de archivos secundarios  
 En el ejemplo siguiente se crea una copia de seguridad de archivos completa de cada archivo en los dos grupos de archivos secundarios.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck';  
GO  
```  
  
###  <a name="differential_file_backup"></a> D. Crear una copia de seguridad de archivos diferencial de los grupos de archivos secundarios  
 En el ejemplo siguiente se crea una copia de seguridad de archivos diferencial de cada archivo en los dos grupos de archivos secundarios.  
  
```sql  
--Back up the files in SalesGroup1:  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'Z:\SQLServerBackups\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
###  <a name="create_single_family_mirrored_media_set"></a> E. Crear y realizar una copia de seguridad en un conjunto de medios reflejado de una sola familia  
 En el siguiente ejemplo se crea un conjunto de medios reflejado que contiene una sola familia de medios y cuatro reflejos, y se realiza una copia de seguridad de la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] en ellos.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0'  
MIRROR TO TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2'  
MIRROR TO TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet0';  
```  
  
###  <a name="create_multifamily_mirrored_media_set"></a> F. Crear y realizar una copia de seguridad en un conjunto de medios reflejado de varias familias  
 En el siguiente ejemplo se crea un conjunto de medios reflejado en el que cada reflejo consta de dos familias de medios. A continuación, se realiza una copia de seguridad de la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] en ambos reflejos.  
  
```sql  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
   FORMAT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
###  <a name="existing_mirrored_media_set"></a>G. Realizar una copia de seguridad en un conjunto de medios reflejado existente  
 En el siguiente ejemplo se anexa un conjunto de copia de seguridad al conjunto de medios creado en el ejemplo anterior.  
  
```sql  
BACKUP LOG AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH   
   NOINIT,  
   MEDIANAME = 'AdventureWorksSet1';  
```  
  
> [!NOTE]  
>  NOINIT, que es el valor predeterminado, se muestra aquí para mayor claridad.  
  
###  <a name="creating_compressed_backup_new_media_set"></a>H. Crear una copia de seguridad comprimida en un nuevo conjunto de medios  
 En el ejemplo siguiente se da formato a los medios, creando un nuevo conjunto de medios, y se realiza una copia de seguridad completa comprimida de la base de datos [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)].  
  
```sql  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   COMPRESSION;  
```  

###  <a name="url"></a>I. Realizar una copia de seguridad del servicio de almacenamiento de blobs de Microsoft Azure 
En el ejemplo se realiza una copia de seguridad completa de la base de datos de `Sales` en el servicio de almacenamiento de blobs de Microsoft Azure.  El nombre de la cuenta de almacenamiento es `mystorageaccount`.  El contenedor se denomina `myfirstcontainer`.  Se ha creado una directiva de acceso almacenada con derechos de lectura, escritura, eliminación y lista.  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] credencial, `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`, se creó con una firma de acceso compartido que está asociado a la directiva de acceso almacenada.  Para obtener información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] copia de seguridad para el servicio de almacenamiento de blobs de Windows Azure, consulte [copias de seguridad de SQL Server y restauración con el servicio de almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) y [copias de seguridad de SQL Server a URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md).

```sql  
BACKUP DATABASE Sales
TO URL = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer/Sales_20160726.bak'
WITH STATS = 5;
```

  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC SQLPERF &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-filelistonly-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [sp_helpfile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfile-transact-sql.md)   
 [sp_helpfilegroup &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpfilegroup-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Restauración por etapas de bases de datos con tablas con optimización para memoria](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md)  
  
  
