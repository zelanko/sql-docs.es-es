---
title: Configurar copia de seguridad administrada (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f8c9664baa2803bbab4282b6897d49f0ddb1831
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812712"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>Configurar la copia de seguridad administrada (SQL Server Management Studio)
  El **copia de seguridad administrada** cuadro de diálogo le permite configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] valores predeterminados para la instancia. En este tema se describe cómo usar este cuadro de diálogo para configurar los valores predeterminados de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de la instancia y las opciones que debe tener en cuenta al hacerlo. Cuando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado para la instancia, la configuración se aplica a cualquier base de datos nueva creada posteriormente.  
  
 Si desea configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para una base de datos específica, consulte [habilitar y configurar SQL Server Managed Backup to Windows Azure para una base de datos](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
 
> [!NOTE] 
> Los servidores proxy no admiten copias de seguridad administradas en SQL Server. 
  
## <a name="task-list"></a>Lista de tareas  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>Funciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con la interfaz de copias de seguridad administradas en SQL Server Management Studio  
 En esta versión, sólo se pueden configurar opciones predeterminadas de nivel de instancia mediante el **copia de seguridad de administración** interfaz. No se puede configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para una base de datos, pausar o reanudar las operaciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ni configurar notificaciones de correo electrónico. Para obtener información sobre cómo realizar operaciones no se admite actualmente a través de la **copia de seguridad administrada** interfaz, vea [SQL Server Managed Backup to Windows Azure: configuración de almacenamiento y retención](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
## <a name="permissions"></a>Permisos  
 **Nodo de copia de seguridad administrada de vista es SQL Server Management Studio:** Para ver **copia de seguridad administrada** nodo **Explorador de objetos**, debe ser un administrador del sistema o tener los siguientes permisos concedidos específicamente a su cuenta de usuario:  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` en `smart_admin.fn_is_master_switch_on`.  
  
-   `SELECT` en `smart_admin.fn_backup_instance_config`.  
  
 **Para configurar la copia de seguridad administrada:** configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] en SQL Server Management Studio, debe ser un administrador del sistema o tener los permisos siguientes:  
  
 Pertenencia en el rol de base de datos `db_backupoperator`, con permisos `ALTER ANY CREDENTIAL` y permisos `EXECUTE` en el procedimiento almacenado de `sp_delete_backuphistory`.  
  
 `SELECT` los permisos en el `smart_admin.fn_get_current_xevent_settings` función.  
  
 `EXECUTE` los permisos en el `smart_admin.sp_get_backup_diagnostics` procedimiento almacenado. Además, requiere permisos `VIEW SERVER STATE` ya que internamente llama a otros objetos del sistema que requieren este permiso.  
  
 Permisos `EXECUTE` en `smart_admin.sp_set_instance_backup` y `smart_admin.sp_backup_master_switch`.  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>Configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con SQL Server Management Studio  
 Desde el **Explorador de objetos**, expanda el **administración** nodo y haga clic en **copia de seguridad administrada**. Seleccione **Configurar**. Esto abre el cuadro de diálogo **Copia de seguridad administrada** .  
  
 Comprobar **habilitar copia de seguridad administrada** opción y especifique los valores de configuración:  
  
 El **archivo retención** período se especifica en días y debe estar comprendido entre 1 y 30.  
  
 El **credencial SQL** seleccione debe coincidir con la cuenta de almacenamiento. Si no tiene una credencial de SQL que almacena la información de autenticación, puede crearla haciendo **crear**. También puede crear la credencial con la instrucción CREATE CREDENTIAL de Transact-SQL y proporcionar el nombre de la cuenta de almacenamiento de Identidad y la clave de acceso de los parámetros SECRET. Para obtener más información, consulte [crear una credencial](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential).  
  
 Especifique el **dirección URL de almacenamiento** para la cuenta de almacenamiento de Windows Azure, la credencial SQL que almacena la información de autenticación para la cuenta de almacenamiento y el período de retención para los archivos de copia de seguridad.  
  
 El formato de dirección URL de almacenamiento es: https://\<cuenta de almacenamiento >.blob.core.windows.net/  
  
 Para establecer la configuración de cifrado en el nivel de instancia, comprobar **Cifrar copia de seguridad** opción y especifique el algoritmo y un certificado o clave asimétrica que se usará para el cifrado.  Esto se establece en el nivel de instancia y se usa para todas las bases de datos creadas después de la aplicación de esta configuración.  
  
> [!WARNING]  
>  Este cuadro de diálogo no se puede usar para especificar las opciones de cifrado sin configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Estas opciones de cifrado solo se aplican a las operaciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para usar el cifrado para otros procedimientos de copia de seguridad, consulte [cifrado de copia de seguridad](../relational-databases/backup-restore/backup-encryption.md).  
  
### <a name="considerations"></a>Consideraciones  
 Si configura [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] en el nivel de instancia, la configuración se aplica a cualquier base de datos creada posteriormente.  Sin embargo, la base de datos existente no heredará automáticamente esta configuración. Para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] en bases de datos existentes, debe configurar cada base de datos específicamente. Para obtener más información, consulte [habilitar y configurar SQL Server Managed Backup to Windows Azure para una base de datos](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
  
 Si [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se ha detenido mediante el `smart_admin.sp_backup_master_switch`, aparecerá una advertencia al intentar completar la configuración del mensaje "copia de seguridad administrada está deshabilitada y las configuraciones actuales no surtirán efecto...". Use la `smart_admin.sp_backup_master_switch` almacenado y establezca el @new_state= 1. Esto reanudará los servicios de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] y aplicará las opciones de configuración. Para obtener más información sobre el procedimiento almacenado, vea [smart_admin.sp_ backup_master_switch &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server copia de seguridad administrada en Windows Azure: Interoperabilidad y coexistencia](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
