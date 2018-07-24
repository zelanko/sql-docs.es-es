---
title: Habilitar la copia de seguridad administrada de SQL Server en Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 10/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d0b9b90aa7ca04cb7b1cbedde2befae373339bab
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984047"
---
# <a name="enable-sql-server-managed-backup-to-microsoft-azure"></a>Habilitar la copia de seguridad administrada de SQL Server en Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con la configuración predeterminada en el nivel de la base de datos y de la instancia. También se describe cómo habilitar las notificaciones de correo electrónico y cómo supervisar la actividad de copia de seguridad.  
  
 En este tutorial se usa Azure PowerShell. Antes de iniciar el tutorial, [descargue e instale Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!IMPORTANT]  
>  Si también desea habilitar opciones avanzadas o usar una programación personalizada, configure las opciones antes de habilitar por primera vez [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Para obtener más información, consulte [Configure Advanced Options for SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="enable-and-configure-includesssmartbackupincludesss-smartbackup-mdmd-with-default-settings"></a>Habilitar y configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con valores predeterminados  
  
#### <a name="create-the-azure-blob-container"></a>Crear el Contenedor de blobs de Azure  
  
1.  **Suscríbase a Azure:** si ya tiene una suscripción de Azure, vaya al paso siguiente. En caso contrario, puede comenzar a trabajar con una [evaluación gratuita](http://azure.microsoft.com/pricing/free-trial/) o explorar las [opciones de compra](http://azure.microsoft.com/pricing/purchase-options/).  
  
2.  **Cree una cuenta de Almacenamiento de Azure:** si ya tiene una cuenta de almacenamiento, vaya al paso siguiente. En caso contrario, puede usar el [Portal de administración de Azure](https://manage.windowsazure.com/) o Azure PowerShell para crear la cuenta de almacenamiento. El siguiente comando `New-AzureStorageAccount` crea una cuenta de almacenamiento denominada `managedbackupstorage` en la región este de EE. UU.  
  
    ```powershell  
    New-AzureStorageAccount -StorageAccountName "managedbackupstorage" -Location "EAST US"  
    ```  
  
     Para obtener más información sobre las cuentas de almacenamiento, consulte [Acerca de las cuentas de almacenamiento de Azure](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/).  
  
3.  **Cree un contenedor de blobs para los archivos de copia de seguridad:** puede crear un contenedor de blobs en el Portal de administración de Azure o con Azure PowerShell. El siguiente comando `New-AzureStorageContainer` crea un contenedor de blobs denominado `backupcontainer` en la cuenta de almacenamiento `managedbackupstorage` .  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary  
    New-AzureStorageContainer -Name backupcontainer -Context $context  
    ```  
  
4.  **Genere una firma de acceso compartido (SAS):** para acceder al contenedor, debe crear una SAS. Puede hacerlo en algunas herramientas, código y Azure PowerShell. El siguiente comando `New-AzureStorageContainerSASToken` crea un token de SAS para el contenedor de blobs `backupcontainer` que expira en un año.  
  
    ```powershell  
    $context = New-AzureStorageContext -StorageAccountName managedbackupstorage -StorageAccountKey (Get-AzureStorageKey -StorageAccountName managedbackupstorage).Primary   
    New-AzureStorageContainerSASToken -Name backupcontainer -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context  
    ```  
  
     La salida de este comando contendrá la dirección URL del contenedor y el token de SAS. A continuación se muestra un ejemplo:  
  
    ```  
    https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl  
    ```  
  
     En el ejemplo anterior, separe la dirección URL del contenedor y el token de SAS en el signo de interrogación (no incluya el signo de interrogación). Por ejemplo, la salida anterior tendría como resultado los dos valores siguientes.  
  
    |||  
    |-|-|  
    |**Dirección URL del contenedor:**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
    |**Token de SAS:**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
  
     Anote la dirección URL del contenedor y la SAS para usarlos al crear una credencial de SQL. Para obtener más información sobre SAS, consulte [Firmas de acceso compartido, Parte 1: Descripción del modelo SAS](http://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/).  
  
#### <a name="enable-includesssmartbackupincludesss-smartbackup-mdmd"></a>Habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
1.  **Cree una credencial de SQL para la URL de SAS:** use el token de SAS para crear una credencial de SQL para la dirección URL del contenedor de blobs. En SQL Server Management Studio, use la siguiente consulta de Transact-SQL para crear la credencial para la dirección URL del contenedor de blobs según el ejemplo siguiente:  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **Asegúrese de que el servicio del Agente SQL Server se haya iniciado y esté ejecutándose:** inicie el Agente SQL Server, si no se está ejecutando.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requiere que el Agente SQL Server se ejecute en la instancia para realizar operaciones de copia de seguridad.  Puede ser conveniente configurar el Agente SQL Server para que se ejecute automáticamente con el fin de asegurarse de que las operaciones de copia de seguridad pueden realizarse periódicamente.  
  
3.  **Determinar el período de retención:** determine el período de retención para los archivos de copia de seguridad. El período de retención se especifica en días y puede abarcar de 1 a 30.  
  
4.  **Enable and configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :** inicie SQL Server Management Studio y conéctese a la instancia de SQL Server de destino. En la ventana de consulta, ejecute la siguiente instrucción después de modificar los valores correspondientes al nombre de la base de datos, la dirección URL del contenedor y el período de retención según sus requisitos:  
  
    > [!IMPORTANT]  
    >  Para habilitar la copia de seguridad administrada en el nivel de instancia, especifique `NULL` para el parámetro `database_name` .  
  
    ```sql  
    Use msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada ahora en la base de datos especificada. Puede tardarse hasta 15 minutos en que las operaciones de copia de seguridad de la base de datos empiecen a ejecutarse.  
  
5.  **Revise la configuración predeterminada de los eventos extendidos:** revise la configuración de eventos extendidos ejecutando la siguiente instrucción de Transact-SQL.  
  
    ```  
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Debe ver que los eventos de canal Administración, Operativo y Analítico están habilitados de forma predeterminada y no se pueden deshabilitar. Debe ser suficiente supervisar los eventos que requieren intervención manual.  Puede habilitar los eventos de depuración, pero los canales de depuración incluyen eventos informativos y de depuración que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa para detectar problemas y solucionarlos.  
  
6.  **Habilite y configure la notificación del estado de mantenimiento:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tiene un procedimiento almacenado que crea un trabajo del agente para enviar notificaciones por correo electrónico de los errores o las advertencias que puedan requerir atención. En los pasos siguientes se describe el proceso para habilitar y configurar las notificaciones por correo electrónico:  
  
    1.  Configure Correo electrónico de base de datos si aún no está habilitado en la instancia. Para obtener más información, vea [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configure la notificación del Agente SQL Server para que use Correo electrónico de base de datos. Para obtener más información, consulte [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilite las notificaciones por correo electrónico para recibir los errores y advertencias de copia de seguridad:** en la ventana de consulta, ejecute las siguientes instrucciones Transact-SQL:  
  
        ```  
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
7.  **Consulte los archivos de copia de seguridad en la cuenta de Almacenamiento de Microsoft Azure:** conéctese a la cuenta de almacenamiento desde SQL Server Management Studio o desde el Portal de administración de Azure. Verá los archivos de copia de seguridad del contenedor especificado. Tenga en cuenta que podría ver una base de datos y una copia de seguridad de registros antes de que transcurran 5 minutos desde la habilitación de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la base de datos.  
  
8.  **Supervise el estado de mantenimiento:**  puede supervisar a través de notificaciones por correo electrónico que configuró previamente o supervisar los eventos registrados de forma activa. Las siguientes son algunas instrucciones de Transact-SQL de ejemplo que se utilizan para ver los eventos:  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 Los pasos descritos en esta sección son específicos para configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez en la base de datos. Puede modificar las configuraciones existentes usando los mismos procedimientos almacenados del sistema y proporcionar los nuevos valores.  
  
## <a name="see-also"></a>Ver también  
 [Copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
