---
title: "Supervisión y solución de problemas de migración de datos (Stretch Database) | Microsoft Docs"
ms.custom: 
ms.date: 06/14/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba0f6bd29e18108a2a93240e5fa1dd3d59d00d05
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>Supervisión y solución de problemas de migración de datos (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Para supervisar la migración de datos en Stretch Database Monitor, seleccione **Tareas | Stretch | Monitor** para una base de datos en SQL Server Management Studio.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Comprobación del estado de la migración de datos en Stretch Database Monitor  
 Seleccione **Tareas | Stretch | Monitor** para una base de datos de SQL Server Management Studio para abrir Stretch Database Monitor y supervisar la migración de datos.  
  
-   La parte superior del monitor muestra información general sobre la base de datos de SQL Server habilitada para Stretch y la base de datos de Azure remota.  
  
-   La parte inferior del monitor muestra el estado de la migración de datos para cada tabla habilitada para Stretch en la base de datos.  
  
 ![Stretch Database Monitor](../../sql-server/stretch-database/media/stretch-monitor.PNG "Stretch Database Monitor")  
  
##  <a name="Migration"></a> Comprobación del estado de la migración de datos en una vista de administración dinámica  
 Abra la vista de administración dinámica **sys.dm_db_rda_migration_status** para ver el número de lotes y filas de datos que se han migrado. Para obtener más información, vea [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
##  <a name="Firewall"></a> Solución de problemas de migración de datos  
 **Las filas de la tabla habilitada para Stretch no se están migrando a Azure. ¿Cuál es el problema?**  
 Hay varios problemas que pueden afectar a la migración. Realice las siguientes comprobaciones:  
  
-   Compruebe la conectividad de red del equipo de SQL Server.  
  
-   Compruebe que el firewall de Azure no esté impidiendo la conexión entre SQL Server y el punto de conexión remoto.  
  
-   Compruebe la vista de administración dinámica **sys.dm_db_rda_migration_status** para ver el estado del lote más reciente. Si se ha producido un error, compruebe los valores error_number, error_state y error_severity del lote.  
  
    -   Para obtener más información sobre la vista, vea [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
    -   Para obtener más información sobre el contenido de un mensaje de error de SQL Server, vea [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
 **El firewall de Azure está bloqueando las conexiones desde mi servidor local.**  
 Puede que tenga que agregar una regla en la configuración de firewall de Azure del servidor Azure para permitir que SQL Server se comunique con el servidor de Azure remoto.  
  
## <a name="see-also"></a>Ver también  
 [Administrar y solucionar problemas de Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
