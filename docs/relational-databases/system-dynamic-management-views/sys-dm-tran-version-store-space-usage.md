---
title: Sys.dm_tran_version_store_space_usage (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 10
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: fbfc968d9fb4620884f282121a820dad548405cc
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Devuelve una tabla que muestra el total de espacio en tempdb usado por los registros del almacén de versión para cada base de datos. **Sys.dm_tran_version_store_space_usage** es eficaz y económica que se ejecuta, tal y como no navegar por los registros de almacén de versión individual, y se devuelve agrega espacio de almacén de versión utilizado en tempdb por base de datos.
  
Cada registro de versión se almacena como datos binarios, junto con cierta información de estado o seguimiento. Al igual que los registros en tablas de base de datos, los registros del almacén de versiones se almacenan en páginas de 8.192 bytes. Si un registro supera los 8.192 bytes, se dividirá en dos registros diferentes.  
  
Puesto que el registro de versiones se almacena como binario, no existen problemas con las diferentes intercalaciones de bases de datos distintas. Use **sys.dm_tran_version_store_space_usage** para supervisar y planear el tamaño tempdb según el uso del espacio de almacén de versión de las bases de datos en una instancia de SQL Server.
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de base de datos de la base de datos.|  
|**reserved_page_count**|**bigint**|Número total de las páginas reservadas en tempdb para versión almacenar los registros de la base de datos.|  
|**reserved_space_kb**|**bigint**|Espacio total utilizado en kilobytes en tempdb para versión almacenar los registros de la base de datos.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   

## <a name="examples"></a>Ejemplos  
La siguiente consulta se puede utilizar para determinar el espacio utilizado en tempdb, por el almacén de versiones de cada base de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia. 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
