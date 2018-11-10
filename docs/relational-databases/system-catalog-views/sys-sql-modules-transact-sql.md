---
title: Sys.sql_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_modules_TSQL
- sql_modules
- sql_modules_TSQL
- sys.sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_modules catalog view
ms.assetid: 23d3ccd2-f356-4d89-a2cd-bee381243f99
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 59f65e8743dab760b54cec9b088f5feca8d49e0b
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221541"
---
# <a name="syssqlmodules-transact-sql"></a>sys.sql_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para cada objeto que es un módulo definido con lenguaje SQL en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluido de forma nativa compila función escalar definida por el usuario. Los objetos del tipo P, RF, V, TR, FN, IF, TF y R tienen un módulo SQL asociado. Los valores predeterminados independientes, objetos del tipo D, también incluyen una definición de módulo SQL en esta vista. Para obtener una descripción de estos tipos, vea la **tipo** columna en el [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista de catálogo.  
  
 Para obtener más información, vea [Funciones escalares definidas por el usuario para OLTP en memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. de objeto del objeto contenedor. Es único en una base de datos.|  
|**Definición**|**nvarchar(max)**|Texto SQL que define este módulo. Este valor también se puede obtener mediante la [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) función integrada.<br /><br /> NULL = Cifrado.|  
|**uses_ansi_nulls**|**bit**|Módulo creado con SET ANSI_NULLS ON.<br /><br /> Siempre será = 0 para reglas y valores predeterminados.|  
|**uses_quoted_identifier**|**bit**|Módulo creado con SET QUOTED_IDENTIFIER ON.|  
|**is_schema_bound**|**bit**|El módulo se ha creado con la opción SCHEMABINDING.<br /><br /> Siempre contiene el valor 1 para los procedimientos almacenados generados de forma nativa.|  
|**uses_database_collation**|**bit**|1 = La definición del módulo enlazado a un esquema depende de la intercalación predeterminada de la base de datos para la evaluación correcta; en caso contrario, 0. Esta dependencia impide cambiar la intercalación predeterminada de la base de datos.|  
|**is_recompiled**|**bit**|El procedimiento se ha creado con la opción WITH RECOMPILE.|  
|**null_on_null_input**|**bit**|Módulo declarado para generar una salida NULL en cualquier entrada NULL.|  
|**execute_as_principal_id**|**Int**|Id. de la entidad de seguridad de base de datos EXECUTE AS.<br /><br /> NULL de manera predeterminada o si EXECUTE AS CALLER.<br /><br /> Id. de la entidad de seguridad especificado si EXECUTE AS SELF o EXECUTE AS \<principal >.<br /><br /> -2 = EXECUTE AS OWNER.|  
|**uses_native_compilation**|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].<br /><br /> 0 = no está compilado de forma nativa<br /><br /> 1 = está compilado de forma nativa<br /><br /> El valor predeterminado es 0.|  
|**is_inlineable**|**bit**|**Se aplica a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] y versiones posteriores.<br/><br />Indica si el módulo es inlineable o no. Capacidad de alineación se basa en las condiciones especificadas [aquí](../user-defined-functions/scalar-udf-inlining.md#inlineable-scalar-udfs-requirements).<br /><br /> 0 = no inlineable<br /><br /> 1 = es inlineable. <br /><br /> Para UDF escalares, el valor será 1 si la UDF es inlineable y 0 en caso contrario. Siempre contiene un valor de 1 para funciones TVF en línea y 0 para todos los demás tipos de módulo.<br />|  
|**inline_type**|**bit**|**Se aplica a**: [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] y versiones posteriores.<br /><br />Indica si la inserción está activado para el módulo actualmente. <br /><br />0 = inserción está desactivado<br /><br /> 1 = inserción está activado.<br /><br /> Para UDF escalares, el valor será 1 si la inserción está activado (explícita o implícitamente). El valor siempre será 1 para las funciones TVF insertadas y 0 para otros tipos de módulo.<br />|  

  
## <a name="remarks"></a>Comentarios  
 La expresión SQL para una restricción DEFAULT, objeto de tipo D, se encuentra en la [sys.default_constraints](../../relational-databases/system-catalog-views/sys-default-constraints-transact-sql.md) vista de catálogo. La expresión SQL para una restricción CHECK, objeto de tipo C, se encuentra en la [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) vista de catálogo.  
  
 Esta información también se describe en [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el nombre, el tipo y la definición de cada módulo de la base de datos actual.  
  
```  
SELECT sm.object_id, OBJECT_NAME(sm.object_id) AS object_name, o.type, o.type_desc, sm.definition  
FROM sys.sql_modules AS sm  
JOIN sys.objects AS o ON sm.object_id = o.object_id  
ORDER BY o.type;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Consultar el catálogo del sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
