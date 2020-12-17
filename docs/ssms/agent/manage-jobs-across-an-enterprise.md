---
description: Administrar trabajos en una empresa
title: Administrar trabajos en una empresa
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 62e4eb1574d48ecd40af46ba081f6443bdafb000
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482218"
---
# <a name="manage-jobs-across-an-enterprise"></a>Administrar trabajos en una empresa
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Si realiza cambios en definiciones de trabajos multiservidor fuera de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], tendrá que exponer los cambios en la lista de descargas para que los servidores de destino puedan volver a descargar el trabajo actualizado. Para asegurarse de que los servidores de destino tienen las definiciones de trabajos actuales, exponga una instrucción INSERT después de actualizar el trabajo multiservidor, como se explica a continuación:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Para notificar a los servidores de destino de que se ha modificado un trabajo multiservidor, debe invocar el comando anterior después de utilizar uno de los siguientes procedimientos:  
  
-   [sp_add_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
-   [sp_update_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)  
  
-   [sp_delete_jobstep (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)  
  
-   [Administrar eventos](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_detach_schedule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
    > [!NOTE]  
    > No es necesario llamar a **sp_post_msx_operation** después de llamar a **sp_update_job** o **sp_delete_job**, ya que estos procedimientos almacenados exponen automáticamente los cambios necesarios en la lista de descarga.  
  
A continuación se muestran tareas comunes para la administración de trabajos en una empresa:  
  
**Para comprobar el estado de un servidor de destino**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)  
  
-   [Objetos de administración de SQL Server (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**Para modificar los servidores de destino para un trabajo**  
  
-   [SQL Server Management Studio](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)  
  
-   [Objetos de administración de SQL Server (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**Para modificar la ubicación de un servidor de destino**  
  
-   [SQL Server Management Studio](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)  
  
-   [Objetos de administración de SQL Server (SMO)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**Para sincronizar los relojes de los servidores de destino**  
  
-   [SQL Server Management Studio](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
  
**Para forzar que un servidor de destino sondee el servidor maestro**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
[Administrar eventos](../../ssms/agent/manage-events.md)  
