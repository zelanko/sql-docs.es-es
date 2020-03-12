---
title: Uso de una copia de seguridad administrada en Azure
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.description: Enable SQL Server managed backup to Azure
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e59dfd9c79090bc20a517367e0145303822d8079
ms.sourcegitcommit: e914effe771a1ee323bb3653626cd4ba83d77308
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2020
ms.locfileid: "78280892"
---
# <a name="enable-sql-server-managed-backup-to-azure"></a>Habilitación de la copia de seguridad administrada de SQL Server en Azure

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con la configuración predeterminada en el nivel de la base de datos y de la instancia. También se describe cómo habilitar las notificaciones de correo electrónico y cómo supervisar la actividad de copia de seguridad.  
  
 En este tutorial se usa Azure PowerShell. Antes de iniciar el tutorial, [descargue e instale Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).  
  
> [!IMPORTANT]  
>  Si también desea habilitar opciones avanzadas o usar una programación personalizada, configure las opciones antes de habilitar por primera vez [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Para obtener más información, consulte [Configurar las opciones avanzadas de copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="create-the-azure-blob-container"></a>Crear el Contenedor de blobs de Azure

El proceso requiere una cuenta de Azure. Si ya tiene una cuenta, vaya al paso siguiente. En caso contrario, puede comenzar a trabajar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/) o explorar las [opciones de compra](https://azure.microsoft.com/pricing/purchase-options/).

Para obtener más información sobre las cuentas de almacenamiento, consulte [Acerca de las cuentas de almacenamiento de Azure](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). 

#### <a name="azure-cli"></a>[CLI de Azure](#tab/azure-cli)

1. Inicie sesión en la cuenta de Azure.

    ```azurecli-interactive
    az login
    ```
  
1. Cree una cuenta de almacenamiento de Azure. si ya tiene una cuenta de almacenamiento, vaya al paso siguiente. El comando siguiente crea una cuenta de almacenamiento denominada `<backupStorage>` en la región Este de EE. UU.  
  
    ```azurecli-interactive
    az storage account create -n <backupStorage> -l "eastus" --resource-group <resourceGroup>
    ```  
    
1. Cree un contenedor de blobs denominado `<backupContainer>` para los archivos de copia de seguridad.
  
    ```azurecli-interactive
    $keys = az storage account keys list --account-name <backupStorage> --resource-group <resourceGroup> | ConvertFrom-Json
    az storage container create --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value 
    ```  
  
1. Genere una firma de acceso compartido (SAS) para acceder al contenedor. El comando siguiente crea un token de SAS para el contenedor de blobs `<backupContainer>` que expira en un año.  
  
    ```azurecli-interactive 
    az storage container generate-sas --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value
    ```

#### <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

1. Con el comando siguiente inicia sesión en la cuenta de Azure.

    ```azurepowershell-interactive
    Connect-AzAccount
    Set-AzContext -SubscriptionId "<subscriptionId>"
    ```
  
1. Cree una cuenta de almacenamiento de Azure. si ya tiene una cuenta de almacenamiento, vaya al paso siguiente. El comando siguiente crea una cuenta de almacenamiento denominada `<backupStorage>` en la región Este de EE. UU.  
  
    ```azurepowershell-interactive
    New-AzStorageAccount -StorageAccountName <backupStorage> -Location "EAST US" -ResourceGroupName <resourceGroup> -SkuName Standard_GRS
    ```   
  
1. Cree un contenedor de blobs denominado `<backupContainer>` para los archivos de copia de seguridad.  
  
    ```azurepowershell-interactive
    $context = New-AzStorageContext -StorageAccountName <backupStorage> -StorageAccountKey (Get-AzStorageAccountKey -Name <backupStorage> -ResourceGroupName <resourceGroup>).Value[0]  
    New-AzStorageContainer -Name <backupContainer> -Context $context  
    ```  
  
1. Genere una firma de acceso compartido (SAS) para acceder al contenedor. El comando siguiente crea un token de SAS para el contenedor de blobs `<backupContainer>` que expira en un año.
  
    ```azurepowershell-interactive 
    New-AzStorageContainerSASToken -Name <backupContainer> -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context 
    ```

* * *

> [!NOTE]
> Estos pasos también se pueden realizar mediante [Azure Portal](https://portal.azure.com/).

La salida contendrá la dirección URL del contenedor o el token de SAS. A continuación se muestra un ejemplo:  
  
  `https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl`
  
Si se incluye la dirección URL, sepárela del token de SAS en el signo de interrogación (no incluya el signo de interrogación). Por ejemplo, la salida anterior tendría como resultado los dos valores siguientes.  
  
|||  
|-|-|  
|**Dirección URL del contenedor**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
|**Token de SAS**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
|||
  
Anote la dirección URL del contenedor y la SAS para usarlos al crear una credencial de SQL. Para más información sobre SAS, consulte [Uso de firmas de acceso compartido, parte 1: Descripción del modelo SAS](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/).  
  
## <a name="enable-managed-backup-to-azure"></a>Habilitación de la copia de seguridad administrada en Azure
  
1.  **Cree una credencial de SQL para la dirección URL de SAS:** use el token de SAS para crear una credencial de SQL para la dirección URL del contenedor de blobs. En SQL Server Management Studio, use la siguiente consulta de Transact-SQL para crear la credencial para la dirección URL del contenedor de blobs según el ejemplo siguiente:  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **Asegúrese de que el servicio del Agente SQL Server está iniciado y en ejecutándose:** inicie el Agente SQL Server si no se está ejecutando actualmente.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requiere que el Agente SQL Server se ejecute en la instancia para realizar operaciones de copia de seguridad.  Puede ser conveniente configurar el Agente SQL Server para que se ejecute automáticamente con el fin de asegurarse de que las operaciones de copia de seguridad pueden realizarse periódicamente.  
  
3.  **Determine el período de retención:** Determine el período de retención para los archivos de copia de seguridad. El período de retención se especifica en días y puede abarcar de 1 a 30.  
  
4.  **Habilitar y configurar[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  inicie SQL Server Management Studio y conéctese a la instancia de SQL Server de destino. En la ventana de consulta, ejecute la siguiente instrucción después de modificar los valores correspondientes al nombre de la base de datos, la dirección URL del contenedor y el período de retención según sus requisitos:  
  
    > [!IMPORTANT]  
    >  Para habilitar la copia de seguridad administrada en el nivel de instancia, especifique `NULL` para el parámetro `database_name` .  
  
    ```sql  
    USE msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada ahora en la base de datos especificada. Puede tardarse hasta 15 minutos en que las operaciones de copia de seguridad de la base de datos empiecen a ejecutarse.  
  
5.  **Revise la configuración predeterminada del evento extendido:** Revise la configuración de eventos extendidos ejecutando la siguiente instrucción transact-SQL.  
  
    ```sql
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     Debe ver que los eventos de canal Administración, Operativo y Analítico están habilitados de forma predeterminada y no se pueden deshabilitar. Debe ser suficiente supervisar los eventos que requieren intervención manual.  Puede habilitar los eventos de depuración, pero los canales de depuración incluyen eventos informativos y de depuración que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa para detectar problemas y solucionarlos.  
  
6.  **Habilite y configure la notificación del estado de mantenimiento:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tiene un procedimiento almacenado que crea un trabajo del agente para enviar notificaciones por correo electrónico de los errores o las advertencias que puedan requerir atención. En los pasos siguientes se describe el proceso para habilitar y configurar las notificaciones por correo electrónico:  
  
    1.  Configure Correo electrónico de base de datos si aún no está habilitado en la instancia. Para obtener más información, vea [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md).  
  
    2.  Configure la notificación del Agente SQL Server para que use Correo electrónico de base de datos. Para más información, consulte [Configurar el Agente SQL Server para que use el Correo electrónico de base de datos](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilite las notificaciones por correo electrónico para recibir advertencias y errores de copia de seguridad:** En la ventana de consulta, ejecute las siguientes instrucciones Transact-SQL:  
  
        ```sql
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
        ```  
  
7.  **Vea archivos de copia de seguridad en la cuenta de Azure Storage:** conéctese a la cuenta de almacenamiento desde SQL Server Management Studio o Azure Portal. Verá los archivos de copia de seguridad del contenedor especificado. Tenga en cuenta que podría ver una base de datos y una copia de seguridad de registros antes de que transcurran 5 minutos desde la habilitación de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la base de datos.  
  
8.  **Supervise el estado de mantenimiento:**  puede supervisar a través de notificaciones por correo electrónico que ha configurado previamente, o bien supervisar los eventos registrados de forma activa. Las siguientes son algunas instrucciones de Transact-SQL de ejemplo que se utilizan para ver los eventos:  
  
    ```sql  
    --  view all admin events  
    USE msdb;  
    GO  
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
  
    ```sql  
    -- to enable debug events  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
    ```sql  
    --  View all events in the current week  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
    ```
  
Los pasos descritos en esta sección son específicos para configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez en la base de datos. Puede modificar las configuraciones existentes usando los mismos procedimientos almacenados del sistema y proporcionar los nuevos valores.  
  
## <a name="see-also"></a>Consulte también  
 [Copia de seguridad administrada de SQL Server en Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
