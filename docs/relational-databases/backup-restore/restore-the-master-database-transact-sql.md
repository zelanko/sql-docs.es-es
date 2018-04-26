---
title: Restaurar la base de datos maestra (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- master database [SQL Server], restoring
ms.assetid: c83d802c-e84e-4458-b3ca-173d9ba32f73
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ded66fff7ebab4f29a883815459e1020e3acc3c7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="restore-the-master-database-transact-sql"></a>Restaurar la base de datos maestra (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se explica cómo restaurar la base de datos **maestra** desde una copia de seguridad de base de datos completa.  
  
### <a name="to-restore-the-master-database"></a>Para restaurar la base de datos maestra  
  
1.  Inicie la instancia de servidor en modo de usuario único.  
  
     Para obtener más información sobre cómo especificar el parámetro de inicio de usuario único (**-m**), vea [Configurar opciones de inicio del servidor &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
2.  Para restaurar una copia de seguridad de base de datos completa de **maestra**, use la siguiente instrucción [RESTORE DATABASE](../../t-sql/statements/restore-statements-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
     `RESTORE DATABASE master FROM`  *<dispositivo_de_copia_de_seguridad>*  `WITH REPLACE`  
  
     La opción REPLACE indica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que restaure la base de datos especificada incluso cuando ya exista otra con el mismo nombre. La base de datos existente, si existe, se elimina. En el modo de usuario único, es recomendable introducir la instrucción RESTORE DATABASE en la [utilidad sqlcmd](../../tools/sqlcmd-utility.md). Para obtener más información, vea [Usar la utilidad sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md).  
  
    > [!IMPORTANT]  
    >  Después de que la base de datos **maestra** se haya restaurado, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cierra y finaliza el proceso **sqlcmd** . Antes de reiniciar la instancia de servidor, quite el parámetro de inicio de usuario único. Para obtener más información, vea [Configurar opciones de inicio del servidor &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
3.  Reinicie la instancia del servidor y continúe con otros pasos de la recuperación, por ejemplo, restaurando otras bases de datos, adjuntando bases de datos y corrigiendo incoherencias de los usuarios.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente restaura la base de datos `master` en la instancia de servidor predeterminada. En el ejemplo se asume que la instancia de servidor ya se ejecuta en modo de usuario único. El ejemplo inicia `sqlcmd` y ejecuta una instrucción `RESTORE DATABASE` que restaura una copia de seguridad de base de datos completa de `master` desde un dispositivo de disco: `Z:\SQLServerBackups\master.bak`.  
  
> [!NOTE]  
>  Para una instancia con nombre, el comando **sqlcmd** debe especificar la opción **-S***\<<NombreDeEquipo*\\*\<NombreDeInstancia>*.  
  
```  
  
      C:\> sqlcmd  
1> RESTORE DATABASE master FROM DISK = 'Z:\SQLServerBackups\master.bak' WITH REPLACE;  
2> GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [Restauraciones de base de datos completas &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [Solucionar problemas de usuarios huérfanos &#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [Volver a generar bases de datos del sistema](../../relational-databases/databases/rebuild-system-databases.md)   
 [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md)   
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Iniciar SQL Server en modo de usuario único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
