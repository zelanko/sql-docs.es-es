---
title: MSSQL_ENG003165 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e1702588ba6ac1beeb33b87a7afc7fc330271559
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049313"
---
# <a name="mssql_eng003165"></a>MSSQL_ENG003165
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|3165|  
|Origen de eventos|MSSQLSERVER|  
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
  
1.  Ejecute ALTER DATABASE para conectar la base de datos en línea; por ejemplo: `ALTER DATABASE AdventureWorks SET ONLINE`. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql). Si desea conservar la configuración de la réplica, vaya al paso 2. En caso contrario, continúe en el paso 3.  
  
2.  Ejecute [sp_restoredbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql). Si este procedimiento almacenado se ejecuta correctamente, la restauración ha finalizado. Si no se ejecuta correctamente, vaya al paso 3.  
  
3.  Ejecute [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) para eliminar la configuración de replicación completa.  
  
     Si es necesario, vuelva a configurar la replicación. Si, tal y como se recomienda, ha creado scripts para la topología de replicación, utilícelos para volver a configurar la topología.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Hacer copias de seguridad y restaurar bases de datos replicadas](administration/back-up-and-restore-replicated-databases.md)   
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
