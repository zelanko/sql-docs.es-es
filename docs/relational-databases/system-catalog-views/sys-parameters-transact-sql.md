---
title: Sys.Parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.parameters_TSQL
- sys.parameters
- parameters
- parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.parameters catalog view
- table-valued parameters,sys.parameters
ms.assetid: 24e2764b-c8e5-4322-97a4-7407d8b8a92b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 33c87d4b784e46defac98823a5cf9d4dc9420aaa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752313"
---
# <a name="sysparameters-transact-sql"></a>sys.parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada parámetro de un objeto que acepta parámetros. Si el objeto es una función escalar, también hay una fila que describe el valor devuelto. Esa fila tendrá un **parameter_id** el valor 0.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Identificador del objeto al que pertenece el parámetro.|  
|**Nombre**|**sysname**|Nombre del parámetro. Es único en el objeto.<br /><br /> Si el objeto es una función escalar, el nombre del parámetro es una cadena vacía en la fila que representa el valor devuelto.|  
|**parameter_id**|**int**|Id. del parámetro. Es único en el objeto.<br /><br /> Si el objeto es una función escalar, **parameter_id** = 0 representa el valor devuelto.|  
|**system_type_id**|**tinyint**|Id. del tipo de sistema del parámetro.|  
|**user_type_id**|**int**|Id. de tipo del parámetro, definido por el usuario.<br /><br /> Para devolver el nombre del tipo, unir a la [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) en esta columna de la vista de catálogo.|  
|**max_length**|**smallint**|Longitud máxima del parámetro, en bytes.<br /><br /> Valor = -1 cuando el tipo de datos de columna es **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, o **xml**.|  
|**Precisión**|**tinyint**|Precisión del parámetro si está basado en numerales; de lo contrario es 0.|  
|**Escala**|**tinyint**|Escala del parámetro si está basado en numerales; de lo contrario es 0.|  
|**is_output**|**bit**|1 = El parámetro es OUTPUT o RETURN; de lo contrario, es 0.|  
|**is_cursor_ref**|**bit**|1 = El parámetro es un parámetro de referencia a un cursor.|  
|**has_default_value**|**bit**|1 = el parámetro tiene el valor predeterminado.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo mantiene valores predeterminados para objetos de CLR en esta vista de catálogo; por lo tanto, esta columna tiene valor 0 para objetos [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para ver el valor predeterminado de un parámetro en un [!INCLUDE[tsql](../../includes/tsql-md.md)] de objetos, consulta el **definición** columna de la [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) vista de catálogo o utilizar el [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md)función del sistema.|  
|**is_xml_document**|**bit**|1 = El contenido es un documento XML completo.<br /><br /> 0 = el contenido es un fragmento de documento o el tipo de datos de la columna no es **xml**.|  
|**default_value**|**sql_variant**|Si **has_default_value** es 1, el valor de esta columna es el valor predeterminado para el parámetro; en caso contrario, NULL.|  
|**xml_collection_id**|**int**|Distinto de cero si el tipo de datos del parámetro es **xml** y se escribe el código XML. El valor es el identificador de la colección que contiene el espacio de nombres del esquema XML de validación del parámetro.<br /><br /> 0 = No es una colección de esquemas XML.|  
|**is_readonly**|**bit**|1 =  El parámetro es READONLY; de lo contrario, es 0.|  
|**is_nullable**|**bit**|1 = El parámetro admite valores NULL. (el valor predeterminado).<br /><br /> 0 = El parámetro no admite valores NULL, para que la ejecución de procedimientos almacenados compilados de forma nativa sea más eficaz.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Sys.all_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-parameters-transact-sql.md)   
 [Sys.system_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md)  
  
  
