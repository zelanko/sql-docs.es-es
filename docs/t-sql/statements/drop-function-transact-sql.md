---
title: DROP FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e7754da5821f3531ac8db359ae95668681f94b0
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636060"
---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita una o más funciones definidas por el usuario de la base de datos actual. Las funciones definidas por el usuario se crean mediante [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) y se modifican con [ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md).  
  
 La función DROP admite funciones escalares definidas por el usuario y compiladas de forma nativa. Para obtener más información, vea [Funciones escalares definidas por el usuario para OLTP en memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```syntaxsql
 -- Azure SQL Data Warehouse, Parallel Data Warehouse 

DROP FUNCTION [IF EXISTS] [ schema_name. ] function_name
[;] 
```  
   
  
## <a name="arguments"></a>Argumentos
 *IF EXISTS*    
 Quita la función condicionalmente solo si ya existe. Disponible a partir de [!INCLUDE[ssnoversion_md](../../includes/ssnoversion-md.md)] 2016 y en [!INCLUDE[sssds_md](../../includes/sssds-md.md)].
  
 *schema_name*  
 Nombre del esquema al que pertenece la función definida por el usuario.  
  
 *function_name*  
 Es el nombre de la función definida por el usuario que se va a quitar. Especificar el nombre del esquema es opcional. No se pueden especificar el nombre del servidor ni el nombre de la base de datos.  
  
## <a name="remarks"></a>Observaciones  
 DROP FUNCTION no funcionará correctamente si existen vistas o funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] en la base de datos que hacen referencia a esta función y que fueron creadas con SCHEMABINDING; tampoco funcionará si existen columnas calculadas o restricciones CHECK o DEFAULT que hacen referencia a la función.  
  
 DROP FUNCTION no funcionará correctamente si existen columnas calculadas que hacen referencia a esta función y que han sido indizadas.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar DROP FUNCTION, el usuario debe, como mínimo, contar con permiso de tipo ALTER sobre el esquema al que pertenece la función, o con un permiso de tipo CONTROL sobre la función.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-dropping-a-function"></a>A. Quitar una función  
 En este ejemplo se quita la función definida por el usuario `fn_SalesByStore` del esquema `Sales` en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Para crear esta función, vea el ejemplo B en [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
```  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>Consulte también  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
