---
title: CDC. captured_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1a635ab2284a413fb3a4cf9e11b9f40e0369f958
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832453"
---
# <a name="cdccaptured_columns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada columna de la que se ha realizado un seguimiento en una instancia de captura. De forma predeterminada, se capturan todas las columnas de la tabla de origen. Sin embargo, se podrán incluir o excluir columnas si la tabla de origen está habilitada para la captura de datos modificados especificando una lista de columnas. Para obtener más información, vea [Sys. sp_cdc_enable_table &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 Se recomienda **no consultar directamente las tablas del sistema**. En su lugar, ejecute el procedimiento almacenado [Sys. sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md) .  
   
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de la tabla de origen a la que pertenece la columna capturada.|  
|**column_name**|**sysname**|Nombre de la columna capturada.|  
|**column_id**|**int**|Id. de la columna capturada dentro de la tabla de origen.|  
|**column_type**|**sysname**|Tipo de columna capturada.|  
|**column_ordinal**|**int**|Ordinal de columna (basado en 1) en la tabla de cambios. Se excluyen las columnas de metadatos de la tabla de cambios. El ordinal 1 está asignado a la primera columna capturada.|  
|**is_computed**|**bit**|Indica que la columna capturada es una columna calculada en la tabla de origen.|  
  
## <a name="see-also"></a>Consulte también  
 [CDC. change_tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
