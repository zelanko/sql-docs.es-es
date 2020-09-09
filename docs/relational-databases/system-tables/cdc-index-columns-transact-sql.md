---
description: cdc.index_columns (Transact-SQL)
title: CDC. index_columns (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5cf09c3a66a3db1b7275dfe8017d953aaf57b42d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544649"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve una fila para cada columna de índice asociada a una tabla de cambios. La captura de datos modificados usa las columnas de índice para identificar de manera única las filas en la tabla de origen. De forma predeterminada, se incluyen las columnas de la clave principal de la tabla de origen. Sin embargo, si en la tabla de origen se especifica un índice único cuando la captura de datos modificados está habilitada en la tabla de origen, se utilizan las columnas en dicho índice en su lugar. Se requiere una clave principal o un índice único en la tabla de origen si se habilita el seguimiento de cambios de la red. Para obtener más información, vea [Sys. sp_cdc_enable_table &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Se recomienda que no consulte directamente las tablas del sistema. En su lugar, ejecute el procedimiento almacenado [Sys. sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) .  

  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla de cambios.|  
|**column_name**|**sysname**|Nombre de la columna de índice.|  
|**index_ordinal**|**tinyint**|Ordinal (basado en 1) de la columna en el índice.|  
|**column_id**|**int**|Id. de la columna en la tabla de origen.|  
  
## <a name="see-also"></a>Consulte también  
 [CDC. change_tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
