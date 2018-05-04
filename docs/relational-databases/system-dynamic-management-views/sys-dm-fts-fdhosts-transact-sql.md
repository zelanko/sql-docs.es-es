---
title: Sys.dm_fts_fdhosts (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/29/2017
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
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b4bc446dbcf3b896dca1b33789cfd1f0f1e89ff9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmftsfdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre la actividad actual de los host de demonio de filtro en la instancia de servidor.  
  
 
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|Id. del host de demonio de filtro.|  
|**fdhost_name**|**nvarchar(120)**|Nombre del host de demonio de filtro.|  
|**fdhost_process_id**|**int**|Id. de proceso de Windows del host de demonio de filtro.|  
|**fdhost_type**|**nvarchar(120)**|Tipo de documento que procesa el host de demonio de filtro, que puede ser uno de los siguientes:<br /><br /> Subproceso único<br /><br /> Varios subprocesos<br /><br /> Documento gigante|  
|**max_thread**|**int**|Número máximo de subprocesos del host de demonio de filtro.|  
|**batch_count**|**int**|Número de lotes que se procesan en el host de demonio de filtro.|  
  
## <a name="permissions"></a>Permissions  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el nombre del host de demonio de filtro y el número máximo de subprocesos que contiene. También supervisa el número de lotes que se procesan actualmente en el demonio de filtro. Esta información se puede utilizar para evaluar el rendimiento.  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
