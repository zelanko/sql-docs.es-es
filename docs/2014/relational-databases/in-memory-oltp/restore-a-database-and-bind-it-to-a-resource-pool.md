---
title: Restaurar una base de datos y enlazarla a un grupo de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0d20a569-8a27-409c-bcab-0effefb48013
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0b518c93ca9d5e7157ceaa20d9548d7b6061017d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050044"
---
# <a name="restore-a-database-and-bind-it-to-a-resource-pool"></a>Restaurar una base de datos y enlazarla a un grupo de recursos de servidor
  Aunque tenga memoria suficiente para restaurar una base de datos con tablas optimizadas para memoria, se aconseja seguir los procedimientos recomendados y enlazar la base de datos a un grupo de recursos de servidor con nombre. Puesto que es preciso que la base de datos exista antes de poder enlazarla al grupo que restaura la base de datos, se trata de un proceso en varias fases. Este tema le guiará a través de ese proceso.  
  
##  <a name="restore-with-norecovery"></a>Restaure con NORECOVERY.  
 Cuando se restaura una base de datos, NORECOVERY provoca que se cree la base de datos y se restaura la imagen de disco sin consumir memoria.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   FROM DISK = 'C:\IMOLTP_test\IMOLTP_DB.bak'  
   WITH NORECOVERY  
```  
  
##  <a name="create-the-resource-pool"></a>Crear el grupo de recursos de servidor  
 El siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)] crea un grupo de recursos de servidor denominado Pool_IMOLTP con el 50 % de memoria disponible para su uso.  Una vez creado el grupo, hay que reconfigurar el Regulador de recursos para incluir Pool_IMOLTP.  
  
```sql  
CREATE RESOURCE POOL Pool_IMOLTP WITH (MAX_MEMORY_PERCENT = 50);  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
##  <a name="bind-the-database-and-resource-pool"></a>Enlazar la base de datos y el grupo de recursos de servidor  
 Use la función del sistema `sp_xtp_bind_db_resource_pool` para enlazar la base de datos al grupo de recursos de servidor. La función utiliza dos parámetros: el nombre de la base de datos seguido del nombre del grupo de recursos de servidor.  
  
 El siguiente código [!INCLUDE[tsql](../../includes/tsql-md.md)] define un enlace de la base de datos IMOLTP_DB con el grupo de recursos de servidor Pool_IMOLTP. El enlace no toma efecto hasta que se complete el paso siguiente.  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
##  <a name="restore-with-recovery"></a>Restaurar con RECOVERY  
 Cuando restaure la base de datos con RECOVERY, la base de datos se conecta y se restauran todos los datos.  
  
```sql  
RESTORE DATABASE IMOLTP_DB   
   WITH RECOVERY  
```  
  
##  <a name="monitor-the-resource-pool-performance"></a>Supervisar el rendimiento del grupo de recursos de servidor  
 Una vez que la base de datos se enlaza al grupo de recursos de servidor con nombre y se restaura con la recuperación, supervise el objeto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Estadísticas de grupo de recursos de servidor. Para obtener más información vea [Objeto SQL Server: Estadísticas de grupo de recursos de servidor](../performance-monitor/sql-server-resource-pool-stats-object.md).  
  
## <a name="see-also"></a>Consulte también  
 [Enlazar una base de datos con tablas optimizadas para memoria a un grupo de recursos](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [Sys. sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [SQL Server, objeto de estadísticas de grupo de recursos](../performance-monitor/sql-server-resource-pool-stats-object.md)   
 [sys.dm_resource_governor_resource_pools](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)  
  
  
