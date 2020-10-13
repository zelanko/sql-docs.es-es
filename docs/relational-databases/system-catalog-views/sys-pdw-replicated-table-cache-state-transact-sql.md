---
description: sys.pdw_replicated_table_cache_state (Transact-SQL)
title: sys.pdw_replicated_table_cache_state (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 07/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e437a9ab920ac7f6774fad58c5927d8d43db1fb4
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005643"
---
# <a name="syspdw_replicated_table_cache_state-transact-sql"></a>sys.pdw_replicated_table_cache_state (Transact-SQL)
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  Devuelve el estado de la memoria caché asociada a una tabla replicada por **object_id**.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|IDENTIFICADOR de objeto de la tabla. Vea [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **object_id** es la clave de esta vista.||  
|state|**nvarchar(40)**|El estado de la memoria caché de la tabla replicada para esta tabla.|' ', ' Ready '|  
  
## <a name="example"></a>Ejemplo
En este ejemplo se combina sys.pdw_replicated_table_cache_state con sys. Tables para recuperar el nombre de la tabla y el estado de la memoria caché de la tabla replicada.

```sql
SELECT t.[name], p.[object_id], p.[state]
  FROM sys.pdw_replicated_table_cache_state p 
  JOIN sys.tables t ON t.object_id = p.object_id
```



## <a name="next-steps"></a>Pasos siguientes  
 Para obtener una lista de todas las vistas de catálogo de Azure Synapse Analytics y almacenamiento de datos paralelos, consulte [SQL Data Warehouse y las vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md).   
  
