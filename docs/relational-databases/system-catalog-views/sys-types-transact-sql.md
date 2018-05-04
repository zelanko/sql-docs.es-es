---
title: Sys.Types (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- types
- types_TSQL
- sys.types_TSQL
- sys.types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.types catalog view
- table-valued parameters,sys.types
ms.assetid: a5dbc842-71a0-4f62-b5e0-f560a99b7f8c
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0e474a164ce837ccf2ea965ae3590921461d3bce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="systypes-transact-sql"></a>sys.types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada tipo del sistema y definido por el usuario.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del tipo. Es exclusivo en el esquema.|  
|**system_type_id**|**tinyint**|Id. del tipo del sistema interno del tipo.|  
|**user_type_id**|**int**|Id. del tipo. Es único en la base de datos. Tipos de datos del sistema, **user_type_id** = **system_type_id**.|  
|**schema_id**|**int**|Id. del esquema al que pertenece el tipo.|  
|**principal_id**|**int**|Id. del propietario individual si es distinto al propietario del esquema. De forma predeterminada, los objetos contenidos en el esquema pertenecen al propietario del esquema. No obstante, es posible especificar un propietario alternativo mediante la instrucción ALTER AUTHORIZATION para cambiar la propiedad.<br /><br /> Si no hay un propietario alternativo individual, el valor es NULL.|  
|**max_length**|**smallint**|Longitud máxima del tipo, en bytes.<br /><br /> -1 = la columna es de tipo de datos **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, o **xml**.<br /><br /> Para **texto** columnas, el **max_length** valor será 16.|  
|**precisión**|**tinyint**|Precisión máxima del tipo si está basado en numerales; de lo contrario, es 0.|  
|**escala**|**tinyint**|Escala máxima del tipo si está basado en numerales; de lo contrario, es 0.|  
|**collation_name**|**sysname**|Nombre de la intercalación del tipo si está basado en caracteres; de lo contrario, es NULL.|  
|**is_nullable**|**bit**|El tipo admite valores NULL.|  
|**is_user_defined**|**bit**|1 = Tipo definido por el usuario.<br /><br /> 0 = tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**is_assembly_type**|**bit**|1 = La implementación del tipo está definida en un ensamblado CLR.<br /><br /> 0 = El tipo está basado en un tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**default_object_id**|**int**|Id. del valor predeterminado independiente que está enlazado al tipo mediante el uso de [sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md).<br /><br /> 0 = No hay valor predeterminado.|  
|**rule_object_id**|**int**|Id. de la regla independiente que está enlazada al tipo mediante el uso de [sp_bindrule](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md).<br /><br /> 0 = No hay regla.|  
|**is_table_type**|**bit**|Indica que el tipo es una tabla.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de tipos escalares &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
