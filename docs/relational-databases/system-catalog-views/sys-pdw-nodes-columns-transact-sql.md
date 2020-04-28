---
title: Sys. pdw_nodes_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 201af9001703bb8f1dfbdaf2c41151697b945df3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68059402"
---
# <a name="syspdw_nodes_columns-transact-sql"></a>Sys. pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Muestra las columnas para las tablas definidas por el usuario y las vistas definidas por el usuario.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|Identificador del objeto al que pertenece esta columna.||  
|name|**sysname**|Nombre de la columna. Único en el objeto.||  
|column_id|**int**|Identificador de la columna. Único en el objeto.||  
|system_type_id|**tinyint**|Id. del tipo de sistema de la columna.||  
|user_type_id|**int**|Id. del tipo de la columna, tal como lo ha definido el usuario.||  
|max_length|**smallint**|Longitud máxima de la columna, en bytes.|Incluye-1 (no válido) para los tipos de columna no admitidos.|  
|precision|**tinyint**|Precisión de la columna, si está basada en números; de lo contrario, es 0.||  
|scale|**tinyint**|La escala de la columna se basa en valores numéricos; en caso contrario, es 0.||  
|collation_name|**sysname**|Nombre de la intercalación de la columna, si está basada en caracteres; de lo contrario, es NULL.||  
|is_nullable|**bit**|1 = La columna acepta valores NULL.||  
|is_ansi_padded|**bit**|1 = La columna utiliza el comportamiento ANSI_PADDING ON si es de tipo character, binary o variant.|Siempre es 0.|  
|is_rowguidcol|**bit**|1 = La columna se ha declarado como ROWGUIDCOL.|Siempre es 0.|  
|is_identity|**bit**|1 = la columna tiene valores de identidad.|Siempre es 0.|  
|is_computed|**bit**|1 = La columna es una columna calculada.|Siempre es 0.|  
|is_filestream|**bit**|1 = La columna es una columna FILESTREAM.|Siempre es 0.|  
|is_replicated|**bit**|1 = La columna está replicada.|Siempre es 0.|  
|is_non_sql_subscribed|**bit**|1 = la columna tiene un suscriptor que no es de SQL.|Siempre es 0.|  
|is_merge_published|**bit**|1 = La columna está publicada para mezcla.|Siempre es 0.|  
|is_dts_replicated|**bit**|1 = la columna se replica mediante SSIS.|Siempre es 0.|  
|is_xml_document|**bit**|1 = El contenido es un documento XML completo.|Siempre es 0.|  
|xml_collection_id|**int**|0 = No es una colección de esquemas XML.|Siempre es 0.|  
|default_object_id|**int**|IDENTIFICADOR del objeto predeterminado; 0 = no hay ningún valor predeterminado.|Siempre es 0.|  
|rule_object_id|**int**|IDENTIFICADOR de la regla independiente enlazada a la columna. <br />0 = No hay ninguna regla independiente.|Siempre es 0.|  
|is_sparse|**bit**|1 = La columna es una columna dispersa.|Siempre es 0.|  
|is_column_set|**bit**|1 = La columna es un conjunto de columnas.|Siempre es 0.|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|NOT NULL|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [Sys. all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
