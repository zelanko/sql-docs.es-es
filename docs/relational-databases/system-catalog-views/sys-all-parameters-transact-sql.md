---
title: Sys.all_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- all_parameters_TSQL
- sys.all_parameters
- all_parameters
- sys.all_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_parameters catalog view
ms.assetid: eecbb68e-9b4c-4243-94e2-8096a9cc7892
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63231301109f83243b431244028fddffb8cc6fe7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001325"
---
# <a name="sysallparameters-transact-sql"></a>sys.all_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Muestra la unión de todos los parámetros que pertenecen a objetos definidos por el usuario u objetos del sistema.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece el parámetro.|  
|**name**|**sysname**|Nombre del parámetro. Es único en el objeto. Si el objeto es una función escalar, el nombre del parámetro es una cadena vacía en la fila que representa el valor devuelto.|  
|**parameter_id**|**int**|Id. del parámetro. Es único en el objeto. Si el objeto es una función escalar, **parameter_id** = 0 representa el valor devuelto.|  
|**system_type_id**|**tinyint**|Id. del tipo de sistema del parámetro.|  
|**user_type_id**|**int**|Id. de tipo del parámetro, definido por el usuario.<br /><br /> Para devolver el nombre del tipo, unir a la [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) en esta columna de la vista de catálogo.|  
|**max_length**|**smallint**|Longitud máxima del parámetro, en bytes.<br /><br /> -1 = la columna es de tipo de datos **varchar (max)** , **nvarchar (max)** , **varbinary (max)** , o **xml**.|  
|**precisión**|**tinyint**|Precisión del parámetro si es numérico; de otro modo, es 0.|  
|**scale**|**tinyint**|Escala del parámetro si es numérico; de otro modo, es 0.|  
|**is_output**|**bit**|1 = El parámetro es de salida (o de retorno); de otro modo, es 0.|  
|**is_cursor_ref**|**bit**|1 = Se trata de un parámetro de referencia de cursor.|  
|**has_default_value**|**bit**|1 = El parámetro tiene un valor predeterminado.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo mantiene valores predeterminados para objetos CLR en esta vista de catálogo; por lo tanto, esta columna siempre tiene valor 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para ver el valor predeterminado de un parámetro en un [!INCLUDE[tsql](../../includes/tsql-md.md)] de objetos, consulta el **definición** columna de la [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista de catálogo o utilizar el [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)función del sistema.|  
|**is_xml_document**|**bit**|1 = El contenido es un documento XML completo.<br /><br /> 0 = el contenido es un fragmento de documento o el tipo de datos de la columna no es **xml**.|  
|**default_value**|**sql_variant**|Si **has_default_value** es 1, el valor de esta columna es el valor predeterminado para el parámetro; en caso contrario, NULL.|  
|**xml_collection_id**|**int**|Es el Id. de la colección de esquemas XML utilizada para validar el parámetro.<br /><br /> Distinto de cero si el tipo de datos del parámetro es **xml** y se escribe el código XML.<br /><br /> 0 = No hay una colección de esquemas XML o el parámetro no es XML.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [Sys.system_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
