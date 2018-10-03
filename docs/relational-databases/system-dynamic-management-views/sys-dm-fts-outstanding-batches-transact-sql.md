---
title: Sys.dm_fts_outstanding_batches (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6903c5eeb18cad271eb6f9e7ba1671380112ebe9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47594673"
---
# <a name="sysdmftsoutstandingbatches-transact-sql"></a>sys.dm_fts_outstanding_batches (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información acerca de cada lote de indización de texto completo.  
  
  |Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Id. de la base de datos|  
|catalog_id|**int**|Id. del catálogo de texto completo|  
|table_id|**int**|Id. del identificador de tabla que contiene el índice de texto completo.|  
|batch_id|**int**|Identificador de lote|  
|memory_address|**varbinary (8)**|Dirección de memoria del objeto de lote.|  
|crawl_memory_address|**varbinary (8)**|Dirección de memoria del objeto de rastreo (objeto primario)|  
|memregion_memory_address|**varbinary (8)**|Dirección del área de memoria de la memoria compartida saliente del host de demonio del filtro (fdhost.exe)|  
|hr_batch|**int**|Código de error más reciente del lote|  
|is_retry_batch|**bit**|Indica si el lote es un lote de reintento:<br /><br /> 0 = No<br /><br /> 1 = Sí|  
|retry_hints|**int**|Tipo de reintento requerido para el lote:<br /><br /> 0 = Sin reintento<br /><br /> 1 = Reintento de varios subprocesos<br /><br /> 2 = Reintento de subproceso único<br /><br /> 3 = Reintento de subproceso único y de varios subprocesos<br /><br /> 5 = Reintento final de varios subprocesos<br /><br /> 6 = Reintento final de subproceso único<br /><br /> 7 = Reintento final de subproceso único y de varios subprocesos|  
|retry_hints_description|**nvarchar(120)**|Descripción del tipo de reintento requerido:<br /><br /> NO RETRY<br /><br /> MULTI THREAD RETRY<br /><br /> SINGLE THREAD RETRY<br /><br /> SINGLE AND MULTI THREAD RETRY<br /><br /> MULTI THREAD FINAL RETRY<br /><br /> SINGLE THREAD FINAL RETRY<br /><br /> SINGLE AND MULTI THREAD FINAL RETRY|  
|doc_failed|**bigint**|Número de documentos que generaron errores en el lote|  
|batch_timestamp|**timestamp**|El valor de marca de tiempo obtenido al crear el lote|  
  
## <a name="permissions"></a>Permisos  

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se determina el número de lotes que se están procesando actualmente para cada una de las tablas de la instancia de servidor.  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
