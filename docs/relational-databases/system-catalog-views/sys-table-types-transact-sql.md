---
title: Sys. table_types (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e000d4e4f7f46d57bb1ae9a4e5c370169eb1227f
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821331"
---
# <a name="systable_types-transact-sql"></a>sys.table_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Muestra las propiedades de los tipos de tabla definidos por el usuario en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un tipo de tabla es un tipo del que se pueden declarar variables de tabla o parámetros con valores de tabla. Cada tipo de tabla tiene una **type_table_object_id** que es una clave externa en la vista de catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) . Puede utilizar esta columna de identificador para consultar varias vistas de catálogo, de forma similar a una columna de **object_id** de una tabla normal, para detectar la estructura del tipo de tabla, como sus columnas y restricciones.    
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|*\<columnas heredadas>*||Para obtener una lista de las columnas que hereda esta vista, vea [Sys. types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md).|  
|**type_table_object_id**|**int**|Número de identificación del objeto. Este número es único en la base de datos.|  
|**is_memory_optimized**|**bit**|**Válido para** : [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y versiones posteriores.<br /><br /> Los posibles valores son los siguientes:<br /><br /> 0 = no está optimizado en memoria<br /><br /> 1 = está optimizado en memoria<br /><br /> Un valor de 0 es el valor predeterminado.<br /><br /> Los tipos de tabla siempre se crean con DURABILITY = SCHEMA_ONLY. Solo el esquema se conserva en el disco.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Usar parámetros con valores de tabla &#40;Motor de base de datos&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
