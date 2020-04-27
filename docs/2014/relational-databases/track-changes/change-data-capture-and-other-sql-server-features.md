---
title: Captura de datos modificados y otras características de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87fcd7656ff1e86522e4ea398fc49d91acde9a34
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62672074"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>Captura de datos modificados y otras características de SQL Server
  En este tema se describe cómo interactúan las características siguientes con la captura de datos modificados:  
  
-   [Seguimiento de cambios](#ChangeTracking)  
  
-   [Creación de reflejo de la base de datos](#DatabaseMirroring)  
  
-   [Replicación transaccional](#TransReplication)  
  
-   [Restaurar o asociar una base de datos habilitada para la captura de datos modificados](#RestoreOrAttach)  
  
##  <a name="change-tracking"></a><a name="ChangeTracking"></a>Change Tracking  
 La captura de datos modificados y el [seguimiento de cambios](about-change-tracking-sql-server.md) pueden habilitarse en la misma base de datos. No se requiere ninguna consideración especial. Para obtener más información, vea [Trabajar con el seguimiento de cambios &#40;SQL Server&#41;](work-with-change-tracking-sql-server.md).  
  
##  <a name="database-mirroring"></a><a name="DatabaseMirroring"></a>Creación de reflejo de la base de datos  
 Se puede reflejar una base de datos que está habilitada para la captura de datos modificados. Para asegurarse de que la captura y la limpieza se producen automáticamente tras una conmutación por error, siga estos pasos:  
  
1.  Asegúrese de que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecute en la nueva instancia del servidor principal.  
  
2.  Cree el trabajo de captura y el trabajo de limpieza en la nueva base de datos principal, la antigua base de datos de reflejo. Para crear los trabajos, use el procedimiento almacenado [sp_cdc_add_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql) .  
  
 Para ver la configuración actual de un trabajo de captura o limpieza, use el procedimiento almacenado [sys.sp_cdc_help_jobs](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql) en la nueva instancia de servidor principal. Para una base de datos concreta, el trabajo de captura se denomina cdc.*database_name*_capture y el trabajo de limpieza, cdc.*database_name*_cleanup, donde *database_name* es el nombre de la base de datos.  
  
 Para cambiar la configuración de un trabajo, use el procedimiento almacenado [sys.sp_cdc_change_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql) .  
  
 Para obtener más información sobre la creación de reflejo de la base de datos, vea [Creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
##  <a name="transactional-replication"></a><a name="TransReplication"></a>Replicación transaccional  
 La captura de datos modificados y la replicación transaccional pueden coexistir en la misma base de datos, pero el rellenado de las tablas de cambios se trata de forma diferente cuando se habilitan ambas características. La captura de datos modificados y la replicación transaccional siempre usan el mismo procedimiento, [sp_replcmds](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql), para leer los cambios del registro de transacciones. Cuando la captura de datos modificados se habilita por sí [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sola, un `sp_replcmds`trabajo del agente llama a. Cuando ambas características están habilitadas en la misma base de datos, `sp_replcmds`el agente de registro del log llama a. Este agente rellena las tablas de cambios y las tablas de base de datos de distribución. Para más información, consulte [Replication Log Reader Agent](../replication/agents/replication-log-reader-agent.md).  
  
 Considere un escenario en el que la captura de datos modificados está habilitada en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y se habilitan dos tablas para la captura. Para rellenar las tablas de cambios, el `sp_replcmds`trabajo de captura llama a. La base de datos se habilita para la replicación transaccional y se crea una publicación. Ahora, se crea el Agente de registro del LOG para la base de datos y se elimina el trabajo de captura. El Agente de registro del LOG continúa examinando el registro desde el último número de secuencia de registro que se confirmó en la tabla de cambios. De esta forma se asegura de la coherencia de los datos en las tablas de cambios. Si la replicación transaccional está deshabilitada en esta base de datos, se quita el Agente de registro del LOG y vuelve a recrear el trabajo de captura.  
  
> [!NOTE]  
>  Cuando el Agente de registro del LOG se utiliza para la captura de datos modificados y la replicación transaccional, los cambios replicados se escriben primero en la base de datos de distribución. A continuación, los cambios capturados se escriben en las tablas de cambios. Ambas operaciones se confirman conjuntamente. Si hay alguna latencia al escribir en la base de datos de distribución, habrá una latencia correspondiente antes de que los cambios aparezcan en las tablas de cambios.  
  
 La opción **proc exec** de la replicación transaccional no está disponible cuando la captura de datos modificados está habilitada.  
  
##  <a name="restoring-or-attaching-a-database-enabled-for-change-data-capture"></a><a name="RestoreOrAttach"></a>Restaurar o adjuntar una base de datos habilitada para la captura de datos modificados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la lógica siguiente para determinar si la captura de datos modificados permanece habilitada una vez restaurada o asociada una base de datos:  
  
-   Si una base de datos se restaura en el mismo servidor con el mismo nombre, la captura de datos modificados sigue habilitada.  
  
-   Si una base de datos se restaura en otro servidor, de forma predeterminada la captura de datos modificados está deshabilitada y se eliminan todos los metadatos relacionados.  
  
     Para conservar la captura de datos modificados, utilice la opción `KEEP_CDC` al restaurar la base de datos. Para obtener más información acerca de esta opción, vea [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql).  
  
-   Si una base de datos se desasocia y asocia en el mismo servidor o en otro servidor, la captura de datos modificados sigue estando habilitada.  
  
-   Si una base de datos se asocia o restaura con la opción `KEEP_CDC` en cualquier edición distinta de Enterprise, la operación se bloquea porque la captura de datos modificados requiere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise. Se muestra el mensaje de error 934:  
  
     `SQL Server cannot load database '%.*ls' because change data capture is enabled. The currently installed edition of SQL Server does not support change data capture. Either disable change data capture in the database by using a supported edition of SQL Server, or upgrade the instance to one that supports change data capture.`  
  
 Puede usar [sys.sp_cdc_disable_db](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql) para quitar la captura de datos modificados desde una base de datos restaurada o asociada.  
  
## <a name="change-data-capture-and-alwayson"></a>Captura de datos modificados y AlwaysON  
 Cuando se utiliza AlwaysON, la enumeración de cambios se debe realizar en la réplica secundaria con el fin de reducir la carga del disco en la réplica principal.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar y supervisar la captura de datos modificados &#40;SQL Server&#41;](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
