---
title: STATS_DATE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATS_DATE_TSQL
- STATS_DATE
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], last time updated
- STATS_DATE function
- query optimization statistics [SQL Server], last time updated
- last time statistics updated
ms.assetid: f9ec3101-1e41-489d-b519-496a0d6089fb
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44fc7524040db874abc5d596b641cba985dcf893
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="statsdate-transact-sql"></a>STATS_DATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve la fecha de la actualización más reciente de las estadísticas de una tabla o vista indizada.  
  
 Para obtener más información acerca de cómo actualizar las estadísticas, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
STATS_DATE ( object_id , stats_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Identificador de la tabla o vista indizada con las estadísticas.  
  
 *stats_id*  
 Identificador del objeto de estadísticas.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve **datetime** si se ejecuta correctamente. Devuelve **NULL** en caso de error.  
  
## <a name="remarks"></a>Comentarios  
 Las funciones del sistema se pueden utilizar en la lista de selección, en la cláusula WHERE y en cualquier lugar donde se permita una expresión.  
  
## <a name="permissions"></a>Permissions  
 Es necesaria la pertenencia al rol fijo de servidor db_owner o al rol fijo de base de datos maestra o al rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-return-the-dates-of-the-most-recent-statistics-for-a-table"></a>A. Devolver las fechas de las estadísticas más recientes de una tabla  
 En el ejemplo siguiente, se devuelve la fecha de la actualización más reciente de cada objeto de estadísticas de la tabla `Person.Address`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_update_date  
FROM sys.stats   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
 Si las estadísticas corresponden a un índice, el *stats_id* valor en el [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) vista de catálogo es el mismo que el *index_id* valor en el [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo y la consulta siguiente devuelve los mismos resultados que la consulta anterior. Si las estadísticas no corresponden a un índice, aparecen en los resultados de sys.stats pero no en los de sys.indexes.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('Person.Address');  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-learn-when-a-named-statistics-was-last-updated"></a>B. Obtenga información acerca de cuándo se actualizó por última vez las estadísticas con nombre  
 En el ejemplo siguiente se crea las estadísticas sobre la columna LastName de la tabla DimCustomer. A continuación, se ejecuta una consulta para mostrar la fecha de las estadísticas. A continuación, las estadísticas de las actualizaciones y se ejecuta la consulta para mostrar la fecha de actualización de nuevo.  
  
```  
  
--First, create a statistics object  
USE AdventureWorksPDW2012;  
GO  
CREATE STATISTICS Customer_LastName_Stats  
ON AdventureWorksPDW2012.dbo.DimCustomer (LastName)  
WITH SAMPLE 50 PERCENT;  
GO  
  
--Return the date when Customer_LastName_Stats was last updated  
USE AdventureWorksPDW2012;  
GO  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO  
  
--Update Customer_LastName_Stats so it will have a different timestamp in the next query  
GO  
UPDATE STATISTICS dbo.dimCustomer (Customer_LastName_Stats);  
  
--Return the date when Customer_LastName_Stats was last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer')  
    AND s.name = 'Customer_LastName_Stats';  
GO  
  
```  
  
### <a name="c-view-the-date-of-the-last-update-for-all-statistics-on-a-table"></a>C. Ver la fecha de la última actualización de todas las estadísticas en una tabla  
 Este ejemplo devuelve la fecha de cuando se actualizó por última vez cada objeto de estadísticas en la tabla DimCustomer.  
  
```  
--Return the dates all statistics on the table were last updated.  
SELECT stats_id, name AS stats_name,   
    STATS_DATE(object_id, stats_id) AS statistics_date  
FROM sys.stats s  
WHERE s.object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
 Si las estadísticas corresponden a un índice, el *stats_id* valor en el [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) vista de catálogo es el mismo que el *index_id* valor en el [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo y la consulta siguiente devuelve los mismos resultados que la consulta anterior. Si las estadísticas no corresponden a un índice, aparecen en los resultados de sys.stats pero no en los de sys.indexes.  
  
```  
USE AdventureWorksPDW2012;  
GO  
SELECT name AS index_name,   
    STATS_DATE(object_id, index_id) AS statistics_update_date  
FROM sys.indexes   
WHERE object_id = OBJECT_ID('dbo.DimCustomer');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_autostats &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [Estadísticas](../../relational-databases/statistics/statistics.md)  
  
  


