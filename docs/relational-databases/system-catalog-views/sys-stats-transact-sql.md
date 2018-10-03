---
title: Sys.STATS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.stats
- stats_TSQL
- sys.stats_TSQL
- stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.stats catalog view
ms.assetid: 42605c80-126f-460a-befb-a0b7482fae6a
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5150dfbccb6998c69151ca4cf02d9fe88a222830
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832374"
---
# <a name="sysstats-transact-sql"></a>sys.stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada objeto de estadísticas que existe para las tablas, los índices y las vistas indizadas de la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cada índice tiene una fila de estadísticas correspondiente con el mismo nombre e identificador (**index_id** = **stats_id**), pero no cada fila de estadísticas tiene un índice correspondiente.  
  
 La vista de catálogo [sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) proporciona información estadística para cada columna de la base de datos. Para obtener más información sobre las estadísticas, vea [Estadísticas](../../relational-databases/statistics/statistics.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenecen estas estadísticas.|  
|**Nombre**|**sysname**|Nombre de las estadísticas. Es único en el objeto.|  
|**stats_id**|**int**|Id. de las estadísticas. Es único en el objeto.<br /><br />Si las estadísticas corresponden a un índice, el *stats_id* valor es igual que el *index_id* valor en el [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.|  
|**auto_created**|**bit**|Indica si las estadísticas fueron creadas automáticamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = Las estadísticas no fueron creadas automáticamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Las estadísticas fueron creadas automáticamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**user_created**|**bit**|Indica si las estadísticas fueron creadas por un usuario.<br /><br /> 0 = Las estadísticas no fueron creadas por un usuario.<br /><br /> 1 = Las estadísticas fueron creadas por un usuario.|  
|**no_recompute**|**bit**|Indica si las estadísticas fueron creadas con el **NORECOMPUTE** opción.<br /><br /> 0 = las estadísticas no se crearon con la **NORECOMPUTE** opción.<br /><br /> 1 = las estadísticas fueron creadas con el **NORECOMPUTE** opción.|  
|**definiciones has_filter**|**bit**|0 = Las estadísticas no tienen un filtro y se calculan en todas las filas.<br /><br /> 1 = Las estadísticas tienen un filtro y solo se calculan en las filas que cumplen con la definición del filtro.|  
|**filter_definition**|**nvarchar(max)**|Expresión para el subconjunto de filas incluido en las estadísticas filtradas.<br /><br /> NULL = estadísticas no filtradas.|  
|**is_temporary**|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica si las estadísticas son temporales. Las estadísticas temporales admiten las bases de datos secundarias de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] habilitadas para acceso de solo lectura.<br /><br /> 0 = Las estadísticas no son temporales.<br /><br /> 1 = Las estadísticas son temporales.|  
|**is_incremental**|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica si las estadísticas se crean como estadísticas incrementales.<br /><br /> 0 = Las estadísticas no son incrementales.<br /><br /> 1 = Las estadísticas son incrementales.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se devuelven todas las estadísticas y las columnas de estadísticas de la tabla `HumanResources.Employee`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT s.name AS statistics_name  
      ,c.name AS column_name  
      ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('HumanResources.Employee');  
```  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Utilizar las estadísticas para mejorar el rendimiento de las consultas](../../relational-databases/statistics/statistics.md)    
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [Sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)   
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)
 

 
