---
title: Configuración de SQL Server copia de seguridad administrada en Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b69439226b55965e37f24f2131c77340ae833590
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154721"
---
# <a name="setting-up-sql-server-managed-backup-to-azure"></a>Configuración de SQL Server copia de seguridad administrada en Azure
  Este tema incluye dos tutoriales:  
  
 Configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en el nivel de base de datos, habilitar la notificación por correo electrónico y supervisar la actividad de copia de seguridad.  
  
 Configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en el nivel de instancia, habilitar la notificación por correo electrónico y supervisar la actividad de copia de seguridad.  
  
 Para ver un tutorial sobre la [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] configuración de grupos de disponibilidad, consulte [configuración de SQL Server copia de seguridad administrada en Microsoft Azure para grupos de disponibilidad](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md).  
  
## <a name="setting-up-includess_smartbackupincludesss-smartbackup-mdmd"></a>Configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
  
### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-a-database"></a>Habilitar y configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos  
 En este tutorial se describen los pasos necesarios para habilitar y configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos (TestDB), además de los pasos para habilitar la supervisión del estado de mantenimiento de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 **Permisos:**  
  
-   Requiere la pertenencia al rol de base de datos **db_backupoperator** , con permisos `EXECUTE` **ALTER any Credential** y permisos en el procedimiento almacenado **sp_delete_backuphistory**.  
  
-   Requiere permisos **Select** en la función **smart_admin. fn_get_current_xevent_settings**.  
  
-   Requiere `EXECUTE` permisos en el procedimiento almacenado **smart_admin. sp_get_backup_diagnostics** . Además, requiere permisos `VIEW SERVER STATE` ya que internamente llama a otros objetos del sistema que requieren este permiso.  
  
-   Requiere `EXECUTE` permisos en los `smart_admin.sp_set_instance_backup` procedimientos `smart_admin.sp_backup_master_switch` almacenados y.  


1.  **Cree una cuenta de almacenamiento de Microsoft Azure:** Las copias de seguridad se almacenan en el servicio de almacenamiento de Microsoft Azure. En primer lugar, debe crear una cuenta de almacenamiento de Microsoft Azure, si aún no tiene una cuenta.
    - SQL Server 2014 usa blobs en páginas, que son diferentes de los blobs en bloques y anexos. Por lo tanto, debe crear una cuenta de uso general y no una cuenta de BLOB. Para obtener más información, consulte [acerca de las cuentas de Azure Storage](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/).
    - Anote el nombre de la cuenta de almacenamiento y las claves de acceso. La información del nombre de cuenta y de la clave de acceso se utiliza para crear una credencial SQL. La credencial SQL se usa para autenticarse en la cuenta de almacenamiento.  
 
2.  **Cree una credencial de SQL:** Cree una credencial de SQL con el nombre de la cuenta de almacenamiento como identidad y la clave de acceso de almacenamiento como contraseña.  
  
3.  **Asegúrese de que el servicio del Agente SQL Server está iniciado y en ejecutándose:**  inicie el Agente SQL Server si no se está ejecutando actualmente.  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requiere que el Agente SQL Server se ejecute en la instancia para realizar operaciones de copia de seguridad.  Puede ser conveniente configurar el Agente SQL Server para que se ejecute automáticamente con el fin de asegurarse de que las operaciones de copia de seguridad pueden realizarse periódicamente.  
  
4.  **Determine el período de retención:** Determine el período de retención para los archivos de copia de seguridad. El período de retención se especifica en días y puede abarcar de 1 a 30.  
  
