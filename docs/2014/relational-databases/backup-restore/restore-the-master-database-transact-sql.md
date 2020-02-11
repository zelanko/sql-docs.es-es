---
title: Restaurar la base de datos maestra (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 823a6455616b412a41179d831b565e10b3286fb7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62875138"
---
# <a name="restore-the-master-database-transact-sql"></a>Restaurar la base de datos maestra (Transact-SQL)
  En este tema se explica cómo restaurar la base de datos **maestra** desde una copia de seguridad de base de datos completa.  
  
### <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie la instancia de servidor en modo de usuario único.  
  
     Para obtener más información sobre cómo especificar el parámetro de inicio de usuario único ( **-m**), vea [Configurar opciones de inicio del servidor &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
2.  Para restaurar una copia de seguridad de base de datos completa de **maestra**, use la siguiente instrucción [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `RESTORE DATABASE master FROM`  *<backup_device>*  `WITH REPLACE`  
  
     La opción REPLACE indica a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que restaure la base de datos especificada incluso cuando ya exista otra con el mismo nombre. La base de datos existente, si existe, se elimina. En el modo de usuario único, es recomendable introducir la instrucción RESTORE DATABASE en la [utilidad sqlcmd](../../tools/sqlcmd-utility.md). Para obtener más información, vea [Usar la utilidad sqlcmd](../scripting/sqlcmd-use-the-utility.md).  
  
    > [!IMPORTANT]  
    >  Después de que la base de datos **maestra** se haya restaurado, la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se cierra y finaliza el proceso **sqlcmd** . Antes de reiniciar la instancia de servidor, quite el parámetro de inicio de usuario único. Para obtener más información, vea [Configurar opciones de inicio del servidor &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
3.  Reinicie la instancia del servidor y continúe con otros pasos de la recuperación, por ejemplo, restaurando otras bases de datos, adjuntando bases de datos y corrigiendo incoherencias de los usuarios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente restaura la base de datos `master` en la instancia de servidor predeterminada. En el ejemplo se asume que la instancia de servidor ya se ejecuta en modo de usuario único. El ejemplo inicia `sqlcmd` y ejecuta una instrucción `RESTORE DATABASE` que restaura una copia de seguridad de base de datos completa de `master` desde un dispositivo de disco: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]
>  Para una instancia con nombre, el comando **sqlcmd** debe especificar la opción **-S** _\<nombreDeEquipo>_ \\ *\<nombreDeInstancia>* .  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](complete-database-restores-simple-recovery-model.md)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación completa&#41;](complete-database-restores-full-recovery-model.md)   
 [Solucionar problemas de usuarios huérfanos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)   
 [Volver a generar bases de datos del sistema](../databases/system-databases.md)   
 [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [Administrador de configuración de SQL Server](../sql-server-configuration-manager.md)   
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Iniciar SQL Server en modo de usuario único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
