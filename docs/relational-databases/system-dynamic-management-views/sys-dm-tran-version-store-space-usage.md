---
title: Sys.dm_tran_version_store_space_usage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f8ae2babba09f30b03ea512a85bdc6f06c4bf7f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688283"
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

Devuelve una tabla que muestra el espacio total en tempdb usado por los registros del almacén de versión para cada base de datos. **Sys.dm_tran_version_store_space_usage** es eficaz y económica de ejecutar, ya que no vaya a través de los registros del almacén de versión individual y devuelve agregadas espacio utilizado en tempdb por base de datos del almacén de versión.
  
Cada registro de versión se almacena como datos binarios, junto con cierta información de estado o seguimiento. Al igual que los registros en tablas de base de datos, los registros del almacén de versiones se almacenan en páginas de 8.192 bytes. Si un registro supera los 8.192 bytes, se dividirá en dos registros diferentes.  
  
Puesto que el registro de versiones se almacena como binario, no existen problemas con las diferentes intercalaciones de bases de datos distintas. Use **sys.dm_tran_version_store_space_usage** para supervisar y planear tamaño de tempdb según el uso del espacio de almacén de versión de las bases de datos en una instancia de SQL Server.
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de base de datos de la base de datos.|  
|**reserved_page_count**|**bigint**|Recuento total de las páginas reservadas en tempdb para la versión almacenar registros de la base de datos.|  
|**reserved_space_kb**|**bigint**|Espacio total usado en kilobytes en tempdb para la versión almacenar registros de la base de datos.|  
  
## <a name="permissions"></a>Permisos  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   

## <a name="examples"></a>Ejemplos  
La consulta siguiente puede utilizarse para determinar el espacio utilizado en tempdb, por almacén de versiones de cada base de datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia. 
  
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
  
