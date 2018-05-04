---
title: Sys.pdw_replicated_table_cache_state (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 07/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: barbkess
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 02c228a15c76a791ab3abd2558d63ed71d403471
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syspdwreplicatedtablecachestate-transact-sql"></a>Sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Devuelve el estado de la memoria caché asociada con una tabla replicada por **object_id**.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|El identificador de objeto para la tabla. Vea [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **object_id** es la clave para esta vista.||  
|state|**nvarchar(40)**|El estado de la memoria caché de tabla replicada para esta tabla.|'No está listo', 'Listo'|  
  
## <a name="example"></a>Ejemplo
Este ejemplo combina sys.pdw_replicated_table_cache_state con sys.tables para recuperar el nombre de tabla y el estado de la memoria caché de la tabla replicada.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>Pasos siguientes  
 Para obtener una lista de todas las vistas de catálogo para el almacenamiento de datos de SQL y almacenamiento de datos paralelos, vea [paralelo vistas de catálogo de almacenamiento de datos y almacenamiento de datos de SQL](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md).   
  
