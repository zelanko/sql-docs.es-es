---
title: Sys.dm_fts_fdhosts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: faa79f48a4f3b8ac70984c3b02c8863d7d37e8ac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47608544"
---
# <a name="sysdmftsfdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre la actividad actual de los host de demonio de filtro en la instancia de servidor.  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|Id. del host de demonio de filtro.|  
|**fdhost_name**|**nvarchar(120)**|Nombre del host de demonio de filtro.|  
|**fdhost_process_id**|**int**|Id. de proceso de Windows del host de demonio de filtro.|  
|**fdhost_type**|**nvarchar(120)**|Tipo de documento que procesa el host de demonio de filtro, que puede ser uno de los siguientes:<br /><br /> Subproceso único<br /><br /> Varios subprocesos<br /><br /> Documento gigante|  
|**max_thread**|**int**|Número máximo de subprocesos del host de demonio de filtro.|  
|**batch_count**|**int**|Número de lotes que se procesan en el host de demonio de filtro.|  
  
## <a name="permissions"></a>Permisos  

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
  
  
