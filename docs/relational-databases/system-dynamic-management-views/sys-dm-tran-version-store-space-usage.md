---
title: Sys.dm_tran_version_store_space_usage (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: "10"
author: savjani
ms.author: pariks
manager: ajayj
ms.workload: Inactive
ms.openlocfilehash: cfdd2caa03fdd12501580c2584d68f374ee54222
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>Sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Devuelve una tabla que muestra el total de espacio en tempdb usado por los registros del almacén de versión para cada base de datos. **Sys.dm_tran_version_store_space_usage** es eficaz y eficiente para que se ejecute como no vaya a través del almacén de versiones individuales registra y devuelve el espacio de almacén de versiones agregado utilizado en tempdb por base de datos.
  
Cada registro de versión se almacena como datos binarios junto con alguna información de estado o seguimiento. Al igual que los registros en tablas de base de datos, los registros del almacén de versiones se almacenan en páginas de 8.192 bytes. Si un registro supera los 8.192 bytes, se dividirá en dos registros diferentes.  
  
Puesto que el registro de versiones se almacena como binario, no existen problemas con las diferentes intercalaciones de bases de datos distintas. Use **sys.dm_tran_version_store_space_usage** para supervisar y planear el tamaño tempdb según el uso del espacio de almacén de versión de las bases de datos en una instancia de SQL Server.
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de base de datos de la base de datos.|  
|**reserved_page_count**|**bigint**|Número total de las páginas reservadas en tempdb para versión almacenar los registros de la base de datos.|  
|**reserved_space_kb**|**bigint**|Espacio total utilizado en kilobytes en tempdb para versión almacenar los registros de la base de datos.|  
  
## <a name="permissions"></a>Permissions  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   

## <a name="examples"></a>Ejemplos  
 La siguiente consulta se puede utilizar para determinar el espacio utilizado en tempdb por el almacén de versiones de cada base de datos en una instancia de SQL Server. 
  
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
  
