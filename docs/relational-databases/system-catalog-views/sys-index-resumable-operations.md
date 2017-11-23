---
title: Sys.index_resumable_operations (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: 
caps.latest.revision: "1"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb2d574822922598524458e9e5a5fe45638a178e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**Sys.index_resumable_operations** es una vista de sistema que supervisa y comprueba el estado de ejecución actual para la reconstrucción de índices reanudable.  
**Se aplica a**: SQL Server 2017 y Azure base de datos SQL 
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. del objeto al que pertenece (que no acepta valores NULL) en este índice.|  
|**index_id**|**int**|Id. del índice (no acepta valores NULL). **index_id** es único solo dentro del objeto.|
|**Nombre**|**sysname**|Nombre del índice. **nombre** es único solo dentro del objeto.|  
|**sql_text**|**nvarchar(max)**|Texto de la instrucción DDL T-SQL|
|**last_max_dop**|**smallint**|MAX_DOP usa la última (valor predeterminado = 0)|
|**número_de_partición**|**int**|Número de partición en el índice o montón propietario. Para índices y tablas sin particiones o en caso de todas las particiones se va a volver a generar el valor de esta columna es NULL.|
|**estado**|**tinyint**|Estado operativo de índice reanudable:<br /><br />0 = en ejecución<br /><br />1 = pausa|
|**state_desc**|**nvarchar (60)**|Descripción del estado operativo para reanudable índice (en ejecución o en pausa)|  
|**start_time**|**datetime**|Hora de inicio de operación de índice (no acepta valores NULL)|
|**last_pause_time**|**DateTime**| Último tiempo de pausa (admite valores NULL) de la operación de índice. Es NULL si la operación se ejecutan y nunca en pausa.|
|**total_execution_time**|**int**|Tiempo de ejecución total de tiempo de inicio en minutos (no acepta valores NULL)|
|**percent_complete**|**real**|Realización de progreso de la operación de índice en % (que no acepta valores NULL).|
|**page_count**|**bigint**|Número total de páginas de índice asignadas por la operación de generación de índice para el nuevo e índices de asignación (que no acepta valores NULL). 

## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
   
## <a name="example"></a>Ejemplo  
 Enumerar todas las operaciones de regeneración de índice reanudables que están en el estado de pausa. 
  
```  
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```  
  
## <a name="see-also"></a>Vea también 
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)    
 [Vistas de catálogo &#40; Transact-SQL &#41; ](catalog-views-transact-sql.md) [Objeto vistas de catálogo &#40; Transact-SQL &#41; ](object-catalog-views-transact-sql.md) [sys.indexes &#40; Transact-SQL &#41; ](sys-xml-indexes-transact-sql.md) [sys.index_columns &#40; Transact-SQL &#41;](sys-index-columns-transact-sql.md)   
 [Sys.xml_indexes &#40; Transact-SQL &#41;](sys-xml-indexes-transact-sql.md)   
 [Sys.Objects &#40; Transact-SQL &#41;](sys-index-columns-transact-sql.md)   
 [Sys.key_constraints &#40; Transact-SQL &#41;](sys-key-constraints-transact-sql.md)   
 [Sys.FileGroups &#40; Transact-SQL &#41;](sys-filegroups-transact-sql.md)   
 [Sys.partition_schemes &#40; Transact-SQL &#41;](sys-partition-schemes-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](querying-the-sql-server-system-catalog-faq.md)   
  
