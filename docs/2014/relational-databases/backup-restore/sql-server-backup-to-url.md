---
title: Copia de seguridad en URL de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 11be89e9-ff2a-4a94-ab5d-27d8edf9167d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ebc7fb8d170ddac10f1a326b3c05a54a0896666
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688738"
---
# <a name="sql-server-backup-to-url"></a>Copia de seguridad en URL de SQL Server
  En este tema se presentan los conceptos, los requisitos y los componentes necesarios para utilizar el servicio de almacenamiento de blobs de Azure como destino de copia de seguridad. La funcionalidad de copia de seguridad y restauración es igual o similar que la que usa DISK o TAPE, con algunas diferencias. En este tema se incluyen las diferencias, excepciones notables y algunos ejemplos de código.  
  
## <a name="requirements-components-and-concepts"></a>Requisitos, componentes y conceptos  
 **Esta sección:**  
  
-   [Seguridad](#security)  
  
-   [Introducción a los principales componentes y conceptos](#intorkeyconcepts)  
  
-   [Servicio de Azure Blob Storage](#Blob)  
  
-   [Componentes de SQL Server](#sqlserver)  
  
-   [Limitaciones](#limitations)  
  
-   [Compatibilidad con instrucciones BACKUP y RESTORE](#Support)  
  
-   [Usar la tarea Copia de seguridad en SQL Server Management Studio](sql-server-backup-to-url.md#BackupTaskSSMS)  
  
-   [Copia de seguridad de SQL Server en una dirección URL mediante el Asistente para planes de mantenimiento](sql-server-backup-to-url.md#MaintenanceWiz)  
  
-   [Restauración desde Azure Storage con SQL Server Management Studio](sql-server-backup-to-url.md#RestoreSSMS)  
  
###  <a name="security"></a> Seguridad  
 A continuación se muestran los requisitos y las consideraciones de seguridad al realizar copias de seguridad o restaurar desde los servicios de almacenamiento de blobs de Azure.  
  
-   Al crear un contenedor para el servicio de almacenamiento de blobs de Azure, se recomienda establecer el acceso en **privado**. Al configurar el acceso privado se restringe el acceso a los usuarios o las cuentas capaces de proporcionar la información necesaria para autenticarse en la cuenta de Azure.  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiere que el nombre de cuenta de Azure y la autenticación de clave de acceso se almacenen en una credencial de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta información se usa para autenticarse en la cuenta de Azure cuando realiza operaciones de copia de seguridad o restauración.  
  
-   La cuenta de usuario que se usa para emitir comandos BACKUP o RESTORE debe tener el rol de base de datos **operador de db_backup** con permisos **Modificar cualquier credencial** .  
  
###  <a name="intorkeyconcepts"></a> Introducción a los principales componentes y conceptos  
 En las dos secciones siguientes se presentan el servicio de almacenamiento de blobs de Azure y los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se usan para realizar copias de seguridad o restaurar desde el servicio de almacenamiento de blobs de Azure. Es importante comprender los componentes y la interacción entre ellos para realizar una copia de seguridad o una restauración desde el servicio de almacenamiento de blobs de Azure.  
  
 La creación de una cuenta de Azure es el primer paso de este proceso. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa el **nombre** de la cuenta de almacenamiento de Azure y sus valores de **clave de acceso** para autenticar y escribir y leer blobs en el servicio de almacenamiento. La credencial de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena esta información de autenticación y se emplea durante las operaciones de copia de seguridad o restauración. Para obtener un tutorial completo sobre cómo crear una cuenta de almacenamiento y realizar una restauración simple, vea el tutorial sobre cómo [usar el servicio de Azure Storage para la copia de seguridad y restauración de SQL Server](https://go.microsoft.com/fwlink/?LinkId=271615).  
  
 ![asignación de la cuenta de almacenamiento a las credenciales de SQL](../../tutorials/media/backuptocloud-storage-credential-mapping.gif "asignación de la cuenta de almacenamiento a las credenciales de SQL")  
  
###  <a name="Blob"></a>Servicio de Azure Blob Storage  
 **Cuenta de almacenamiento** : la cuenta de almacenamiento es el punto de partida para todos los servicios de almacenamiento. Para acceder al servicio Azure Blob Storage, cree primero una cuenta de Azure Storage. El **nombre** de la cuenta de almacenamiento y sus propiedades de **clave de acceso** son necesarias para autenticarse en el servicio de Azure BLOB Storage y sus componentes.  
  
 **Contenedor** : un contenedor proporciona una agrupación de un conjunto de blobs y puede almacenar un número ilimitado de blobs. Para escribir una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Blob service de Azure, debe haber creado al menos el contenedor raíz.  
  
 **Blob** : un archivo de cualquier tipo y tamaño. Hay dos tipos de blobs que se pueden almacenar en el servicio de almacenamiento de blobs de Azure: blobs en bloques y en páginas. La copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa blobs en páginas como tipo de blob. Los blobs son direccionables mediante el siguiente formato de dirección URL: https://\<storage cuenta >. BLOB. Core. Windows. net/\<container >/\<blob >  
  
 ![Azure Blob Storage](../../database-engine/media/backuptocloud-blobarchitecture.gif "Almacenamiento de blobs de Azure")  
  
 Para obtener más información sobre el servicio Azure BLOB Storage, consulte [uso del servicio de Azure BLOB Storage](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)  
  
 Para obtener más información sobre los blobs en páginas, vea [Descripción de los blobs en bloques y los blobs en páginas](https://msdn.microsoft.com/library/windowsazure/ee691964.aspx).  
  
###  <a name="sqlserver"></a> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Components  
 **Dirección URL:** una dirección URL especifica un identificador uniforme de recursos (URI) para un archivo de copia de seguridad único. La dirección URL se emplea para proporcionar la ubicación y el nombre del archivo de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En esta implementación, la única dirección URL válida es aquella que señala a un BLOB en páginas en una cuenta de almacenamiento de Azure. La dirección URL debe apuntar a un blob real, no solo a un contenedor. Si el blob no existe, se crea. Si se especifica un BLOB existente, se produce un error en la copia de seguridad, a menos que se especifique la opción "WITH FORMAT".  
  
> [!WARNING]  
>  Si elige copiar y cargar un archivo de copia de seguridad en el servicio de almacenamiento de blobs de Azure, use el BLOB en páginas como opción de almacenamiento. No se admiten restauraciones desde blobs en bloques. La instrucción RESTORE desde un tipo de blob en bloques produce un error.  
  
 Este es un valor de dirección URL de ejemplo: http [s]://ACCOUNTNAME.Blob.core.windows.net/\<CONTAINER >/\<FILENAME. bak >. HTTPS no es necesario, pero es recomendable.  
  
 **Credencial:** una credencial de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un objeto que se usa para almacenar la información de autenticación necesaria para conectarse a un recurso fuera de SQL Server.  En este caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesos de copia de seguridad y restauración usan credenciales para autenticarse en el servicio de almacenamiento de blobs de Azure. La credencial contiene los valores de nombre y la **clave de acceso** de la cuenta de almacenamiento. Una vez creada la credencial, se debe especificar en la opción WITH CREDENTIAL al emitir las instrucciones BACKUP y RESTORE. Para obtener más información sobre cómo ver, copiar o regenerar **access keys**de cuentas de almacenamiento, vea [Ver, copiar y regenerar las claves de acceso de una cuenta de almacenamiento de Windows Azure](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Para obtener instrucciones paso a paso sobre cómo crear una credencial de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea el ejemplo de [Create a Credential](#credential) más adelante en este tema.  
  
 Para obtener información general sobre las credenciales, vea [Credenciales](../security/authentication-access/credentials-database-engine.md).  
  
 Para obtener información sobre otros ejemplos donde se usan credenciales, vea [Crear un proxy del Agente SQL Server](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
###  <a name="limitations"></a> Limitaciones  
  
-   No se pueden realizar copias de seguridad en el almacenamiento premium.  
  
-   El tamaño máximo de copia de seguridad admitido es 1 TB.  
  
-   Puede emitir instrucciones de copia de seguridad o de restauración mediante cmdlets de PowerShell, SMO o TSQL. Actualmente no está habilitada la copia de seguridad o la restauración desde el servicio de almacenamiento de blobs de Azure mediante SQL Server Management Studio Asistente para copia de seguridad o restauración.  
  
-   No se admite la creación de un nombre de dispositivo lógico. Por tanto, no se admite agregar URL como dispositivo de copia de seguridad mediante sp_dumpdevice o mediante SQL Server Management Studio.  
  
-   No se admite anexar a blobs de copia de seguridad existentes. Las copias de seguridad en un blob existente solo se pueden sobrescribir mediante la opción WITH FORMAT.  
  
-   No se admite la copia de seguridad en varios blobs en una sola operación de copia de seguridad. Por ejemplo, el código siguiente devuelve un error:  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_1.bak'   
       URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_2.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,STATS = 5;  
    GO  
  
    ```  
  
-   No se admite especificar un tamaño de bloque con `BACKUP`.  
  
-   No se admite especificar `MAXTRANSFERSIZE`.  
  
-   No se admite especificar opciones de conjunto de copia de seguridad, `RETAINDAYS` y `EXPIREDATE`.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene un límite máximo de 259 caracteres para un nombre de dispositivo de copia de seguridad. BACKUP TO URL consume 36 caracteres para los elementos necesarios que se usan para especificar la dirección URL: "https://.blob.core.windows.net//.bak", y deja 223 caracteres para la cuenta, el contenedor y los nombres de blob.  
  
###  <a name="Support"></a> Compatibilidad con instrucciones BACKUP y RESTORE  
  
|||||  
|-|-|-|-|  
|Instrucción BACKUP/RESTORE|Admitida|Excepciones|Comentarios|  
|BACKUP|&#x2713;|No se admiten BLOCKSIZE y MAXTRANSFERSIZE.|Es necesario especificar WITH CREDENTIAL|  
|RESTORE|&#x2713;||Es necesario especificar WITH CREDENTIAL|  
|RESTORE FILELISTONLY|&#x2713;||Es necesario especificar WITH CREDENTIAL|  
|RESTORE HEADERONLY|&#x2713;||Es necesario especificar WITH CREDENTIAL|  
|RESTORE LABELONLY|&#x2713;||Es necesario especificar WITH CREDENTIAL|  
|RESTORE VERIFYONLY|&#x2713;||Es necesario especificar WITH CREDENTIAL|  
|RESTORE REWINDONLY|&#x2713;|||  
  
 Para conocer la sintaxis y obtener información general sobre las instrucciones de copia de seguridad, vea [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
 Para conocer la sintaxis y obtener información general sobre las instrucciones de restauración, vea [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
### <a name="support-for-backup-arguments"></a>Compatibilidad con los argumentos de copia de seguridad  
  
|||||  
|-|-|-|-|  
|Argumento|Admitida|Exception|Comentarios|  
|DATABASE|&#x2713;|||  
|LOG|&#x2713;|||  
||  
|TO (URL)|&#x2713;|A diferencia de DISK y TAPE, URL no admite especificar o crear un nombre lógico.|Este argumento se emplea para especificar la ruta de acceso de la dirección URL del archivo de copia de seguridad.|  
|MIRROR TO|&#x2713;|||  
|**OPCIONES DE WITH:**||||  
|CREDENTIAL|&#x2713;||WITH CREDENTIAL solo se admite cuando se usa la opción BACKUP TO URL para hacer una copia de seguridad en el servicio Azure BLOB Storage.|  
|DIFFERENTIAL|&#x2713;|||  
|COPY_ONLY|&#x2713;|||  
|COMPRESSION&#124;NO_COMPRESSION|&#x2713;|||  
|Descripción|&#x2713;|||  
|NAME|&#x2713;|||  
|EXPIREDATE &#124; RETAINDAYS|&#x2713;|||  
|NOINIT &#124; INIT|&#x2713;||Esta opción se omite si se usa.<br /><br /> No es posible anexar a blobs. Para sobrescribir una copia de seguridad, use el argumento FORMAT.|  
|NOSKIP &#124; SKIP|&#x2713;|||  
|NOFORMAT &#124; FORMAT|&#x2713;||Esta opción se omite si se usa.<br /><br /> Una copia de seguridad realizada en un blob existente producirá un error a menos que se especifique WITH FORMAT. Se sobrescribe el blob existente si se especifica WITH FORMAT.|  
|MEDIADESCRIPTION|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|NO_CHECKSUM &#124; CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|STATS|&#x2713;|||  
|REWIND &#124; NOREWIND|&#x2713;|||  
|UNLOAD &#124; NOUNLOAD|&#x2713;|||  
|NORECOVERY &#124; STANDBY|&#x2713;|||  
|NO_TRUNCATE|&#x2713;|||  
  
 Para obtener más información sobre los argumentos de copia de seguridad, vea [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
### <a name="support-for-restore-arguments"></a>Compatibilidad con los argumentos de restauración  
  
|||||  
|-|-|-|-|  
|Argumento|Admitida|Excepciones|Comentarios|  
|DATABASE|&#x2713;|||  
|LOG|&#x2713;|||  
|FROM (URL)|&#x2713;||El argumento FROM URL se emplea para especificar la ruta de acceso de la dirección URL del archivo de copia de seguridad.|  
|**WITH Options:**||||  
|CREDENTIAL|&#x2713;||WITH CREDENTIAL solo se admite cuando se usa la opción RESTOre FROM URL para restaurar desde Azure Blob Storage Service.|  
|PARTIAL|&#x2713;|||  
|RECOVERY &#124; NORECOVERY &#124; STANDBY|&#x2713;|||  
|LOADHISTORY|&#x2713;|||  
|MOVE|&#x2713;|||  
|REPLACE|&#x2713;|||  
|RESTART|&#x2713;|||  
|RESTRICTED_USER|&#x2713;|||  
|FILE|&#x2713;|||  
|PASSWORD|&#x2713;|||  
|MEDIANAME|&#x2713;|||  
|MEDIAPASSWORD|&#x2713;|||  
|BLOCKSIZE|&#x2713;|||  
|BUFFERCOUNT|&#x2713;|||  
|MAXTRANSFERSIZE|&#x2713;|||  
|CHECKSUM &#124; NO_CHECKSUM|&#x2713;|||  
|STOP_ON_ERROR &#124; CONTINUE_AFTER_ERROR|&#x2713;|||  
|FILESTREAM|&#x2713;|||  
|STATS|&#x2713;|||  
|REWIND &#124; NOREWIND|&#x2713;|||  
|UNLOAD &#124; NOUNLOAD|&#x2713;|||  
|KEEP_REPLICATION|&#x2713;|||  
|KEEP_CDC|&#x2713;|||  
|ENABLE_BROKER &#124; ERROR_BROKER_CONVERSATIONS &#124; NEW_BROKER|&#x2713;|||  
|STOPAT &#124; STOPATMARK &#124; STOPBEFOREMARK|&#x2713;|||  
  
 Para obtener más información sobre los argumentos de restauración, vea [RESTORE &#40;argumentos, Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql).  
  
##  <a name="BackupTaskSSMS"></a>Uso de la tarea de copia de seguridad en SQL Server Management Studio  
 La tarea de copia de seguridad de SQL Server Management Studio se ha mejorado para incluir la dirección URL como una de las opciones de destino y otros objetos de compatibilidad necesarios para realizar la copia de seguridad en Azure Storage, como la credencial SQL.  
  
 En los pasos siguientes se describen los cambios realizados en la tarea copia de seguridad de base de datos para permitir realizar copias de seguridad en Azure Storage:  
  
1.  Inicie SQL Server Management Studio y conéctese a una instancia de SQL Server.  Seleccione una base de datos de la que desee hacer una copia de seguridad, haga clic con el botón derecho en **tareas**y seleccione **copia de seguridad..** . Se abrirá el cuadro de diálogo copia de seguridad de base de datos.  
  
2.  En la página general, se usa la opción **dirección URL** para crear una copia de seguridad en Azure Storage. Al seleccionar esta opción, se ven otras opciones habilitadas en esta página:  
  
    1.  **Nombre de archivo:** nombre del archivo de copia de seguridad.  
  
    2.  **Credencial SQL:** puede especificar una credencial existente de SQL Server o crear una nueva haciendo clic en **Crear** , junto al cuadro Credencial SQL.  
  
        > [!IMPORTANT]  
        >  El cuadro de diálogo que se abre al hacer clic en **Crear** requiere un certificado de administración o el perfil de publicación para la suscripción. SQL Server admite actualmente la versión 2.0 del perfil de publicación. Para descargar la versión compatible del perfil de publicación, vea [Descargar perfil de publicación 2.0](https://go.microsoft.com/fwlink/?LinkId=396421).  
        >   
        >  Si no tiene acceso al certificado de administración o al perfil de publicación, puede crear una credencial de SQL; para ello, especifique la información del nombre de cuenta de almacenamiento y de clave de acceso mediante Transact-SQL o SQL Server Management Studio. Vea el código de ejemplo de la sección [Crear una credencial](#credential) para crear una credencial mediante Transact-SQL. O bien, con SQL Server Management Studio, desde el motor de base de datos, haga clic con el botón secundario en **Seguridad**, seleccione **Nuevo**y **Credencial**. Especifique el nombre de cuenta de almacenamiento para **Identidad** y la clave de acceso en el campo **Contraseña** .  
  
    3.  **Contenedor de Azure Storage:** Nombre del contenedor de almacenamiento de Azure en el que se almacenarán los archivos de copia de seguridad.  
  
    4.  **Prefijo de dirección URL:** se genera automáticamente con la información especificada en los campos que se describen en los pasos anteriores. Si edita este valor manualmente, asegúrese de que coincide con el resto de la información que proporcionó antes. Por ejemplo, si modifica la dirección URL de almacenamiento, asegúrese de que la credencial SQL está establecida para autenticar en la misma cuenta de almacenamiento.  
  
 Al seleccionar la dirección URL como destino, ciertas opciones de la página **Opciones multimedia** están deshabilitadas.  Los temas siguientes tienen más información acerca del cuadro de diálogo Copia de seguridad de la base de datos:  
  
 [Copia de seguridad de base de datos &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
 [Copia de seguridad de la base de datos &#40;página Opciones multimedia&#41;](back-up-database-media-options-page.md)  
  
 [Copia de seguridad de la base de datos &#40;página Opciones de copia de seguridad&#41;](back-up-database-backup-options-page.md)  
  
 [Crear credencial - autenticarse en Azure Storage](create-credential-authenticate-to-azure-storage.md)  
  
##  <a name="MaintenanceWiz"></a> Copia de seguridad de SQL Server en una dirección URL mediante el Asistente para planes de mantenimiento  
 Al igual que la tarea de copia de seguridad descrita anteriormente, el Asistente para planes de mantenimiento de SQL Server Management Studio se ha mejorado para incluir la **dirección URL** como una de las opciones de destino y otros objetos de compatibilidad necesarios para realizar la copia de seguridad en Azure Storage como SQL Caja. Para obtener más información, consulte la sección **Definir las tareas de copia de seguridad** en [Using Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md#SSMSProcedure).  
  
##  <a name="RestoreSSMS"></a>Restauración desde Azure Storage mediante SQL Server Management Studio  
 Si restaura una base de datos, **Dirección URL** se incluye como dispositivo desde el que restaurar. En los pasos siguientes se describen los cambios en la tarea de restauración para permitir la restauración desde Azure Storage:  
  
1.  Al seleccionar **Dispositivos** en la página **General** de la tarea Restaurar en SQL Server Management Studio, se le llevará al cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** que incluye **Dirección URL** como tipo de medio de copia de seguridad.  
  
2.  Al seleccionar **Dirección URL** y hacer clic en **Agregar**, se abre el cuadro de diálogo **Conectar al almacenamiento de Windows Azure** . Especifique la información de la credencial SQL para autenticarse en Azure Storage.  
  
3.  A continuación, SQL Server se conecta a Azure Storage con la información de la credencial SQL proporcionada y abre el cuadro **de diálogo Buscar archivo de copia de seguridad en Azure** . Los archivos de copia de seguridad que residen en el almacenamiento se muestran en esta página. Seleccione el archivo que desee usar para restaurar y haga clic en **Aceptar**. De esta forma, vuelve al cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** y, haciendo clic en **Aceptar** en este cuadro de diálogo, vuelve al cuadro de diálogo principal **Restaurar** donde podrá completar la restauración.  Para obtener más información, vea los siguientes temas:  
  
     [Restaurar la base de datos &#40;página General&#41;](restore-database-general-page.md)  
  
     [Restaurar base de datos &#40;página Archivos&#41;](restore-database-files-page.md)  
  
     [Restaurar base de datos &#40;página Opciones&#41;](restore-database-options-page.md)  
  
##  <a name="Examples"></a> Ejemplos de código  
 Esta sección contiene los siguientes ejemplos.  
  
-   [Crear una credencial](#credential)  
  
-   [Realizar una copia de seguridad completa de la base de datos](#complete)  
  
-   [Realizar una copia de seguridad de la base de datos y el registro](#databaselog)  
  
-   [Crear una copia de seguridad de archivos completa del grupo de archivos principal](#filebackup)  
  
-   [Crear una copia de seguridad diferencial de archivos de los grupos de archivos principales](#differential)  
  
-   [Restaurar una base de datos y mover archivos](#restoredbwithmove)  
  
-   [Restaurar a un momento dado con STOPAT](#PITR)  
  
###  <a name="credential"></a> Crear una credencial  
 En el ejemplo siguiente se crea una credencial que almacena la información de autenticación de Azure Storage.  
  
1.  **Tsql**  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL mycredential WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key>' ;  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
    string secret = "<storage access key>";  
  
    // Create a Credential  
    string credentialName = "mycredential";  
    Credential credential = new Credential(server, credentialName);  
    credential.Create(identity, secret);  
    ```  
  
3.  **PowerShell**  
  
    ```  
    # create variables  
    $storageAccount = "mystorageaccount"  
    $storageKey = "<storage access key>"  
    $secureString = convertto-securestring $storageKey  -asplaintext -force  
    $credentialName = "mycredential"  
  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Create a credential  
     New-SqlCredential -Name $credentialName -Path $srvpath -Identity $storageAccount -Secret $secureString  
  
    ```  
  
###  <a name="complete"></a>Copia de seguridad de una base de datos completa  
 En el ejemplo siguiente se realiza una copia de seguridad de la base de datos AdventureWorks2012 en el servicio Azure BLOB Storage.  
  
1.  **Tsql**  
  
    ```  
    BACKUP DATABASE AdventureWorks2012   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
          WITH CREDENTIAL = 'mycredential'   
         ,COMPRESSION  
         ,STATS = 5;  
    GO  
  
    ```  
  
1.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
    ```  
  
2.  **PowerShell**  
  
    ```  
    # create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"   
    # for default instance, the $srvpath varilable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
    CD $srvPath   
    $backupFile = $backupUrlContainer + "AdventureWorks2012" +  ".bak"  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On  
  
    ```  
  
###  <a name="databaselog"></a>Realizar copias de seguridad de la base de datos y del registro  
 En el ejemplo siguiente se realiza la copia de seguridad de la base de datos de ejemplo AdventureWorks2012, que usa de forma predeterminada el modelo de recuperación simple. Para admitir copias de seguridad de registros, se ha modificado la base de datos AdventureWorks2012 para usar el modelo de recuperación completa. A continuación, en el ejemplo se crea una copia de seguridad de base de datos completa en BLOB de Azure y, después de un período de actividad de actualización, se realiza una copia de seguridad del registro. En este ejemplo se crea un nombre de archivo de copia de seguridad con una marca de fecha y hora.  
  
1.  **Tsql**  
  
    ```  
    -- To permit log backups, before the full database backup, modify the database   
    -- to use the full recovery model.  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks2012  
       SET RECOVERY FULL;  
    GO  
  
    -- Back up the full AdventureWorks2012 database.  
           -- First create a file name for the backup file with DateTime stamp  
  
    DECLARE @Full_Filename AS VARCHAR (300);  
    SET @Full_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Full_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.bak';   
    --Back up Adventureworks2012 database  
  
    BACKUP DATABASE AdventureWorks2012  
    TO URL =  @Full_Filename  
    WITH CREDENTIAL = 'mycredential';  
    ,COMPRESSION  
    GO  
    -- Back up the AdventureWorks2012 log.  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url for data backup  
    string urlDataBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Data-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database to Url  
    Backup backupData = new Backup();  
    backupData.CredentialName = credentialName;  
    backupData.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupData.Devices.AddDevice(urlDataBackup, DeviceType.Url);  
    backupData.SqlBackup(server);  
  
    // Generate Unique Url for data backup  
    string urlLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}_Log-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Database Log to Url  
    Backup backupLog = new Backup();  
    backupLog.CredentialName = credentialName;  
    backupLog.Database = dbName;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backupLog.Devices.AddDevice(urlLogBackup, DeviceType.Url);  
    backupLog.Action = BackupActionType.Log;  
    backupLog.SqlBackup(server);  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to theSQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the full database backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Backup Database to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Database    
  
    #Create a unique file name for log backup  
  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup Log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Log  
  
    ```  
  
###  <a name="filebackup"></a>Crear una copia de seguridad de archivos completa del grupo de archivos principal  
 En el ejemplo siguiente se crea una copia de seguridad de archivos completa del grupo de archivos principal.  
  
1.  **Tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012files.bck'  
       WITH CREDENTIAL = 'mycredential'  
       ,COMPRESSION;  
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bck",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to the SQL Server Instance  
  
    CD $srvPath   
    #Create a unique file name for the file backup  
    $backupFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bck"  
  
    #Backup Primary File Group to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary  
  
    ```  
  
###  <a name="differential"></a>Crear una copia de seguridad diferencial de archivos del grupo de archivos principal  
 En el ejemplo siguiente se crea una copia de seguridad de archivos diferencial del grupo de archivos principal.  
  
1.  **Tsql**  
  
    ```  
    --Back up the files in Primary:  
    BACKUP DATABASE AdventureWorks2012  
       FILEGROUP = 'Primary'  
       TO URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012filesdiff.bck'  
       WITH   
          CREDENTIAL = 'mycredential'  
          ,COMPRESSION  
      ,DIFFERENTIAL;  
    GO  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string url = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Action = BackupActionType.Files;  
    backup.DatabaseFileGroups.Add("PRIMARY");  
    backup.Incremental = true;  
    backup.CompressionOption = BackupCompressionOptions.On;  
    backup.Devices.AddDevice(url, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    #Create a differential backup of the primary filegroup  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName -CompressionOption On -BackupAction Files -DatabaseFileGroup Primary -Incremental  
  
    ```  
  
###  <a name="restoredbwithmove"></a>Restaurar una base de datos y migrar archivos  
 Para restaurar una copia de seguridad completa y mover la base de datos restaurada al directorio C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data, realice los pasos siguientes.  
  
1.  **Tsql**  
  
    ```  
    -- Backup the tail of the log first  
  
    DECLARE @Log_Filename AS VARCHAR (300);  
    SET @Log_Filename = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012_Log_'+   
    REPLACE (REPLACE (REPLACE (CONVERT (VARCHAR (40), GETDATE (), 120), '-','_'),':', '_'),' ', '_') + '.trn';  
    BACKUP LOG AdventureWorks2012  
     TO URL = @Log_Filename  
    WITH CREDENTIAL = 'mycredential'  
    ,NORECOVERY;  
    GO  
  
    RESTORE DATABASE AdventureWorks2012 FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'  
    WITH CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,MOVE 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,STATS = 5  
  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for tail log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath  + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName+ "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTNACENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # navigate to SQL Server Instance   
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On      
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery    
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath)  
  
    ```  
  
###  <a name="PITR"></a> Restaurar a un momento dado con STOPAT  
 En el ejemplo siguiente se restaura una base de datos a su estado en un momento dado y se muestra una operación de restauración.  
  
1.  **Tsql**  
  
    ```  
    RESTORE DATABASE AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.bak'   
    WITH   
     CREDENTIAL = 'mycredential'  
    ,MOVE 'AdventureWorks2012_data' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf'  
    ,Move 'AdventureWorks2012_log' to 'C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf'  
    ,NORECOVERY  
    --,REPLACE  
    ,STATS = 5;  
    GO   
  
    RESTORE LOG AdventureWorks FROM URL = 'https://mystorageaccount.blob.core.windows.net/mycontainer/AdventureWorks2012.trn'   
    WITH CREDENTIAL = 'mycredential'  
    ,RECOVERY   
    ,STOPAT = 'Oct 23, 2012 5:00 PM'   
    GO  
    ```  
  
2.  **C#**  
  
    ```  
    // Connect to default sql server instance on local machine  
    Server server = new Server(".");  
    string identity = "mystorageaccount";  
  
    string credentialName = "mycredential";  
    string dbName = "AdventureWorks2012";  
    string blobContainerName = "mycontainer";  
  
    // Generate Unique Url  
    string urlBackupData = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-Data{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup to Url  
    Backup backup = new Backup();  
    backup.CredentialName = credentialName;  
    backup.Database = dbName;  
    backup.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    backup.SqlBackup(server);  
  
    // Generate Unique Url for Tail Log backup  
    string urlTailLogBackup = String.Format(@"https://{0}.blob.core.windows.net/{1}/{2}-TailLog{3}.bak",  
            identity,  
            blobContainerName,  
            dbName,  
            DateTime.Now.ToString("s").Replace(":", "-"));  
  
    // Backup Tail Log to Url  
    Backup backupTailLog = new Backup();  
    backupTailLog.CredentialName = credentialName;  
    backupTailLog.Database = dbName;  
    backupTailLog.Action = BackupActionType.Log;  
    backupTailLog.NoRecovery = true;  
    backupTailLog.Devices.AddDevice(urlTailLogBackup, DeviceType.Url);  
    backupTailLog.SqlBackup(server);  
  
    // Restore a database and move files  
    string newDataFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".mdf";  
    string newLogFilePath = server.MasterDBLogPath + @"\" + dbName + DateTime.Now.ToString("s").Replace(":", "-") + ".ldf";  
  
    Restore restore = new Restore();  
    restore.CredentialName = credentialName;  
    restore.Database = dbName;  
    restore.ReplaceDatabase = true;  
    restore.NoRecovery = true;  
    restore.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restore.RelocateFiles.Add(new RelocateFile(dbName, newDataFilePath));  
    restore.RelocateFiles.Add(new RelocateFile(dbName + "_Log", newLogFilePath));  
    restore.SqlRestore(server);  
  
    // Restore transaction Log with stop at   
    Restore restoreLog = new Restore();  
    restoreLog.CredentialName = credentialName;  
    restoreLog.Database = dbName;  
    restoreLog.Action = RestoreActionType.Log;  
    restoreLog.Devices.AddDevice(urlBackupData, DeviceType.Url);  
    restoreLog.ToPointInTime = DateTime.Now.ToString();   
    restoreLog.SqlRestore(server);  
  
    ```  
  
3.  **PowerShell**  
  
    ```  
  
    #create variables  
    $backupUrlContainer = "https://mystorageaccount.blob.core.windows.net/mycontainer/"  
    $credentialName = "mycredential"  
    $srvPath = "SQLSERVER:\SQL\COMPUTERNAME\INSTANCENAME"  
    # for default instance, the $srvpath variable would be "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
  
    # Navigate to SQL Server Instance Directory  
  
    CD $srvPath   
  
    #create a unique file name for the full backup  
    $backupdbFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".bak"  
  
    # Full database backup to URL  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupdbFile  -SqlCredential $credentialName -CompressionOption On     
  
    #Create a unique file name for the tail log backup  
    $backuplogFile = $backupUrlContainer + "AdventureWorks2012_" + (Get-Date).ToString("s").Replace("-","_").Replace(":", "_").Replace(" ","_").Replace("/", "_") +  ".trn"  
  
    #Backup tail log to URL  
  
    Backup-SqlDatabase -Database AdventureWorks2012 -backupFile $backupFile  -SqlCredential $credentialName  -BackupAction Log -NoRecovery     
  
    # Restore Database and move files  
  
    $newDataFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile ("AdventureWorks_Data","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.mdf")  
    $newLogFilePath = New-Object Microsoft.SqlServer.Management.Smo.RelocateFile("AdventureWorks_Log","C:\Program Files\Microsoft SQL Server\myinstance\MSSQL\DATA\AdventureWorks2012.ldf")  
  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backupdbFile -RelocateFile @($newDataFilePath,$newLogFilePath) -NoRecovery    
  
    # Restore Transaction log with Stop At:  
    Restore-SqlDatabase -Database AdventureWorks2012 -SqlCredential $credentialName -BackupFile $backuplogFile  -ToPointInTime (Get-Date).ToString()  
  
    ```  
  
## <a name="see-also"></a>Ver también  
 [Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [Tutorial: SQL Server copias de seguridad y restauración en Azure Blob Storage Service](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
  