5.  **Habilitar y configurar[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  Inicie SQL Server Management Studio y conéctese a la instancia donde está instalada la base de datos. En la ventana de consulta, ejecute la siguiente instrucción después de modificar los valores correspondientes al nombre de la base de datos, la credencial SQL, el período de retención y las opciones de cifrado según sus requisitos:  
  
     Para obtener más información sobre la creación de un certificado para el cifrado, vea el paso **crear un certificado de copia** de seguridad en [creación de una copia de seguridad cifrada](create-an-encrypted-backup.md).  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada ahora en la base de datos especificada. Puede tardarse hasta 15 minutos en que las operaciones de copia de seguridad de la base de datos empiecen a ejecutarse.  
  
6.  **Revise la configuración predeterminada del evento extendido:** Revise la configuración de eventos extendidos ejecutando la siguiente instrucción transact-SQL.  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     Debe ver que los eventos de canal Administración, Operativo y Analítico están habilitados de forma predeterminada y no se pueden deshabilitar. Debe ser suficiente supervisar los eventos que requieren intervención manual.  Puede habilitar los eventos de depuración, pero los canales de depuración incluyen eventos informativos y de depuración que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] usa para detectar problemas y solucionarlos. Para obtener más información, vea [supervisar SQL Server copia de seguridad administrada en Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
7.  **Habilite y configure la notificación del estado de mantenimiento:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tiene un procedimiento almacenado que crea un trabajo del agente para enviar notificaciones por correo electrónico de los errores o las advertencias que puedan requerir atención. En los pasos siguientes se describe el proceso para habilitar y configurar las notificaciones por correo electrónico:  
  
    1.  Configure Correo electrónico de base de datos si aún no está habilitado en la instancia. Para obtener más información, vea [Configure Database Mail](../database-mail/configure-database-mail.md).  
  
    2.  Configure la notificación del Agente SQL Server para que use Correo electrónico de base de datos. Para más información, consulte [Configurar el Agente SQL Server para que use el Correo electrónico de base de datos](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilite las notificaciones por correo electrónico para recibir advertencias y errores de copia de seguridad:** En la ventana de consulta, ejecute las siguientes instrucciones Transact-SQL:  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
         Para obtener más información y un script de ejemplo completo, vea [Monitor SQL Server copia de seguridad administrada en Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
8.  **Vea archivos de copia de seguridad en la cuenta de Microsoft Azure Storage:** Conéctese a la cuenta de almacenamiento desde SQL Server Management Studio o el Portal de administración de Azure. Verá un contenedor para la instancia de SQL Server que hospeda la base de datos que configuró para utilizar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. También puede ver una base de datos y una copia de seguridad de registros antes de 15 minutos después de habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la base de datos.  
  
9. **Supervise el estado de mantenimiento:**  puede supervisar a través de notificaciones por correo electrónico que ha configurado previamente, o bien supervisar los eventos registrados de forma activa. Las siguientes son algunas instrucciones de Transact-SQL de ejemplo que se utilizan para ver los eventos:  
  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 Los pasos descritos en esta sección son específicos para configurar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] por primera vez en la base de datos. Puede modificar las configuraciones existentes mediante el mismo procedimiento almacenado del sistema **smart_admin. sp_set_db_backup** y proporcionar los nuevos valores. Para obtener más información, vea [SQL Server la copia de seguridad administrada en la configuración de retención y almacenamiento de Microsoft Azure](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
### <a name="enable-includess_smartbackupincludesss-smartbackup-mdmd-for-the-instance-with-default-settings"></a>Habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la instancia con la configuración predeterminada  
 En este tutorial se describen los pasos para habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y configurar para la instancia de, ' instanceof\\',. Incluye pasos para habilitar la supervisión del estado de mantenimiento de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
 **Permisos:**  
  
-   Requiere la pertenencia al rol de base de datos **db_backupoperator** , con permisos `EXECUTE` **ALTER any Credential** y permisos en el procedimiento almacenado **sp_delete_backuphistory**.  
  
-   Requiere permisos **Select** en la función **smart_admin. fn_get_current_xevent_settings**.  
  
-   Requiere `EXECUTE` permisos en el procedimiento almacenado **smart_admin. sp_get_backup_diagnostics** . Además, requiere permisos `VIEW SERVER STATE` ya que internamente llama a otros objetos del sistema que requieren este permiso.  


1.  **Cree una cuenta de almacenamiento de Microsoft Azure:** Las copias de seguridad se almacenan en el servicio de almacenamiento de Microsoft Azure. En primer lugar, debe crear una cuenta de almacenamiento de Microsoft Azure, si aún no tiene una cuenta.
    - SQL Server 2014 usa blobs en páginas, que son diferentes de los blobs en bloques y anexos. Por lo tanto, debe crear una cuenta de uso general y no una cuenta de BLOB. Para obtener más información, consulte [acerca de las cuentas de Azure Storage](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/).
    - Anote el nombre de la cuenta de almacenamiento y las claves de acceso. La información del nombre de cuenta y de la clave de acceso se utiliza para crear una credencial SQL. La credencial SQL se usa para autenticarse en la cuenta de almacenamiento.  
  
2.  **Cree una credencial de SQL:** Cree una credencial de SQL con el nombre de la cuenta de almacenamiento como identidad y la clave de acceso de almacenamiento como contraseña.  
  
3.  **Asegúrese de que el servicio del Agente SQL Server está iniciado y en ejecutándose:** inicie el Agente SQL Server si no se está ejecutando actualmente. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] requiere que el Agente SQL Server se ejecute en la instancia para realizar operaciones de copia de seguridad.  Puede ser conveniente configurar el Agente SQL Server para que se ejecute automáticamente con el fin de asegurarse de que las operaciones de copia de seguridad pueden realizarse periódicamente.  
  
4.  **Determine el período de retención:** Determine el período de retención para los archivos de copia de seguridad. El período de retención se especifica en días y puede abarcar de 1 a 30. Una vez que [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] esté habilitada en el nivel de instancia con los valores predeterminados, todas las nuevas bases de datos creadas posteriormente heredarán los valores. Solo se admiten y se configurarán automáticamente las bases de datos configuradas para los modelos de recuperación completo u optimizado para cargas masivas de registro. Puede deshabilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos específica en cualquier momento si no desea que se configure [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. También puede cambiar la configuración de una base de datos específica configurando [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en el nivel de base de datos.  
  
5.  **Habilitar y configurar[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  Inicie SQL Server Management Studio y conéctese a la instancia de SQL Server. En la ventana de consulta, ejecute la siguiente instrucción después de modificar los valores correspondientes al nombre de la base de datos, la credencial SQL, el período de retención y las opciones de cifrado según sus requisitos:  
  
     Para obtener más información sobre la creación de un certificado para el cifrado, vea el paso **crear un certificado de copia** de seguridad en [creación de una copia de seguridad cifrada](create-an-encrypted-backup.md).  
  
    ```  
    Use msdb;  
    Go  
       EXEC smart_admin.sp_set_instance_backup  
                     @enable_backup=1  
                    ,@retention_days=30   
                    ,@credential_name='sqlbackuptoURL'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert';  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está habilitada ahora en la instancia.  
  
6.  Comprobar la configuración ejecutando la siguiente instrucción Transact-SQL:  
  
    ```  
    Use msdb;  
    GO  
    SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
    ```  
  
7.  Crear una nueva base de datos en la instancia. Ejecute la siguiente instrucción Transact-SQL para ver la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para la base de datos:  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('NewDB')  
    ```  
  
     Puede tardarse hasta 15 minutos en mostrarse la configuración y en que las operaciones de copia de seguridad de la base de datos empiecen a ejecutarse.  
  
8.  **Habilite y configure la notificación del estado de mantenimiento:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] tiene un procedimiento almacenado que crea un trabajo del agente para enviar notificaciones por correo electrónico de los errores o las advertencias que puedan requerir atención.  Para recibir dichas notificaciones, debe habilitar el procedimiento almacenado que crea un trabajo del Agente SQL Server. En los pasos siguientes se describe el proceso para habilitar y configurar las notificaciones por correo electrónico:  
  
    1.  Configure Correo electrónico de base de datos si aún no está habilitado en la instancia. Para obtener más información, vea [Configure Database Mail](../database-mail/configure-database-mail.md).  
  
    2.  Configure la notificación del Agente SQL Server para que use Correo electrónico de base de datos. Para más información, consulte [Configurar el Agente SQL Server para que use el Correo electrónico de base de datos](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md).  
  
    3.  **Habilite las notificaciones por correo electrónico para recibir advertencias y errores de copia de seguridad:** En la ventana de consulta, ejecute las siguientes instrucciones Transact-SQL:  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email address>'  
  
        ```  
  
         Para obtener más información acerca de cómo supervisar y un script de ejemplo completo, vea [monitor SQL Server copia de seguridad administrada en Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md).  
  
9. **Vea archivos de copia de seguridad en la cuenta de Microsoft Azure Storage:** Conéctese a la cuenta de almacenamiento desde SQL Server Management Studio o el Portal de administración de Azure. Verá un contenedor para la instancia de SQL Server que hospeda la base de datos que configuró para utilizar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. También puede ver una base de datos y una copia de seguridad de registros antes de 15 minutos después de crear una nueva base de datos.  
  
10. **Supervise el estado de mantenimiento:**  puede supervisar a través de notificaciones por correo electrónico que ha configurado previamente, o bien supervisar los eventos registrados de forma activa. Las siguientes son algunas instrucciones de Transact-SQL de ejemplo que se utilizan para ver los eventos:  
  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 La configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se puede invalidar en una base de datos específica configurando los valores específicamente en el nivel de base de datos. También puede pausar y reanudar el servicio de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de forma temporal. Para obtener más información, vea [SQL Server copia de seguridad administrada en Microsoft Azure-configuración de retención y almacenamiento](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md) .  
  
  
