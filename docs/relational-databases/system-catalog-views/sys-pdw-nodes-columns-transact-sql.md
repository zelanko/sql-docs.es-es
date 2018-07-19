---
title: Sys.pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 20bb25d3699a6fab734da0974bc0726da7e5cb96
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38058143"
---
# <a name="syspdwnodescolumns-transact-sql"></a>Sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Muestra las columnas para las tablas definidas por el usuario y las vistas definidas por el usuario.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|Identificador del objeto al que pertenece esta columna.||  
|NAME|**sysname**|Nombre de la columna. Único objeto.||  
|column_id|**int**|Identificador de la columna. Único objeto.||  
|system_type_id|**tinyint**|Id. del tipo de sistema de la columna.||  
|user_type_id|**int**|Id. del tipo de la columna, tal como lo ha definido el usuario.||  
|max_length|**smallint**|Longitud máxima de la columna, en bytes.|Incluye -1 (no es válido) para los tipos de columna no admitido.|  
|precisión|**tinyint**|Precisión de la columna si basado en numerales; en caso contrario, es 0.||  
|escala|**tinyint**|La escala de la columna se basa en valores numéricos; en caso contrario, es 0.||  
|collation_name|**sysname**|Nombre de la intercalación de la columna si basados en caracteres; en caso contrario, es NULL.||  
|is_nullable|**bit**|1 = La columna acepta valores NULL.||  
|is_ansi_padded|**bit**|1 = La columna utiliza el comportamiento ANSI_PADDING ON si es de tipo character, binary o variant.|Siempre es 0.|  
|is_rowguidcol|**bit**|1 = La columna se ha declarado como ROWGUIDCOL.|Siempre es 0.|  
|is_identity|**bit**|1 = columna tiene valores de identidad.|Siempre es 0.|  
|is_computed|**bit**|1 = La columna es una columna calculada.|Siempre es 0.|  
|is_filestream|**bit**|1 = La columna es una columna FILESTREAM.|Siempre es 0.|  
|is_replicated|**bit**|1 = La columna está replicada.|Siempre es 0.|  
|is_non_sql_subscribed|**bit**|1 = la columna tiene un suscriptor que no son de SQL.|Siempre es 0.|  
|is_merge_published|**bit**|1 = La columna está publicada para mezcla.|Siempre es 0.|  
|is_dts_replicated|**bit**|1 = columna se replica mediante el uso de SSIS.|Siempre es 0.|  
|is_xml_document|**bit**|1 = El contenido es un documento XML completo.|Siempre es 0.|  
|xml_collection_id|**int**|0 = No es una colección de esquemas XML.|Siempre es 0.|  
|default_object_id|**int**|Id. del objeto predeterminado; 0 = no tiene valor predeterminado.|Siempre es 0.|  
|rule_object_id|**int**|Id. de la regla independiente enlazada a la columna. <br />0 = No hay ninguna regla independiente.|Siempre es 0.|  
|is_sparse|**bit**|1 = La columna es una columna dispersa.|Siempre es 0.|  
|is_column_set|**bit**|1 = La columna es un conjunto de columnas.|Siempre es 0.|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|NOT NULL|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Sys.ALL_COLUMNS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
