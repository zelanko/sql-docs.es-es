---
title: Sys.dm_db_missing_index_group_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_group_stats_TSQL
- sys.dm_db_missing_index_group_stats
- dm_db_missing_index_group_stats_TSQL
- dm_db_missing_index_group_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_group_stats dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_group_stats dynamic management view
ms.assetid: c2886986-9e07-44ea-a350-feeac05ee4f4
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4ef06db0b1e9adda430667ee418390cdfb8813ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbmissingindexgroupstats-transact-sql"></a>sys.dm_db_missing_index_group_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información de resumen sobre los grupos de índices que faltan, excluidos los índices espaciales.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra.  
    
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**group_handle**|**int**|Identifica un grupo de índices que faltan. Este identificador es único en todo el servidor.<br /><br /> Las otras columnas proporcionan información sobre todas las consultas para las que se considera que falta el índice del grupo.<br /><br /> Un grupo de índices solo contiene un índice.|  
|**unique_compiles**|**bigint**|Número de compilaciones y recompilaciones que se beneficiarían de este grupo de índices que faltan. Las compilaciones y recompilaciones de muchas consultas distintas puede contribuir a este valor de columna.|  
|**user_seeks**|**bigint**|Número de búsquedas iniciadas por consultas de usuario para las que se podría haber utilizado el índice recomendado del grupo.|  
|**user_scans**|**bigint**|Número de recorridos iniciados por consultas de usuario para los que se podría haber utilizado el índice recomendado del grupo.|  
|**last_user_seek**|**datetime**|Fecha y hora de la última búsqueda iniciada por consultas de usuario para la que se podría haber utilizado el índice recomendado del grupo.|  
|**last_user_scan**|**datetime**|Fecha y hora del último recorrido iniciado por consultas de usuario para el que se podría haber utilizado el índice recomendado del grupo.|  
|**avg_total_user_cost**|**float**|Costo medio de las consultas de usuario que podría reducirse mediante el índice del grupo.|  
|**avg_user_impact**|**float**|Beneficio porcentual medio que podrían obtener las consultas de usuario si se implementara este grupo de índices que faltan. El valor significa que el costo de las consultas se reduciría este porcentaje como promedio si se implementara este grupo de índices que faltan.|  
|**system_seeks**|**bigint**|Número de búsquedas iniciadas por consultas del sistema, como consultas de estadísticas automáticas, para las que se podría haber utilizado el índice recomendado del grupo. Para obtener más información, consulte [Auto Stats (clase de eventos)](../../relational-databases/event-classes/auto-stats-event-class.md).|  
|**system_scans**|**bigint**|Número de recorridos iniciados por consultas del sistema para los que se podría haber utilizado el índice recomendado del grupo.|  
|**last_system_seek**|**datetime**|Fecha y hora de la última búsqueda en el sistema iniciada por consultas del sistema para la que se podría haber utilizado el índice recomendado del grupo.|  
|**last_system_scan**|**datetime**|Fecha y hora del último recorrido en el sistema iniciado por consultas del sistema para el que se podría haber utilizado el índice recomendado del grupo.|  
|**avg_total_system_cost**|**float**|Costo medio de las consultas del sistema que podría reducirse mediante el índice del grupo.|  
|**avg_system_impact**|**float**|Beneficio porcentual medio que podrían obtener las consultas del sistema si se implementara este grupo de índices que faltan. El valor significa que el costo de las consultas se reduciría este porcentaje como promedio si se implementara este grupo de índices que faltan.|  
  
## <a name="remarks"></a>Comentarios  
 Información devuelta por **sys.dm_db_missing_index_group_stats** se actualiza en cada ejecución de la consulta, no por cada consulta compilación o recompilación. Las estadísticas de uso no se guardan; solo se conservan hasta que se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los administradores de bases de datos deben realizar periódicamente una copia de seguridad de la información de los índices que faltan si desean conservar las estadísticas de uso después del reciclaje del servidor.  
  
## <a name="permissions"></a>Permissions  
 Para consultar esta vista de administración dinámica, se debe conceder a los usuarios el permiso VIEW SERVER STATE o cualquier permiso que implique el permiso VIEW SERVER STATE.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo utilizar el **sys.dm_db_missing_index_group_stats** vista de administración dinámica.  
  
### <a name="a-find-the-10-missing-indexes-with-the-highest-anticipated-improvement-for-user-queries"></a>A. Buscar los 10 índices que faltan para los que se prevé mayor aumento de rendimiento en las consultas de usuario  
 La siguiente consulta determina cuáles de los 10 índices que faltan producirían el mayor aumento acumulado previsto, en orden descendente, para consultas de usuario.  
  
```  
SELECT TOP 10 *  
FROM sys.dm_db_missing_index_group_stats  
ORDER BY avg_total_user_cost * avg_user_impact * (user_seeks + user_scans)DESC;  
```  
  
### <a name="b-find-the-individual-missing-indexes-and-their-column-details-for-a-particular-missing-index-group"></a>B. Buscar los índices que faltan individuales y sus detalles de columna para un grupo específico de índices que faltan  
 La siguiente consulta determina cuáles de los índices que faltan forman un grupo específico de índices que faltan y muestra sus detalles de columna. Para este ejemplo, el identificador del grupo de índices que faltan es 24.  
  
```  
SELECT migs.group_handle, mid.*  
FROM sys.dm_db_missing_index_group_stats AS migs  
INNER JOIN sys.dm_db_missing_index_groups AS mig  
    ON (migs.group_handle = mig.index_group_handle)  
INNER JOIN sys.dm_db_missing_index_details AS mid  
    ON (mig.index_handle = mid.index_handle)  
WHERE migs.group_handle = 24;  
```  
  
 Esta consulta proporciona el nombre de la base de datos, el esquema y la tabla en que falta un índice. También proporciona los nombres de las columnas que deben usarse para la clave de índice. Al escribir la instrucción CREATE INDEX DDL para implementar índices que faltan, se muestran las columnas de igualdad en primer lugar y, a continuación, las columnas de desigualdad en ON \< *table_name*> cláusula de la instrucción CREATE INDEX. Las columnas incluidas deben mostrarse en la cláusula INCLUDE de la instrucción CREATE INDEX. Para determinar un orden efectivo para las columnas de igualdad, ordénelas en función de su selectividad, mostrando primero las columnas más selectivas (extremo izquierdo en la lista de columnas).  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  
