---
title: MSSQL_ENG003165 | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8528ec8a83d6f6ca4a92753fb6103a54226ac7bd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="mssqleng003165"></a>MSSQL_ENG003165
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3165|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|La base de datos '%ls' se restauró. Sin embargo, se encontró un error al restaurar o quitar la replicación. Se ha dejado la base de datos sin conexión. Vea el tema MSSQL_ENG003165 en los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
 Este error aparece si se produce un problema al restaurar una copia de seguridad de una base de datos replicada:  
  
-   Si la copia de seguridad se restaura en la misma base de datos y el mismo servidor en los que se realizó, el error indica que no se ha podido restaurar correctamente la configuración de la replicación.  
  
-   Si la copia de seguridad se restaura en una base de datos o un servidor distintos, el error indica que no se ha podido quitar correctamente la configuración de la replicación (de forma predeterminada, la configuración de la replicación se quita si la base de datos o el servidor son distintos).  
  
 Este error probablemente se debe a una discrepancia entre el estado de la base de datos restaurada y una o más bases de datos del sistema que contienen metadatos de replicación: **msdb**, **maestra**o la base de datos de distribución.  
  
## <a name="user-action"></a>Acción del usuario  
 Para solucionar este problema:  
  
1.  Ejecute ALTER DATABASE para conectar la base de datos en línea; por ejemplo: `ALTER DATABASE AdventureWorks SET ONLINE`. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md). Si desea conservar la configuración de la réplica, vaya al paso 2. En caso contrario, continúe en el paso 3.  
  
2.  Ejecute [sp_restoredbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql.md). Si este procedimiento almacenado se ejecuta correctamente, la restauración ha finalizado. Si no se ejecuta correctamente, vaya al paso 3.  
  
3.  Ejecute [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) para eliminar la configuración de replicación completa.  
  
     Si es necesario, vuelva a configurar la replicación. Si, tal y como se recomienda, ha creado scripts para la topología de replicación, utilícelos para volver a configurar la topología.  
  
## <a name="see-also"></a>Vea también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
