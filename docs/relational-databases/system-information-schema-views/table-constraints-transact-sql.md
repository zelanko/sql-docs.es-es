---
title: TABLE_CONSTRAINTS (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TABLE_CONSTRAINTS
- TABLE_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.TABLE_CONSTRAINTS view
- TABLE_CONSTRAINTS view
ms.assetid: 687f3284-2849-4853-8a5c-fc936deceae0
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 77991108c778b123ff13c90eb5bcc8535a9ef1e1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="tableconstraints-transact-sql"></a>TABLE_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada restricción de tabla de la base de datos actual. Esta vista de esquema de información devuelve información acerca de los objetos para los que el usuario actual tiene permisos.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA. *** view_name*.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Calificador de la restricción.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la restricción.<br /><br /> **\*\* Importante \* \***  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nombre de la restricción.|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Calificador de tabla.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nombre de esquema que contiene la tabla.<br /><br /> **\*\* Importante \* \***  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla.|  
|**CONSTRAINT_TYPE**|**varchar (** 11 **)**|Tipo de restricción:<br /><br /> CHECK<br /><br /> UNIQUE<br /><br /> PRIMARY KEY<br /><br /> FOREIGN KEY|  
|**IS_DEFERRABLE**|**varchar (** 2 **)**|Especifica si la comprobación de la restricción se puede aplazar. Siempre devuelve NO.|  
|**INITIALLY_DEFERRED**|**varchar (** 2 **)**|Especifica si la comprobación de la restricción se aplaza inicialmente. Siempre devuelve NO.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [Sys.check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
  
