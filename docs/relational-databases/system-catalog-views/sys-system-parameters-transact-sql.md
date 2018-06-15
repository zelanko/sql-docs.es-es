---
title: Sys.system_parameters (Transact-SQL) | Documentos de Microsoft
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
- sys.system_parameters
- sys.system_parameters_TSQL
- system_parameters_TSQL
- system_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_parameters catalog view
ms.assetid: 0d135c5f-68b5-4009-a0da-35e6abfee0ff
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c849674f30a041ea58a771c3a75505a7d1fa2ebf
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221316"
---
# <a name="syssystemparameters-transact-sql"></a>sys.system_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada objeto del sistema que tiene parámetros.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece el parámetro.|  
|**Nombre**|**sysname**|Nombre del parámetro. Es único en el objeto.<br /><br /> Si el objeto es una función escalar, el nombre del parámetro es una cadena vacía en la fila que representa el valor devuelto.|  
|**parameter_id**|**int**|Id. del parámetro. Es único en el objeto. Si el objeto es una función escalar, **parameter_id** = 0 representa el valor devuelto.|  
|**system_type_id**|**tinyint**|Identificador del tipo de sistema del parámetro.|  
|**user_type_id**|**int**|Id. de tipo del parámetro, definido por el usuario.<br /><br /> Para devolver el nombre del tipo, unir a la [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) vista en esta columna de catálogo.|  
|**max_length**|**smallint**|Longitud máxima del parámetro, en bytes. Valor será -1 cuando la columna tipo de datos es **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, o **xml**.|  
|**precisión**|**tinyint**|Precisión del parámetro si está basado en numerales; de lo contrario es 0.|  
|**escala**|**tinyint**|Escala del parámetro si está basado en numerales; de lo contrario es 0.|  
|**is_output**|**bit**|1 = El parámetro es de salida (o de retorno); de otro modo, es 0.|  
|**is_cursor_ref**|**bit**|1 = El parámetro es un parámetro de referencia a un cursor.|  
|**has_default_value**|**bit**|1 = el parámetro tiene el valor predeterminado.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo mantiene valores predeterminados para objetos CLR en esta vista de catálogo; por lo tanto, esta columna siempre tiene valor 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para ver el valor predeterminado de un parámetro en un [!INCLUDE[tsql](../../includes/tsql-md.md)] de objetos, consulte la **definición** columna de la [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista de catálogo, o usar el [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)función del sistema.|  
|**is_xml_document**|**bit**|1 = El contenido es un documento XML completo.<br /><br /> 0 = el contenido es un fragmento de documento o el tipo de datos de la columna no es **xml**.|  
|**default_value**|**sql_variant**|Si **has_default_value** es 1, el valor de esta columna es el valor predeterminado para el parámetro; en caso contrario, es NULL.|  
|**xml_collection_id**|**int**|Distinto de cero si el tipo de datos del parámetro es **xml** y se ha escrito el código XML. El valor es el Id. de la colección que contiene el espacio de nombres del esquema XML de validación para el parámetro.<br /><br /> 0 = No existe una colección de esquema XML.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [Sys.all_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)  
  
  
