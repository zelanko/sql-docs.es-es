---
title: Vistas del sistema, procedimientos almacenados, las DMV y tipos de espera para OLTP en memoria | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: efaa59e3-dbfa-407f-b1aa-cb0c6602ea17
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: a4e50744a716e42e0fd2767ec9cc677b2ccc085f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201203"
---
# <a name="system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp"></a>Vistas del sistema, procedimientos almacenados, tipos de espera para OLTP en memoria y DMV
  En este tema se ofrecen vínculos y breves descripciones a los múltiples objetos de base de datos que admiten OLTP en memoria.  
  
### <a name="system-views"></a>Vistas del sistema  
  
|Vista del sistema|Descripción|Característica de OLTP en memoria|  
|-----------------|-----------------|-----------------------------|  
|[sys.data_spaces &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-data-spaces-transact-sql)|Compruebe si un grupo de archivos contiene datos optimizados en memoria.|Las siguientes columnas muestran valores adicionales: **tipo** y **type_desc**.|  
|[sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)|Compruebe si un índice se encuentra en una tabla optimizada en memoria.|Las siguientes columnas muestran valores adicionales: **tipo** y **type_desc**.|  
|[sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)|Compruebe si un parámetro no admite valores NULL (para que la ejecución de un procedimiento almacenado compilado de forma nativa sea más eficaz).|**is_nullable** columna.|  
|[Sys.all_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-all-sql-modules-transact-sql)|Compruebe si un procedimiento almacenado se compila de forma nativa.|**uses_native_compilation** columna.|  
|[sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)|Compruebe si un procedimiento almacenado se compila de forma nativa.|**uses_native_compilation** columna.|  
|[Sys.table_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-table-types-transact-sql)|Compruebe si una tabla está optimizada en memoria.|**is_memory_optimized** columna.|  
|[sys.tables &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)|Compruebe si una tabla está optimizada en memoria y la configuración de durabilidad de una tabla.|**durabilidad**, **durability_desc**, y **is_memory_optimized** columnas.|  
|[sys.hash_indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-hash-indexes-transact-sql)|Muestre los índices hash de una tabla optimizada en memoria.|OLTP en memoria específico.|  
  
### <a name="metadata-functions"></a>Funciones de metadatos  
  
|Función de metadatos|Descripción|Característica de OLTP en memoria|  
|-----------------------|-----------------|-----------------------------|  
|[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/objectproperty-transact-sql)|Compruebe si los objetos de base de datos están optimizadas en memoria.|**ExecIsWithNativeCompilation** y **TableIsMemoryOptimized** propiedades.<br /><br /> El **IsSchemaBound** propiedad es compatible con el tipo de objeto de procedimiento (devuelve 0 para los procedimientos en lugar de NULL).|  
|[SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)|Compruebe si un servidor admite OLTP en memoria.|**IsXTPSupported** propiedad.|  
  
### <a name="system-stored-procedures"></a>Procedimientos almacenados del sistema  
  
|Procedimiento almacenado|Descripción|  
|----------------------|-----------------|  
|[Sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)|Enlaza una base de datos OLTP en memoria a un grupo de recursos.|  
|[Sys.sp_xtp_checkpoint_force_garbage_collection &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-checkpoint-force-garbage-collection-transact-sql)|Inicia la recopilación de elementos no utilizados en una base de datos OLTP en memoria.|  
|[Sys.sp_xtp_control_proc_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-proc-exec-stats-transact-sql)|Habilita la recopilación de estadísticas para los procedimientos almacenados compilados de forma nativa|  
|[Sys.sp_xtp_control_query_exec_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql)|Habilita la recopilación de estadísticas por consulta para los procedimientos almacenados compilados de forma nativa|  
|[Sys.sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql)|Combina archivos delta y de datos.|  
|[Sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)|Quita el enlace entre una base de datos y un grupo de recursos.|  
  
## <a name="dynamic-management-views-dmvs"></a>Vistas de administración dinámica (DMV)  
 Hay varias DMV para tablas optimizadas en memoria.  
  
 Para obtener más información, consulte [vistas de administración dinámica tabla con optimización para memoria &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql).  
  
## <a name="wait-types"></a>Tipos de espera  
 Hay varios tipos de espera que admiten OLTP en memoria.  
  
 Para obtener más información, vea tipos de espera que tienen el prefijo **WAIT_XTP**, y **XTPPROC** en el [sys.dm_os_wait_stats &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql) tema.  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)   
 [Compatibilidad de Transact-SQL con OLTP en memoria](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
