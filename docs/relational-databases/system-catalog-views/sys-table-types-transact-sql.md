---
title: Sys.table_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- table_types_TSQL
- sys.table_types
- sys.table_types_TSQL
- table_types
dev_langs:
- TSQL
helpviewer_keywords:
- table types [SQL Server]
- table-valued parameters, sys.table_types
- sys.table_types
- UDTT
ms.assetid: c05fd873-aff2-4a89-9936-a54c2ea09996
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: eef7f540231ff230bf32e4f2e0d4613c5dab8477
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39559255"
---
# <a name="systabletypes-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra las propiedades de los tipos de tabla definidos por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un tipo de tabla es un tipo del que se pueden declarar variables de tabla o parámetros con valores de tabla. Cada tipo de tabla tiene un **type_table_object_id** que es una clave externa en el [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) vista de catálogo. Puede utilizar esta columna de identificador para consultar diversas vistas de catálogo, de manera que es similar a un **object_id** columna de una tabla normal, para detectar la estructura del tipo de tabla como sus columnas y restricciones.    
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|*\<hereda columnas >*||Para obtener una lista de columnas que hereda esta vista, consulte [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md).|  
|**type_table_object_id**|**int**|Número de identificación del objeto. Este número es único en la base de datos.|  
|**is_memory_optimized**|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Los posibles valores son los siguientes:<br /><br /> 0 = no está optimizado en memoria<br /><br /> 1 = está optimizado en memoria<br /><br /> Un valor de 0 es el valor predeterminado.<br /><br /> Los tipos de tabla siempre se crean con DURABILITY = SCHEMA_ONLY. Solo el esquema se conserva en el disco.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Object Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  (Vistas de catálogo de objetos [Transact-SQL])  
 [Usar parámetros con valores de tabla &#40;motor de base de datos&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
