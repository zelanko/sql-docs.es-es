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
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 76b5f9ec684b4733934a8cdd703942f12cf1b541
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97404501"
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
 Para obtener una lista de todas las vistas de catálogo de Azure Synapse Analytics y almacenamiento de datos paralelos, consulte [vistas de catálogo de Azure Synapse Analytics y almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md).   
  
