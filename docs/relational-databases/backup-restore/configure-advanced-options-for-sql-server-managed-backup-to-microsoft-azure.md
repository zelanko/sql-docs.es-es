---
title: Configurar las opciones avanzadas de copia de seguridad administrada de SQL Server en Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b1f6ccfb9fdcf2fa3022864159fb87e589844df
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>Configurar las opciones avanzadas de copia de seguridad administrada de SQL Server en Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En el tutorial siguiente se describe cómo configurar las opciones avanzadas de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Estos procedimientos solo son necesarios si necesita las características que ofrecen. De lo contrario, puede habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y depender del comportamiento predeterminado.  
  
 En cada escenario, la copia de seguridad se especifica mediante el parámetro `database_name` . Cuando `database_name` es NULL o *, los cambios afectan a la configuración predeterminada en el nivel de instancia. La configuración del nivel de instancia afecta también a las nuevas bases de datos que se crean después del cambio.  
  
 Una vez especificada esta configuración, puede habilitar la copia de seguridad administrada para la base de datos o la instancia mediante el procedimiento almacenado del sistema [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Para obtener más información, consulte [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
> [!WARNING]  
>  Las opciones avanzadas y las opciones de programación personalizadas deben configurarse siempre antes de habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). De lo contrario, es posible que se produzcan operaciones de copia de seguridad no deseadas durante el período de tiempo comprendido entre la habilitación de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y la configuración de estos parámetros.  
  
## <a name="configure-encryption"></a>Configurar el cifrado  
 En los pasos siguientes se describe cómo especificar la configuración de cifrado mediante el procedimiento almacenado [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md).  
  
1.  **Determine el algoritmo de cifrado:** determine primero el nombre del algoritmo de cifrado que se usará. Seleccione uno de los algoritmos siguientes:  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **Cree una clave maestra de base de datos:** elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **Cree un certificado de copia de seguridad o una clave asimétrica:** con el cifrado puede usar tanto un certificado como una clave asimétrica. En el ejemplo siguiente se crea un certificado de copia de seguridad que se utilizará para el cifrado.  
  
    ```sql  
    USE Master;  
    GO  
       CREATE CERTIFICATE MyTestDBBackupEncryptCert  
          WITH SUBJECT = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
4.  **Configure el cifrado de la copia de seguridad administrada:** llame al procedimiento almacenado **managed_backup.sp_backup_config_advanced** con los valores correspondientes. Por ejemplo, en el ejemplo siguiente se configura la base de datos `MyDB` para el cifrado mediante un certificado denominado `MyTestDBBackupEncryptCert` y el algoritmo de cifrado `AES_128` .  
  
    ```  
    USE msdb;  
    GO  
       EXEC managed_backup.sp_backup_config_advanced  
          @database_name = 'MyDB'                
          ,@encryption_algorithm ='AES_128'  
          ,@encryptor_type = 'CERTIFICATE'  
          ,@encryptor_name = 'MyTestDBBackupEncryptCert';  
    GO  
    ```  
  
    > [!WARNING]  
    >  Si `@database_name` es NULL en el ejemplo anterior, la configuración se aplica a la instancia de SQL Server.  
  
## <a name="configure-a-custom-backup-schedule"></a>Configurar una programación de copia de seguridad personalizada  
 En los pasos siguientes se describe cómo establecer una programación personalizada con el procedimiento almacenado [managed_backup.sp_backup_config_schedule &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md).  
  
1.  **Determine la frecuencia de las copias de seguridad completas:** determine con qué frecuencia se realizarán copias de seguridad completas de la base de datos. Puede elegir entre copias de seguridad completas diarias y semanales.  
  
2.  **Determine la frecuencia de las copias de seguridad de registros:** determine con qué frecuencia se realizarán las copias de seguridad de registros. Este valor está en minutos u horas.  
  
3.  **Determine el día de la semana para las copias de seguridad semanales:** si la copia de seguridad es semanal, elija el día de la semana en que se realizará la copia de seguridad completa.  
  
4.  **Determine la hora de inicio de la copia de seguridad:** mediante la notación de 24 horas, elija una hora para iniciar la copia de seguridad.  
  
5.  **Determine la duración permitida para la copia de seguridad:** aquí se especifica la cantidad de tiempo que puede tardar una copia de seguridad en completarse.  
  
6.  **Configure la programación de copia de seguridad personalizada:** el siguiente procedimiento almacenado define una programación personalizada para la base de datos `MyDB` . Las copias de seguridad completas se realizan cada `Monday` a las `17:30`. Las copias de seguridad de registros se realizan cada `5` minutos. Las copias de seguridad tienen dos horas para completarse.  
  
    ```  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_backup_config_schedule   
         @database_name =  'MyDB'  
        ,@scheduling_option = 'Custom'  
        ,@full_backup_freq_type = 'Weekly'  
        ,@days_of_week = 'Monday'  
        ,@backup_begin_time =  '17:30'  
        ,@backup_duration = '02:00'  
        ,@log_backup_freq = '00:05'  
    GO  
  
    ```  
  
## <a name="next-steps"></a>Next Steps  
 Después de configurar las opciones avanzadas y las programaciones personalizadas, debe habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en la base de datos de destino o en la instancia de SQL Server. Para obtener más información, consulte [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Ver también  
 [Copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
