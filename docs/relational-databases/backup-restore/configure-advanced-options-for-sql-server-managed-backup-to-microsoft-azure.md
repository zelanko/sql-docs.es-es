---
title: 'Copia de seguridad administrada: configuración de opciones avanzadas'
description: En este tutorial se describe cómo establecer las opciones avanzadas de la copia de seguridad administrada de SQL Server para Microsoft Azure, en caso de que las opciones predeterminadas no se ajusten a sus necesidades.
titleSuffix: to Microsoft Azure
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.managedbackup.configure.f1
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.assetid: ffd28159-8de8-4d40-87da-1586bfef3315
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: 95bf7a69d525721c1610b989cc142d9ab754a7ee
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358910"
---
# <a name="configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure"></a>Configuración de las opciones avanzadas de copia de seguridad administrada de SQL Server en Microsoft Azure
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  En el tutorial siguiente se describe cómo configurar las opciones avanzadas de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Estos procedimientos solo son necesarios si necesita las características que ofrecen. De lo contrario, puede habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y depender del comportamiento predeterminado.  
  
 En cada escenario, la copia de seguridad se especifica mediante el parámetro `database_name` . Cuando `database_name` es NULL o *, los cambios afectan a la configuración predeterminada en el nivel de instancia. La configuración del nivel de instancia afecta también a las nuevas bases de datos que se crean después del cambio.  
  
 Una vez especificada esta configuración, puede habilitar la copia de seguridad administrada para la base de datos o la instancia mediante el procedimiento almacenado del sistema [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). Para obtener más información, consulte [Habilitación de la copia de seguridad administrada de SQL Server en Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
> [!WARNING]  
>  Las opciones avanzadas y las opciones de programación personalizadas deben configurarse siempre antes de habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). De lo contrario, es posible que se produzcan operaciones de copia de seguridad no deseadas durante el período de tiempo comprendido entre la habilitación de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] y la configuración de estos parámetros.  
  
## <a name="configure-encryption"></a>Configurar el cifrado  
 En los pasos siguientes se describe cómo especificar la configuración de cifrado mediante el procedimiento almacenado [managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md).  

1.  **Determine el algoritmo de cifrado:** Determine primero el nombre del algoritmo de cifrado que se utiliza. Seleccione uno de los algoritmos siguientes:  
  
    -   AES_128  
  
    -   AES_192  
  
    -   AES_256  
  
    -   TRIPLE_DES_3KEY  
  
    -   NO_ENCRYPTION  
  
2.  **Cree la clave maestra de una base de datos:** Elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
       CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
    ```  
  
3.  **Cree un certificado de copia de seguridad o clave asimétrica:** con el cifrado puede usar tanto un certificado como una clave asimétrica. En el ejemplo siguiente se crea un certificado de copia de seguridad que se utilizará para el cifrado.  
  
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
 En los pasos siguientes se describe cómo establecer una programación personalizada con el procedimiento almacenado [managed_backup.sp_backup_config_schedule & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md).  
  
1.  **Determine la frecuencia de las copias de seguridad completas:** determine qué frecuencia se realizarán copias de seguridad completas de la base de datos. Puede elegir entre copias de seguridad completas diarias y semanales.  
  
2.  **Determine la frecuencia de las copias de seguridad de registros:** determine con qué frecuencia se realizará una copia de seguridad de registros. Este valor está en minutos u horas.  
  
3.  **Determine el día de la semana para las copias de seguridad semanales:** si la copia de seguridad es semanal, elija el día de la semana para hacer la copia de seguridad completa.  
  
4.  **Determine la hora de inicio de la copia de seguridad:** mediante la notación de 24 horas, elija una hora para iniciar la copia de seguridad.  
  
5.  **Determine el tiempo para permitir la copia de seguridad:** especifique el tiempo en que una copia de seguridad tiene que completarse.  
  
6.  **Configure la programación de copia de seguridad personalizada:** el siguiente procedimiento almacenado define una programación personalizada para la base de datos `MyDB`. Las copias de seguridad completas se realizan cada `Monday` a las `17:30`. Las copias de seguridad de registros se realizan cada `5` minutos. Las copias de seguridad tienen dos horas para completarse.  
  
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
  
## <a name="next-steps"></a>Pasos siguientes  
 Después de configurar las opciones avanzadas y las programaciones personalizadas, debe habilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en la base de datos de destino o en la instancia de SQL Server. Para obtener más información, consulte [Enable SQL Server Managed Backup to Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md).  
  
## <a name="see-also"></a>Consulte también  
 [Copia de seguridad administrada en Microsoft Azure para SQL Server](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
