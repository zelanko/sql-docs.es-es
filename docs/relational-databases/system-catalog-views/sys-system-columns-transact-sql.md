---
title: Sys.system_columns (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- system_columns_TSQL
- system_columns
- sys.system_columns
- sys.system_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_columns catalog view
ms.assetid: 4ab1d48a-d57a-4e76-a08c-9627eeaf4588
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 513fe4c2dd7bfc4c613a920be1ced218900515d7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33222046"
---
# <a name="syssystemcolumns-transact-sql"></a>sys.system_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila para cada columna de objetos de sistema que tienen columnas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece esta columna.|  
|**Nombre**|**sysname**|Nombre de la columna. Es único en el objeto.|  
|**column_id**|**int**|Identificador de la columna. Es único en el objeto.<br /><br /> Los Id. de columna no tienen que ser secuenciales.|  
|**system_type_id**|**tinyint**|Id. del tipo de sistema de la columna|  
|**user_type_id**|**int**|Id. del tipo de la columna, tal como lo ha definido el usuario.<br /><br /> Para devolver el nombre del tipo, unir a la [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) vista en esta columna de catálogo.|  
|**max_length**|**smallint**|Longitud máxima (en bytes) de la columna.<br /><br /> -1 = la columna es de tipo de datos **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, o **xml**.<br /><br /> Para **texto** columnas, el **max_length** valor será 16 o el valor establecido por **sp_tableoption** 'text in row'.|  
|**precisión**|**tinyint**|Precisión de la columna si basada en números; en caso contrario, es 0.|  
|**escala**|**tinyint**|Escala de la columna, si está basada en números; en caso contrario, es 0.|  
|**collation_name**|**sysname**|Nombre de la intercalación de la columna si basados en caracteres; en caso contrario, es NULL.|  
|**is_nullable**|**bit**|1 = La columna acepta valores NULL.|  
|**is_ansi_padded**|**bit**|1 = La columna utiliza el comportamiento ANSI_PADDING ON si es de tipo character, binary o variant.<br /><br /> 0 = La columna no es de tipo character, binary o variant.|  
|**is_rowguidcol**|**bit**|1 = La columna se ha declarado como ROWGUIDCOL.|  
|**is_identity**|**bit**|1 = columna tiene valores de identidad.|  
|**is_computed**|**bit**|1 = La columna es una columna calculada.|  
|**is_filestream**|**bit**|1 = La columna se ha declarado para utilizar el almacenamiento FILESTREAM.|  
|**is_replicated**|**bit**|1 = La columna está replicada.|  
|**is_non_sql_subscribed**|**bit**|1 = La columna tiene un suscriptor que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_merge_published**|**bit**|1 = La columna está publicada para mezcla.|  
|**is_dts_replicated**|**bit**|1 = La columna se replica con [!INCLUDE[ssIS](../../includes/ssis-md.md)].|  
|**is_xml_document**|**bit**|1 = El contenido es un documento XML completo.<br /><br /> 0 = el contenido es un fragmento de documento o el tipo de datos de columna no es **xml**.|  
|**xml_collection_id**|**int**|Distinto de cero si el tipo de datos de la columna es **xml** y se ha escrito el código XML. El valor será el identificador de la colección que contiene el espacio de nombres de esquema XML validación de la columna.<br /><br /> 0 = No es una colección de esquemas XML.|  
|**default_object_id**|**int**|Id. del objeto predeterminado, independientemente de que sea independiente [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md), o una restricción de valor predeterminado de nivel de columna insertada. El **parent_object_id** columna de un objeto predeterminado de nivel de columna insertada es una referencia a la propia tabla. O bien, es 0 si no hay valor predeterminado.|  
|**rule_object_id**|**int**|Id. de la regla independiente enlazada a la columna mediante **sys.sp_bindrule**.<br /><br /> 0 = No hay ninguna regla independiente.<br /><br /> Para las restricciones CHECK de nivel de columna, vea [sys.check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md).|  
|is_sparse|**bit**|1 = La columna es una columna dispersa. Para obtener más información, vea [Usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).|  
|is_column_set|**bit**|1 = La columna es un conjunto de columnas. Para obtener más información, vea [Usar conjuntos de columnas](../../relational-databases/tables/use-column-sets.md).|  
|generated_always_type|**tinyint**|El valor numérico que representa el tipo de columna:<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|La descripción del tipo de columna:<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END<br /><br /> **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Sys.ALL_COLUMNS &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [Sys.computed_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
