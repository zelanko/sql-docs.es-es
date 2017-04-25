---
title: Deshabilitar la copia de seguridad administrada de SQL Server en Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3e02187f-363f-4e69-a82f-583953592544
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: caf1e311db9cc0844294417dfd06e4a384265a4b
ms.lasthandoff: 04/11/2017

---
# <a name="disable-sql-server-managed-backup-to-microsoft-azure"></a>Deshabilitar la copia de seguridad administrada de SQL Server en Microsoft Azure
  En este tema se explica cómo deshabilitar o pausar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en el nivel de la base de datos y de la instancia.  
  
##  <a name="DatabaseDisable"></a> Deshabilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos  
 Puede deshabilitar la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] mediante el procedimiento almacenado del sistema [managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md). El parámetro *@enable_backup* se usa para habilitar y deshabilitar las configuraciones de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de una base de datos específica, donde 1 habilita y 0 deshabilita los valores de configuración.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-a-specific-database"></a>Para deshabilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para una base de datos específica:  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
```  
EXEC msdb.managed_backup.sp_backup_config_basic  
                @database_name = 'TestDB'   
                ,@enable_backup = 0;  
GO  
  
```  
  
##  <a name="DatabaseAllDisable"></a> Deshabilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para todas las bases de datos de la instancia  
 El siguiente procedimiento es válido cuando se desea deshabilitar la configuración de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de todas las bases de datos que tienen habilitado [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en la instancia.  Las opciones de configuración como la dirección URL de almacenamiento, la retención y la credencial de SQL permanecerán en los metadatos y se pueden usar si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se habilita posteriormente para la base de datos. Si solo quiere pausar los servicios de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] temporalmente, puede usar el modificador principal que se explica en las siguientes secciones de este tema.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-for-all-the-databases"></a>Para deshabilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] para todas las bases de datos:  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo siguiente identifica si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está configurado en el nivel de instancia y en todas las bases de datos habilitadas para [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en la instancia, y ejecuta el procedimiento almacenado del sistema **sp_backup_config_basic** para deshabilitar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)].  
  
```  
-- Create a working table to store the database names  
Declare @DBNames TABLE  
  
       (  
             RowID int IDENTITY PRIMARY KEY  
             ,DBName varchar(500)  
  
       )  
-- Define the variables  
DECLARE @rowid int  
DECLARE @dbname varchar(500)  
DECLARE @SQL varchar(2000)  
-- Get the database names from the system function  
  
INSERT INTO @DBNames (DBName)  
  
SELECT db_name  
       FROM   
  
       msdb.managed_backup.fn_backup_db_config (NULL)  
       WHERE is_managed_backup_enabled = 1  
  
       --Select DBName from @DBNames  
  
       select @rowid = min(RowID)  
       FROM @DBNames  
  
       WHILE @rowID IS NOT NULL  
       Begin  
  
             Set @dbname = (Select DBName From @DBNames Where RowID = @rowid)  
             Begin  
             Set @SQL = 'EXEC msdb.managed_backup.sp_backup_config_basic    
                @database_name= '''+'' + @dbname+ ''+''',   
                @enable_backup=0'  
  
            EXECUTE (@SQL)  
  
             END  
             Select @rowid = min(RowID)  
             From @DBNames Where RowID > @rowid  
  
       END  
```  
  
 Para revisar la configuración predeterminada de todas las bases de datos en la instancia, utilice la siguiente consulta:  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL);  
GO  
  
```  
  
##  <a name="InstanceDisable"></a> Deshabilitar la configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] de la instancia  
 La configuración predeterminada en el nivel de instancia se aplica a todas las nuevas bases de datos creadas en esa instancia.  Si ya no necesita la configuración predeterminada, puede deshabilitarla mediante el procedimiento almacenado del sistema **managed_backup.sp_backup_config_basic** con el parámetro *@database_name* establecido en NULL. Al deshabilitarla, no se quita las otras opciones de configuración como la dirección URL de almacenamiento, el valor de retención o el nombre de la credencial de SQL. Estas opciones se utilizarán si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] se habilita para la instancia posteriormente.  
  
#### <a name="to-disable-includesssmartbackupincludesss-smartbackup-mdmd-default-configuration-settings"></a>Para deshabilitar la configuración predeterminada de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] :  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    EXEC msdb.managed_backup.sp_backup_config_basic  
                    @database_name = 'TestDB'   
                    ,@enable_backup = 0;  
    GO  
  
    ```  
  
##  <a name="InstancePause"></a> Pause [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en el nivel de instancia  
 Puede haber ocasiones en que deba detener temporalmente los servicios de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] durante un breve período.  El procedimiento almacenado del sistema **managed_backup.sp_backup_master_switch** permite deshabilitar el servicio de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] en el nivel de instancia.  El mismo procedimiento almacenado se utiliza para reanudar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. El parámetro @state se utiliza para definir si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] debe desactivarse o activarse.  
  
#### <a name="to-pause-includesssmartbackupincludesss-smartbackup-mdmd-services-using-transact-sql"></a>Para pausar los servicios de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con Transact-SQL:  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el ejemplo siguiente en la ventana de consulta y, a continuación, haga clic en **Ejecutar**.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
#### <a name="to-resume-includesssmartbackupincludesss-smartbackup-mdmd-using-transact-sql"></a>Para reanudar [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con Transact-SQL  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el ejemplo siguiente en la ventana de consulta y, a continuación, haga clic en **Ejecutar**.  
  
```  
Use msdb;  
Go  
EXEC managed_backup. sp_backup_master_switch @new_state=1;  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Habilitar la copia de seguridad administrada de SQL Server en Microsoft Azure](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)  
  
  
