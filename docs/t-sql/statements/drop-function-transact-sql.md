---
title: "DROP, función (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b85cb68749cdcf88d62d9d8fbf136a37e845519
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Quita una o más funciones definidas por el usuario de la base de datos actual. Funciones definidas por el usuario se crean mediante [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) y modificar mediante [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md).  
  
 La función de destino es compatible con funciones definidas por el usuario compiladas de forma nativa, escalares. Para obtener más información, consulte [Scalar User-Defined funciones para OLTP en memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```  
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTE*    
 Quita condicionalmente la función solo si ya existe. Disponible a partir [!INCLUDE[ssnoversion_md](../../includes/ssnoversion_md.md)] 2016 y en [!INCLUDE[sssds_md](../../includes/sssds_md.md)].
  
 *schema_name*  
 Nombre del esquema al que pertenece la función definida por el usuario.  
  
 *nombre_función*  
 Es el nombre de la función definida por el usuario que se va a quitar. Especificar el nombre del esquema es opcional. No se pueden especificar el nombre del servidor ni el nombre de la base de datos.  
  
## <a name="remarks"></a>Comentarios  
 DROP FUNCTION no funcionará correctamente si existen vistas o funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] en la base de datos que hacen referencia a esta función y que fueron creadas con SCHEMABINDING; tampoco funcionará si existen columnas calculadas o restricciones CHECK o DEFAULT que hacen referencia a la función.  
  
 DROP FUNCTION no funcionará correctamente si existen columnas calculadas que hacen referencia a esta función y que han sido indizadas.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar DROP FUNCTION, el usuario debe, como mínimo, contar con permiso de tipo ALTER sobre el esquema al que pertenece la función, o con un permiso de tipo CONTROL sobre la función.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-a-function"></a>A. Quitar una función  
 En el ejemplo siguiente se quita el `fn_SalesByStore` función definida por el usuario desde el `Sales` esquema en el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos de ejemplo. Para crear esta función, vea el ejemplo B en [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [Object_id &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [Sys.Parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  

