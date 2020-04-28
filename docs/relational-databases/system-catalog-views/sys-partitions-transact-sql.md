---
title: Sys. partitions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2531dde9237734d3c6eb4b3ea96ed2ac18e9d399
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73982800"
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada partición de todas las tablas y la mayoría de los tipos de índices de la base de datos. En esta vista no se incluyen los tipos de índice especiales, como texto completo, espacial y XML. Todas las tablas e índices de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contienen al menos una partición, ya sea explícita o no.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|Indica el identificador de partición. Es único en una base de datos.|  
|object_id|**int**|Indica el identificador del objeto al que pertenece esta partición. Todas las tablas o vistas se componen al menos de una partición.|  
|index_id|**int**|Indica el identificador del índice dentro del objeto al que pertenece esta partición.<br /><br /> 0 = montón<br />1 = índice clúster<br />2 o superior = índice no clúster|  
|partition_number|**int**|Es un número de partición basado en uno en el índice o el montón propietario. Para las tablas y los índices sin particiones, el valor de esta columna es 1.|  
|hobt_id|**bigint**|Indica el identificador de la montículo o árbol B de datos (HoBT) que contiene las filas de esta partición.|  
|rows|**bigint**|Indica el número aproximado de filas de esta partición.|  
|filestream_filegroup_id|**smallint**|**Válido para** : [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.<br /><br /> Indica el identificador del grupo de archivos FILESTREAM almacenado en esta partición.|  
|data_compression|**tinyint**|Indica el estado de compresión para cada partición:<br /><br /> 0 = NONE <br />1 = ROW <br />2 = PAGE <br />3 = almacén de columnas: **se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores<br />4 = COLUMNSTORE_ARCHIVE: **se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores<br /><br /> **Nota:** Los índices de texto completo se comprimirán en cualquier edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|data_compression_desc|**nvarchar(60)**|Indica el estado de compresión para cada partición. Los valores posibles para las tablas de almacén de filas son NONE, ROW y PAGE. Los valores posibles para tablas de almacén de columnas son COLUMNSTORE y COLUMNSTORE_ARCHIVE.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar las preguntas más frecuentes (P+F) del catálogo del sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
