---
title: Sys.pdw_nodes_indexes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 261bcb7f-a906-4979-b274-bc5f1aa66426
caps.latest.revision: "7"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a9dcf0c5cc21d01359c13f13b33914d73a0a7b5f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="syspdwnodesindexes-transact-sql"></a>Sys.pdw_nodes_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve los índices para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|Id. del objeto al que pertenece este índice.||  
|name|**sysname**|Nombre del índice. Nombre es único solo dentro del objeto. NULL = Montón||  
|index_id|**int**|Id. del índice. index_ID es exclusivo solo dentro del objeto.<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster<br /><br /> > 1 = índice no clúster||  
|Tipo|**tinyint**|Tipo de índice:<br /><br /> 0 = Montón<br /><br /> 1 = Clúster<br /><br /> 2 = no clúster<br /><br /> 5 = índice clúster de almacén de columnas optimizado de memoria de xVelocity|  
|type_desc|**nvarchar (60)**|Descripción del tipo de índice:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> ALMACÉN DE COLUMNAS AGRUPADO||  
|is_unique|**bit**|0 = El índice no es exclusivo.|Siempre es 0.|  
|data_space_id|**int**|Id. del espacio de datos para este índice. El espacio de datos es un grupo de archivos o un esquema de partición.<br /><br /> 0 = object_id es una función con valores de tabla.||  
|ignore_dup_key|**bit**|0 = IGNORE_DUP_KEY está OFF.|Siempre es 0.|  
|is_primary_key|**bit**|1 = El índice forma parte de una restricción PRIMARY KEY.|Siempre es 0.|  
|is_unique_constraint|**bit**|1 = El índice forma parte de una restricción UNIQUE.|Siempre es 0.|  
|fill_factor|**tinyint**|> 0 = Porcentaje de FILLFACTOR utilizado al crear o volver a generar el índice.<br /><br /> 0 = Valor predeterminado|Siempre es 0.|  
|is_padded|**bit**|0 = PADINDEX está OFF.|Siempre es 0.|  
|is_disabled|**bit**|1 = El índice está deshabilitado.<br /><br /> 0 = El índice no está deshabilitado.||  
|is_hypothetical|**bit**|0 = El índice no es hipotético.|Siempre es 0.|  
|allow_row_locks|**bit**|1 = El índice admite bloqueos de fila.|Siempre es 1.|  
|allow_page_locks|**bit**|1 = El índice admite bloqueos de página.|Siempre es 1.|  
|has_filter|**bit**|0 = El índice no tiene un filtro.|Siempre es 0.|  
|filter_definition|**nvarchar(max)**|Expresión para el subconjunto de filas incluido en el índice filtrado.|Siempre es NULL.|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|NOT NULL|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
