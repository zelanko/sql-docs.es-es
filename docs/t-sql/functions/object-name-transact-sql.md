---
title: Object_name (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECT_NAME
- OBJECT_NAME_TSQL
dev_langs: TSQL
helpviewer_keywords:
- OBJECT_NAME function
- viewing database object names
- objects [SQL Server], names
- database objects [SQL Server], names
- displaying database object names
- database objects [SQL Server]
- names [SQL Server], database objects
ms.assetid: 7d5b923f-0c3e-4af9-b39b-132807a6d5b3
caps.latest.revision: "45"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0e6f583fb5fa20c8686343ee4d87e9f4b369183c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="objectname-transact-sql"></a>OBJECT_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el nombre del objeto de la base de datos para los objetos de ámbito de esquema. Para obtener una lista de objetos con ámbito de esquema, consulte [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
OBJECT_NAME ( object_id [, database_id ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_id*  
 Es el identificador del objeto que se va a utilizar. *object_id* es **int** y se supone que es un objeto de ámbito de esquema en la base de datos especificada, o en el contexto de base de datos actual.  
  
 *database_id*  
 Identificador de la base de datos donde se va a buscar el objeto. *database_id* es **int**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **sysname**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto. Si la base de datos de destino tiene la opción AUTO_CLOSE establecida en ON, la función abrirá la base de datos.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como OBJECT_NAME, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ANY en el objeto. Para especificar un identificador de base de datos, también se requiere el permiso CONNECT en la base de datos o se debe habilitar la cuenta de invitado.  
  
## <a name="remarks"></a>Comentarios  
 Funciones de sistema se pueden usar en la lista de selección en la cláusula WHERE, y en cualquier lugar en que se permita una expresión. Para obtener más información, consulte [expresiones](../../t-sql/language-elements/expressions-transact-sql.md) y [donde](../../t-sql/queries/where-transact-sql.md).  
  
 El valor que devuelve esta función del sistema usa la intercalación de la base de datos actual.  
  
 De forma predeterminada, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] se da por supuesto que *object_id* está en el contexto de la base de datos actual. Una consulta que hace referencia a un *object_id* en otra base de datos devuelve NULL o resultados incorrectos. Por ejemplo, en la siguiente consulta, el contexto de la base de datos actual es [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] intenta devolver un nombre de objeto para el identificador de objeto especificado en esa base de datos en lugar de en la base de datos especificada en la cláusula FROM de la consulta. Por lo tanto, se devuelve información incorrecta.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_NAME(object_id)  
FROM master.sys.objects;  
GO  
```  
  
 Puede resolver los nombres de objeto en el contexto de otra base de datos especificando un identificador de base de datos. En el ejemplo siguiente, se especifica el identificador de la base de datos `master` en la función `OBJECT_SCHEMA_NAME` y devuelve los resultados correctos.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT DISTINCT OBJECT_SCHEMA_NAME(object_id, 1) AS schema_name  
FROM master.sys.objects;  
GO  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-objectname-in-a-where-clause"></a>A. Usar OBJECT_NAME en una cláusula WHERE  
 El siguiente ejemplo devuelve columnas de la vista de catálogo `sys.objects` para el objeto especificado por `OBJECT_NAME` en la cláusula `WHERE` de la instrucción `SELECT`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyID int;  
SET @MyID = (SELECT OBJECT_ID('AdventureWorks2012.Production.Product',  
    'U'));  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(@MyID);  
GO  
```  
  
### <a name="b-returning-the-object-schema-name-and-object-name"></a>B. Devolver el nombre del esquema de objetos y el nombre del objeto  
 En el ejemplo siguiente se devuelve el nombre del esquema de objetos, el nombre del objeto y el texto SQL para todos los planes de consulta en caché que no sean instrucciones preparadas o ad hoc.  
  
```  
SELECT DB_NAME(st.dbid) AS database_name,   
    OBJECT_SCHEMA_NAME(st.objectid, st.dbid) AS schema_name,  
    OBJECT_NAME(st.objectid, st.dbid) AS object_name,   
    st.text AS query_text  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
WHERE st.objectid IS NOT NULL;  
GO  
```  
  
### <a name="c-returning-three-part-object-names"></a>C. Devolver nombres de objetos de tres partes  
 En el ejemplo siguiente se devuelve el nombre del objeto, esquema o base de datos junto con todas las demás columnas de la vista de administración dinámica `sys.dm_db_index_operational_stats` de todos los objetos de todas las bases de datos.  
  
```  
SELECT QUOTENAME(DB_NAME(database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_SCHEMA_NAME(object_id, database_id))   
    + N'.'   
    + QUOTENAME(OBJECT_NAME(object_id, database_id))  
    , *   
FROM sys.dm_db_index_operational_stats(null, null, null, null);  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-using-objectname-in-a-where-clause"></a>D. Usar OBJECT_NAME en una cláusula WHERE  
 El siguiente ejemplo devuelve columnas de la vista de catálogo `sys.objects` para el objeto especificado por `OBJECT_NAME` en la cláusula `WHERE` de la instrucción `SELECT`. (El número de objeto (274100017 en el ejemplo siguiente) será diferente.  Para probar este ejemplo, buscar un número de objeto válido mediante la ejecución de `SELECT name, object_id FROM sys.objects;` en la base de datos.)  
  
```  
SELECT name, object_id, type_desc  
FROM sys.objects  
WHERE name = OBJECT_NAME(274100017);  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de metadatos &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
  
  

