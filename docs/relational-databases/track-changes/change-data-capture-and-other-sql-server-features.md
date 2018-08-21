---
title: Captura de datos modificados y otras características de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: track-changes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6d973be20ee14975fce34e7712d44ea8338931fa
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/08/2018
ms.locfileid: "39661458"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>Captura de datos modificados y otras características de SQL Server
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo interactúan las características siguientes con la captura de datos modificados:  
  
-   [Seguimiento de cambios](#ChangeTracking)  
  
-   [Creación de reflejo de base de datos](#DatabaseMirroring)  
  
-   [Replicación transaccional](#TransReplication)  
  
-   [Restaurar o asociar una base de datos habilitada para la captura de datos modificados](#RestoreOrAttach)

-   [Bases de datos independientes](#Contained)
  
##  <a name="ChangeTracking"></a> Seguimiento de los cambios  
 La captura de datos modificados y el [seguimiento de cambios](../../relational-databases/track-changes/about-change-tracking-sql-server.md) pueden habilitarse en la misma base de datos. No se requiere ninguna consideración especial. Para obtener más información, vea [Trabajar con el seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md).  
  
##  <a name="DatabaseMirroring"></a> Creación de reflejo de base de datos  
 Se puede reflejar una base de datos que está habilitada para la captura de datos modificados. Para asegurarse de que la captura y la limpieza se producen automáticamente tras una conmutación por error, siga estos pasos:  
  
1.  Asegúrese de que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecute en la nueva instancia del servidor principal.  
  
2.  Cree el trabajo de captura y el trabajo de limpieza en la nueva base de datos principal, la antigua base de datos de reflejo. Para crear los trabajos, use el procedimiento almacenado [sp_cdc_add_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) .  
  
 Para ver la configuración actual de un trabajo de captura o limpieza, use el procedimiento almacenado [sys.sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md) en la nueva instancia de servidor principal. Para una base de datos concreta, el trabajo de captura se denomina cdc.*database_name*_capture y el trabajo de limpieza, cdc.*database_name*_cleanup, donde *database_name* es el nombre de la base de datos.  
  
 Para cambiar la configuración de un trabajo, use el procedimiento almacenado [sys.sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md).  
  
 Para obtener más información sobre la creación de reflejo de la base de datos, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
##  <a name="TransReplication"></a> Transactional Replication  
 La captura de datos modificados y la replicación transaccional pueden coexistir en la misma base de datos, pero el rellenado de las tablas de cambios se trata de forma diferente cuando se habilitan ambas características. La captura de datos modificados y la replicación transaccional siempre usan el mismo procedimiento, [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md), para leer los cambios del registro de transacciones. Cuando la captura de datos modificados se habilita sola, un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] llama a **sp_replcmds**. Cuando ambas características están habilitadas en la misma base de datos, el Agente de registro del LOG llama a **sp_replcmds**. Este agente rellena las tablas de cambios y las tablas de base de datos de distribución. Para obtener más información, consulte [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md).  
  
 Considere un escenario en el que la captura de datos modificados está habilitada en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se habilitan dos tablas para la captura. Para rellenar las tablas de cambios, el trabajo de captura llama a **sp_replcmds**. La base de datos se habilita para la replicación transaccional y se crea una publicación. Ahora, se crea el Agente de registro del LOG para la base de datos y se elimina el trabajo de captura. El Agente de registro del LOG continúa examinando el registro desde el último número de secuencia de registro que se confirmó en la tabla de cambios. De esta forma se asegura de la coherencia de los datos en las tablas de cambios. Si la replicación transaccional está deshabilitada en esta base de datos, se quita el Agente de registro del LOG y vuelve a recrear el trabajo de captura.  
  
> [!NOTE]  
>  Cuando el Agente de registro del LOG se utiliza para la captura de datos modificados y la replicación transaccional, los cambios replicados se escriben primero en la base de datos de distribución. A continuación, los cambios capturados se escriben en las tablas de cambios. Ambas operaciones se confirman conjuntamente. Si hay alguna latencia al escribir en la base de datos de distribución, habrá una latencia correspondiente antes de que los cambios aparezcan en las tablas de cambios.  
  
 La opción **proc exec** de la replicación transaccional no está disponible cuando la captura de datos modificados está habilitada.  
  
##  <a name="RestoreOrAttach"></a> Restaurar o asociar una base de datos habilitada para la captura de datos modificados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la lógica siguiente para determinar si la captura de datos modificados permanece habilitada una vez restaurada o asociada una base de datos:  
  
-   Si una base de datos se restaura en el mismo servidor con el mismo nombre, la captura de datos modificados sigue habilitada.  
  
-   Si una base de datos se restaura en otro servidor, de forma predeterminada la captura de datos modificados está deshabilitada y se eliminan todos los metadatos relacionados.  
  
     Para conservar la captura de datos modificados, use la opción **KEEP_CDC** a la hora de restaurar la base de datos. Para obtener más información acerca de esta opción, vea [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md).  
  
-   Si una base de datos se desasocia y asocia en el mismo servidor o en otro servidor, la captura de datos modificados sigue estando habilitada.  
  
-   Si una base de datos se asocia o restaura con la opción **KEEP_CDC** en cualquier edición distinta de Enterprise, la operación se bloquea porque la captura de datos modificados requiere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. Se muestra el mensaje de error 934:  
  
     `SQL Server cannot load database '%.*ls' because Change Data Capture is enabled. The currently installed edition of SQL Server does not support Change Data Capture. Either restore database without KEEP_CDC option, or upgrade the instance to one that supports Change Data Capture.`  
  
 Puede usar [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) para quitar la captura de datos modificados desde una base de datos restaurada o asociada.  
  
##  <a name="Contained"></a> Bases de datos independientes  
 La captura de datos modificados no se admite en [bases de datos independientes](../../relational-databases/databases/contained-databases.md).
  
## <a name="change-data-capture-and-always-on"></a>Captura de datos modificados y AlwaysOn  
 Cuando se usa AlwaysOn, la enumeración de cambios se debe realizar en la réplica secundaria con el fin de reducir la carga del disco en la réplica principal.  
  
## <a name="see-also"></a>Ver también  
 [Administrar y supervisar la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
