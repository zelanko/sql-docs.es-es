---
title: CDC.captured_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e0f4ff663a64e2de3fa7a8247eee170907d1a624
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="cdccapturedcolumns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada columna de la que se ha realizado un seguimiento en una instancia de captura. De forma predeterminada, se capturan todas las columnas de la tabla de origen. Sin embargo, se podrán incluir o excluir columnas si la tabla de origen está habilitada para la captura de datos modificados especificando una lista de columnas. Para obtener más información, consulte [sys.sp_cdc_enable_table &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Se recomienda **no consultar directamente las tablas del sistema**. En su lugar, ejecute el [sys.sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) procedimiento almacenado.  
   
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla de origen a la que pertenece la columna capturada.|  
|**column_name**|**sysname**|Nombre de la columna capturada.|  
|**column_id**|**int**|Id. de la columna capturada dentro de la tabla de origen.|  
|**COLUMN_TYPE**|**sysname**|Tipo de columna capturada.|  
|**column_ordinal**|**int**|Ordinal de columna (basado en 1) en la tabla de cambios. Se excluyen las columnas de metadatos de la tabla de cambios. El ordinal 1 está asignado a la primera columna capturada.|  
|**is_computed**|**bit**|Indica que la columna capturada es una columna calculada en la tabla de origen.|  
  
## <a name="see-also"></a>Vea también  
 [CDC.change_tables &#40; Transact-SQL &#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
