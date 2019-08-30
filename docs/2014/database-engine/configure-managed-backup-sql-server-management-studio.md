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
ms.openlocfilehash: 021db5a2283eb6ec68ea80302e938f08e7ba1a5c
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154341"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>Configurar la copia de seguridad administrada (SQL Server Management Studio)
  El cuadro de diálogo **copia de seguridad administrada** permite configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] los valores predeterminados para la instancia. En este tema se describe cómo usar este cuadro de diálogo para configurar los valores predeterminados de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] de la instancia y las opciones que debe tener en cuenta al hacerlo. Cuando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado para la instancia, la configuración se aplica a cualquier base de datos nueva creada posteriormente.  
  
 Si desea configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para una base de datos específica, consulte [habilitación y configuración de SQL Server copia de seguridad administrada en Azure para una base de datos](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
 
> [!NOTE] 
> Los servidores proxy no admiten copias de seguridad administradas en SQL Server. 
  
## <a name="task-list"></a>Lista de tareas  
  
## <a name="includess_smartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>Funciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con la interfaz de copias de seguridad administradas en SQL Server Management Studio  
 En esta versión, solo puede configurar los valores predeterminados de nivel de instancia mediante la interfaz de **copia de seguridad de administración** . No se puede configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para una base de datos, pausar o reanudar las operaciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ni configurar notificaciones de correo electrónico. Para obtener información sobre cómo realizar operaciones que no se admiten actualmente a través de la interfaz de **copia de seguridad administrada** , vea [SQL Server la configuración de la retención y almacenamiento de Azure](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md).  
  
## <a name="permissions"></a>Permisos  
 **Ver el nodo de copia de seguridad administrada es SQL Server Management Studio:** Para ver el nodo de **copia de seguridad administrada** en **Explorador de objetos**, debe ser administrador del sistema o tener los siguientes permisos concedidos específicamente a su cuenta de usuario:  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE`en `smart_admin.fn_is_master_switch_on`.  
  
-   `SELECT`en `smart_admin.fn_backup_instance_config`.  
  
 **Para configurar la copia de seguridad administrada:** para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] en SQL Server Management Studio, debe ser administrador del sistema o tener los permisos siguientes:  
  
 Pertenencia en el rol de base de datos `db_backupoperator`, con permisos `ALTER ANY CREDENTIAL` y permisos `EXECUTE` en el procedimiento almacenado de `sp_delete_backuphistory`.  
  
 `SELECT`permisos en la `smart_admin.fn_get_current_xevent_settings` función.  
  
 `EXECUTE`permisos en el `smart_admin.sp_get_backup_diagnostics` procedimiento almacenado. Además, requiere permisos `VIEW SERVER STATE` ya que internamente llama a otros objetos del sistema que requieren este permiso.  
  
 Permisos `EXECUTE` en `smart_admin.sp_set_instance_backup` y `smart_admin.sp_backup_master_switch`.  
  
## <a name="configure-includess_smartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>Configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con SQL Server Management Studio  
 En el **Explorador de objetos**, expanda el nodo **Administración** y haga clic con el botón derecho en **copia de seguridad administrada**. Seleccione **Configurar**. Esto abre el cuadro de diálogo **Copia de seguridad administrada** .  
  
 Active la opción **Habilitar copia de seguridad administrada** y especifique los valores de configuración:  
  
 El período de **retención de archivos** se especifica en días y debe estar entre 1 y 30.  
  
 La **credencial SQL** que seleccione debe coincidir con la cuenta de almacenamiento. Si actualmente no tiene una credencial SQL que almacene la información de autenticación, puede crear una haciendo clic en **crear**. También puede crear la credencial con la instrucción CREATE CREDENTIAL de Transact-SQL y proporcionar el nombre de la cuenta de almacenamiento de Identidad y la clave de acceso de los parámetros SECRET. Para obtener más información, vea [crear una credencial](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential).  
  
 Especifique la **dirección URL de almacenamiento** de la cuenta de almacenamiento de Azure, la credencial de SQL que almacena la información de autenticación para la cuenta de almacenamiento y el período de retención de los archivos de copia de seguridad.  
  
 El formato de la dirección URL de\<almacenamiento es: https://StorageAccount >. BLOB. Core. Windows. net/  
  
 Para establecer la configuración de cifrado en el nivel de instancia, active la opción **cifrar copia de seguridad** y especifique el algoritmo y un certificado o clave asimétrica que se usará para el cifrado.  Esto se establece en el nivel de instancia y se usa para todas las bases de datos creadas después de la aplicación de esta configuración.  
  
> [!WARNING]  
>  Este cuadro de diálogo no se puede usar para especificar las opciones de cifrado sin configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Estas opciones de cifrado solo se aplican a las operaciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para usar el cifrado para otros procedimientos de copia de seguridad, vea cifrado de [copia de seguridad](../relational-databases/backup-restore/backup-encryption.md).  
  
### <a name="considerations"></a>Consideraciones  
 Si configura [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] en el nivel de instancia, la configuración se aplica a cualquier base de datos creada posteriormente.  Sin embargo, la base de datos existente no heredará automáticamente esta configuración. Para configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] en bases de datos existentes, debe configurar cada base de datos específicamente. Para obtener más información, vea [habilitar y configurar SQL Server copia de seguridad administrada en Azure para una base de datos](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure).  
  
 Si [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se ha pausado mediante el `smart_admin.sp_backup_master_switch`, verá un mensaje de advertencia que indica que la copia de seguridad administrada está deshabilitada y que las configuraciones actuales no surtirán efecto... al intentar completar la configuración. Use el `smart_admin.sp_backup_master_switch` almacenado y establezca el @new_statevalor = 1. Esto reanudará los servicios de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] y aplicará las opciones de configuración. Para obtener más información sobre el procedimiento almacenado, vea [smart_admin. SP &#40;_ BACKUP_MASTER_SWITCH Transact&#41;-SQL](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [SQL Server copia de seguridad administrada en Azure: Interoperabilidad y coexistencia](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
