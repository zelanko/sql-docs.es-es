---
title: CDC.index_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs: TSQL
helpviewer_keywords: cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c5c451887887d687b1f302f59f1fc394bf86b8e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="cdcindexcolumns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada columna de índice asociada a una tabla de cambios. La captura de datos modificados usa las columnas de índice para identificar de manera única las filas en la tabla de origen. De forma predeterminada, se incluyen las columnas de la clave principal de la tabla de origen. Sin embargo, si en la tabla de origen se especifica un índice único cuando la captura de datos modificados está habilitada en la tabla de origen, se utilizan las columnas en dicho índice en su lugar. Se requiere una clave principal o un índice único en la tabla de origen si se habilita el seguimiento de cambios de la red. Para obtener más información, consulte [sys.sp_cdc_enable_table &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Se recomienda que no consulte directamente las tablas del sistema. En su lugar, ejecute el [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) procedimiento almacenado.  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla de cambios.|  
|**column_name**|**sysname**|Nombre de la columna de índice.|  
|**index_ordinal**|**tinyint**|Ordinal (basado en 1) de la columna en el índice.|  
|**column_id**|**int**|Id. de la columna en la tabla de origen.|  
  
## <a name="see-also"></a>Vea también  
 [CDC.change_tables &#40; Transact-SQL &#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
