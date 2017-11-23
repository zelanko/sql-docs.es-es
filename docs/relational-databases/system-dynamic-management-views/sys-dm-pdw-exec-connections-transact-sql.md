---
title: Sys.dm_pdw_exec_connections (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 2625466b-d0ef-4c71-bedc-6d13491a8351
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2020dc2ccf50b9e6ed11c609f908e346c469c8d7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwexecconnections-transact-sql"></a>Sys.dm_pdw_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve información acerca de las conexiones establecidas con esta instancia de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y los detalles de cada conexión.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|Identifica la sesión asociada a esta conexión. Use `SESSION_ID()` para devolver el `session_id` de la conexión actual.|  
|connect_time|**datetime**|Marca de tiempo en que se estableció la conexión. No admite valores NULL.|  
|encrypt_option|**nvarchar (40)**|Indica TRUE (la conexión está cifrada) o FALSE (conexión no es enctypred).|  
|auth_scheme|**nvarchar (40)**|Especifica el esquema de autenticación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Windows usado en esta conexión. No admite valores NULL.|  
|client_id|**varchar(48)**|Dirección IP del cliente que se conecta a este servidor. Acepta valores NULL.|  
|sql_spid|**int**|Id. de proceso de servidor de la conexión. Use `@@SPID` para devolver el `sql_spid` de la conexión actual. Con fines más, utilice el `session_id` en su lugar.|  
  
## <a name="permissions"></a>Permissions  
 Requiere **VIEW SERVER STATE** permiso en el servidor.  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
||||  
|-|-|-|  
|dm_pdw_exec_sessions.session_ID|dm_pdw_exec_connections.session_ID|Uno a uno|  
|dm_pdw_exec_requests.connection_id|dm_pdw_exec_connections.connection_id|Varios a uno|  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 Consulta típica para recopilar información sobre una conexión solo para consultas.  
  
```  
SELECT  
    c.session_id, c.encrypt_option,  
    c.auth_scheme, s.client_id, s.login_name,   
    s.status, s.query_count  
FROM sys.dm_pdw_exec_connections AS c  
JOIN sys.dm_pdw_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = SESSION_ID();  
```  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  

