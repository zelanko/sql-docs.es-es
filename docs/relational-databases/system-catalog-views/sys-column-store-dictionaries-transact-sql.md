---
title: Sys.column_store_dictionaries (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.column_store_dictionaries_TSQL
- column_store_dictionaries
- column_store_dictionaries_TSQL
- sys.column_store_dictionaries
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_dictionaries catalog view
ms.assetid: 56efd563-2f72-4caf-94e3-8a182385c173
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e540f8bea10bb627554ebee15254112e3e4d71c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syscolumnstoredictionaries-transact-sql"></a>sys.column_store_dictionaries (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada diccionario que se utilice en los índices de almacén de columnas optimizados en memoria xVelocity. Los diccionarios se usan para codificar algunos tipos de datos (no todos), por tanto no todas las columnas en un índice de almacén de columnas tienen diccionarios. Un diccionario puede ser un diccionario primario, para todos los segmentos, y posiblemente para otros diccionarios que se usan para un subconjunto de los segmentos de la columna.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**hobt_id**|**bigint**|Identificador del montón o el índice de árbol b (hobt) para la tabla que contiene este índice de almacén de columnas.|  
|**column_id**|**int**|Identificador de la columna de almacén de columnas a partir de 1. La primera columna tiene un identificador = 1, la segunda columna tiene un identificador = 2, etcetera.|  
|**dictionary_id**|**int**|Puede haber dos tipos de diccionarios, globales y locales, asociados a un segmento de columna. Un dictionary_id 0 representa el diccionario global que se comparte entre todos los segmentos columna (uno para cada grupo de filas) para esa columna.|  
|**version**|**int**|Versión del formato de diccionario.|  
|**tipo**|**int**|Tipo de diccionario:<br /><br /> 1 – diccionario que contiene de hash **int** valores<br /><br /> 2 - No se utiliza<br /><br /> 3 - Diccionario hash que contiene valores de cadena<br /><br /> 4-diccionario que contiene de hash de **float** valores<br /><br /> Para obtener más información acerca de los diccionarios, vea [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md).|  
|**last_id**|**int**|El último identificador de datos en el diccionario.|  
|**entry_count**|**bigint**|Número de entradas en el diccionario.|  
|**on_disc_size**|**bigint**|Tamaño del diccionario en bytes.|  
|**partition_id**|**bigint**|Indica el identificador de partición. Es único en una base de datos.|  
  
## <a name="permissions"></a>Permissions  
 Todas las columnas necesitan al menos el permiso VIEW DEFINITION en la tabla. Las columnas siguientes devuelven null a menos que el usuario también tenga **seleccione** permiso: last_id, entry_count, data_ptr.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.ALL_COLUMNS &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys.computed_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [Guía de índices de almacén de columnas](~/relational-databases/indexes/columnstore-indexes-overview.md)   
 [sys.column_store_segments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

