---
title: Sys. hash_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.hash_indexes_TSQL
- hash_indexes
- sys.hash_indexes
- hash_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.hash_indexes catalog view
ms.assetid: d9e230fb-d3ff-486f-86ef-44898f0a703e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7090c0ac52f82c0840c7bc36f91d146a121b1854
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828511"
---
# <a name="syshash_indexes-transact-sql"></a>sys.hash_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra los índices hash actuales y las propiedades del índice hash. Los índices hash solo se admiten en [OLTP en memoria &#40;la optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
 La vista sys. hash_indexes contiene las mismas columnas que la vista sys. Indexes y una columna adicional denominada **bucket_count**. Para obtener más información acerca de las demás columnas de la vista sys. hash_indexes, vea [Sys. indexes &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<columnas heredadas>**||Hereda columnas de [Sys. indexes &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|**bucket_count**|**int**|Número de depósitos de hash para los índices hash.<br /><br /> Para obtener más información sobre el valor de bucket_count, incluidas las instrucciones para establecer el valor, vea [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)].  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
  
```  
SELECT object_name([object_id]) AS 'table_name', [object_id],  
     [name] AS 'index_name', [type_desc], [bucket_count]   
FROM sys.hash_indexes   
WHERE OBJECT_NAME([object_id]) = 'T1';  
```  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
