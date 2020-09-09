---
description: CONSTRAINT_TABLE_USAGE (Transact-SQL)
title: CONSTRAINT_TABLE_USAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_TABLE_USAGE_TSQL
- CONSTRAINT_TABLE_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- CONSTRAINT_TABLE_USAGE view
- INFORMATION_SCHEMA.CONSTRAINT_TABLE_USAGE view
ms.assetid: 5770b696-6c04-4d5c-a8db-9eb92022fa42
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3c9a45cc232200789925462486c54b5b877b5c59
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546432"
---
# <a name="constraint_table_usage-transact-sql"></a>CONSTRAINT_TABLE_USAGE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve una fila por cada tabla de la base de datos actual que tiene una restricción definida en ella. Esta vista de esquema de información devuelve información acerca de los objetos para los que el usuario actual tiene permisos.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Calificador de tabla.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nombre de esquema que contiene la tabla.<br /><br /> **&#42;&#42; importante &#42;&#42;** No use vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. INFORMATION_SCHEMA vistas solo representan un subconjunto de los metadatos de un objeto. La única manera confiable de encontrar el esquema de un objeto es consultar la vista de catálogo sys. Objects.|  
|**TABLE_NAME**|**sysname**|Nombre de la tabla.|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Calificador de la restricción.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la restricción.<br /><br /> **&#42;&#42; importante &#42;&#42;** No use vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. INFORMATION_SCHEMA vistas solo representan un subconjunto de los metadatos de un objeto. La única manera confiable de encontrar el esquema de un objeto es consultar la vista de catálogo sys. Objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nombre de la restricción.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [Sys. key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [Sys. foreign_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
