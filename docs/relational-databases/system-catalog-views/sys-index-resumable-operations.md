---
title: sys.index_resumable_operations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 780cffa17f6ee1af70d942545632c98c9d6dc1e7
ms.sourcegitcommit: ad3b2133585bc14fc6ef8be91f8b74ee2f498b64
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/20/2019
ms.locfileid: "56425780"
---
# <a name="indexresumableoperations-transact-sql"></a>index_resumable_operations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**Sys.index_resumable_operations** es una vista de sistema que supervisa y comprueba el estado de ejecución actual para la reconstrucción de índices reanudable.  
**Se aplica a**: SQL Server 2017 y Azure SQL Database
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece (que no acepta valores NULL) este índice.|  
|**index_id**|**int**|Id. del índice (no acepta valores NULL). **index_id** es único solo dentro del objeto.|
|**Nombre**|**sysname**|Nombre del índice. **nombre** es único solo dentro del objeto.|  
|**sql_text**|**nvarchar(max)**|Texto de la instrucción DDL de T-SQL|
|**last_max_dop**|**smallint**|Última MAX_DOP usa (predeterminado = 0)|
|**partition_number**|**int**|Número de partición en el índice o montón propietario. Para tablas sin particiones e índices, o en caso de todas las particiones son que se va a volver a generar el valor de esta columna es NULL.|
|**state**|**tinyint**|Estado operativo de índices reanudables:<br /><br />0 = en ejecución<br /><br />1 = pausa|
|**state_desc**|**nvarchar(60)**|Descripción del estado operativo de índice reanudable (en ejecución o en pausa)|  
|**start_time**|**datetime**|Hora de inicio de operación de índice (no acepta valores NULL)|
|**last_pause_time**|**datatime**| Operación de índice último tiempo de pausa (que aceptan valores NULL). Es NULL si la operación está en ejecución y nunca en pausa.|
|**total_execution_time**|**int**|Tiempo de ejecución total de tiempo de inicio en minutos (no acepta valores NULL)|
|**percent_complete**|**real**|Finalización de progreso de operación de índice en % (que no acepta valores NULL).|
|**page_count**|**bigint**|Número total de páginas de índice asignadas por la operación de generación de índice para el nuevo e índices de asignación (que no acepta valores NULL).

## <a name="permissions"></a>Permisos

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  

## <a name="example"></a>Ejemplo

 Enumera todas las operaciones de regeneración de índices reanudables que se encuentran en el estado de pausa.

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>Vea también

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [Vistas de catálogo](catalog-views-transact-sql.md)
- [Vistas de catálogo de objetos](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](querying-the-sql-server-system-catalog-faq.md)
