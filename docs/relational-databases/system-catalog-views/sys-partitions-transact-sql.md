---
title: Sys.partitions (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs: TSQL
helpviewer_keywords: sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
caps.latest.revision: "60"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 658d0d22bf2dc757854626f792cc49429ab98916
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Contiene una fila por cada partición de todas las tablas y la mayoría de los tipos de índices de la base de datos. Tipos de índice especiales como texto completo, espacial y XML no se incluyen en esta vista. Todas las tablas e índices de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contienen al menos una partición, ya sea explícita o no.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|Indica el identificador de partición. Es único en una base de datos.|  
|object_id|**int**|Indica el identificador del objeto al que pertenece esta partición. Todas las tablas o vistas se componen al menos de una partición.|  
|index_id|**int**|Indica el identificador del índice dentro del objeto al que pertenece esta partición.<br /><br /> 0 = montón<br />1 = índice clúster<br />2 o superior = índice no clúster|  
|partition_number|**int**|Es un número de partición basado en uno en el índice o el montón propietario. Para las tablas y los índices sin particiones, el valor de esta columna es 1.|  
|hobt_id|**bigint**|Indica el identificador del montón de datos o el árbol b que contiene las filas de esta partición.|  
|rows|**bigint**|Indica el número aproximado de filas de esta partición.|  
|filestream_filegroup_id|**smallint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Indica el identificador del grupo de archivos FILESTREAM almacenado en esta partición.|  
|data_compression|**tinyint**|Indica el estado de compresión para cada partición:<br /><br /> 0 = NONE <br />1 = ROW <br />2 = PAGE <br />3 = COLUMNSTORE: **se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br />4 = COLUMNSTORE_ARCHIVE: **se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> **Nota:** índices de texto completo se comprimirán en cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|data_compression_desc|**nvarchar (60)**|Indica el estado de compresión para cada partición. Los valores posibles para las tablas de almacén de filas son NONE, ROW y PAGE. Los valores posibles para tablas de almacén de columnas son COLUMNSTORE y COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** . Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de objetos &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
