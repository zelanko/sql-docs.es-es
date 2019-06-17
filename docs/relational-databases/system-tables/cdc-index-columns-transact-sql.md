---
title: cdc.index_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d47de7882a6eeeca72ad0da8521ab298c7ea8364
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471213"
---
# <a name="cdcindexcolumns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada columna de índice asociada a una tabla de cambios. La captura de datos modificados usa las columnas de índice para identificar de manera única las filas en la tabla de origen. De forma predeterminada, se incluyen las columnas de la clave principal de la tabla de origen. Sin embargo, si en la tabla de origen se especifica un índice único cuando la captura de datos modificados está habilitada en la tabla de origen, se utilizan las columnas en dicho índice en su lugar. Se requiere una clave principal o un índice único en la tabla de origen si se habilita el seguimiento de cambios de la red. Para obtener más información, consulte [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Se recomienda que no consulte directamente las tablas del sistema. En su lugar, ejecute el [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) procedimiento almacenado.  

  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla de cambios.|  
|**column_name**|**sysname**|Nombre de la columna de índice.|  
|**index_ordinal**|**tinyint**|Ordinal (basado en 1) de la columna en el índice.|  
|**column_id**|**int**|Id. de la columna en la tabla de origen.|  
  
## <a name="see-also"></a>Vea también  
 [cdc.change_tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
