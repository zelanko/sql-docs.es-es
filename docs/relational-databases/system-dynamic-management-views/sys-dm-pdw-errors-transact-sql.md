---
title: Sys.dm_pdw_errors (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: 944eac31-5691-432b-b9f5-f1e11c05191f
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0a394c6eb050fd67da587331c1a2a20546947f64
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmpdwerrors-transact-sql"></a>Sys.dm_pdw_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todos los errores encontrados durante la ejecución de una solicitud o una consulta.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|error_id|**nvarchar(36)**|Clave para esta vista.<br /><br /> Identificador numérico único asociado con el error.|Es único entre todos los errores de consulta en el sistema.|  
|origen|**nvarchar(64)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|Tipo|**nvarchar(4000)**|Tipo de error que se produjo.|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|  
|create_time|**datetime**|Hora en que se produjo el error.|Menor o igual a la hora actual.|  
|pwd_node_id|**int**|Identificador del nodo específico implicado, si existe. Para obtener más información sobre los identificadores de nodo, vea [sys.dm_pdw_nodes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).||  
|session_id|**nvarchar (32)**|Identificador de la sesión implicada, si lo hay. Para obtener más información sobre identificadores de sesión, vea [sys.dm_pdw_exec_sessions &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md).||  
|request_id|**nvarchar (32)**|Identificador de la solicitud implicada, si lo hay. Para obtener más información sobre identificadores de solicitud, vea [sys.dm_pdw_exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).||  
|spid|**int**|SPID de la sesión de SQL Server implicada, si lo hay.||  
|thread_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|detalles|**nvarchar(4000)**|Contiene la descripción de texto de error completo.||  
  
 Para obtener información sobre el número máximo de filas conserva esta vista, vea la sección valores máximos de vista de sistema en el [valores mínimo y máximo (SQL Server PDW)](http://msdn.microsoft.com/en-us/5243f018-2713-45e3-9b61-39b2a57401b9) tema.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de administración dinámica de almacenamiento de datos en paralelo &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
