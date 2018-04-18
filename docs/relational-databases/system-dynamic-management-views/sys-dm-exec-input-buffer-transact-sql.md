---
title: Sys.dm_exec_input_buffer (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 10/13/2017
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
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c22a13e5bbb9aa8d742272515ae9fd882623596d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmexecinputbuffer-transact-sql"></a>sys.dm_exec_input_buffer (Transact-SQL)
[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de las instrucciones enviadas a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_exec_input_buffer ( session_id , request_id )
```  
  
## <a name="arguments"></a>Argumentos  
*session_id*  
Es el identificador de sesión ejecutando el lote que se va a buscar. *session_id* es **smallint**. *session_id* puede obtenerse de los siguientes objetos de administración dinámica:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)   
  
*request_id*  
El request_id de [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md). *request_id* es **int**.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**event_type**|**nvarchar(256)**|El tipo de evento en el búfer de entrada para el spid determinado.|  
|**parameters**|**smallint**|Los parámetros proporcionados para la instrucción.|  
|**event_info**|**nvarchar(max)**|El texto de la instrucción en el búfer de entrada para el spid determinado.|  
  
## <a name="permissions"></a>Permissions  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el usuario tiene permiso VIEW SERVER STATE, el usuario verá las sesiones en ejecución todo en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; de lo contrario, el usuario verá solo la sesión actual.  
  
 En [!INCLUDE[ssSDS](../../includes/sssds-md.md)], si el usuario es el propietario de la base de datos, el usuario verá las sesiones en ejecución todo en el [!INCLUDE[ssSDS](../../includes/sssds-md.md)]; en caso contrario, el usuario verá solo la sesión actual.  
  
## <a name="remarks"></a>Comentarios  
 Esta función de administración dinámica puede utilizarse junto con sys.dm_exec_sessions o sys.dm_exec_requests de manera práctica **CROSS APPLY**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
 En el ejemplo siguiente se muestra cómo pasar un identificador de sesión (SPID) y un identificador de solicitud a la función.  
  
```sql  
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```  
  
### <a name="b-using-cross-apply-to-additional-information"></a>B. Con la entre aplicar a información adicional  
 En el ejemplo siguiente se muestra el búfer de entrada para las sesiones con Id. de sesión mayor que 50.  
  
```sql  
SELECT es.session_id, ib.event_info   
FROM sys.dm_exec_sessions AS es  
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib  
WHERE es.session_id > 50;
GO
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
