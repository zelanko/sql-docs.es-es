---
title: Sys.dm_sql_referenced_entities (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_sql_referenced_entities_TSQL
- dm_sql_referenced_entities
- sys.dm_sql_referenced_entities
- sys.dm_sql_referenced_entities_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_sql_referenced_entities dynamic management function
ms.assetid: 077111cb-b860-4d61-916f-bac5d532912f
caps.latest.revision: "46"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e2fd94b7bab89220337cede905ecbaf1decef722
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmsqlreferencedentities-transact-sql"></a>sys.dm_sql_referenced_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada entidad definida por el usuario a la que se hace referencia por nombre en la definición de la entidad de referencia especificada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se crea una dependencia entre dos entidades cuando una entidad definida por el usuario, llamada la *hacía referencia a entidad*, aparece por nombre en una expresión SQL persistente de otra entidad definida por el usuario, llamada la *entidad de referencia* . Por ejemplo, si un procedimiento almacenado es la entidad especificada de referencia, esta función devuelve todas las entidades definidas por el usuario a las que se hace referencia en el procedimiento almacenado, como tablas, vistas, tipos definidos por el usuario (UDT) u otros procedimientos almacenados.  
  
 Puede usar esta función de administración dinámica para notificar los siguientes tipos de entidades referenciadas por la entidad de referencia especificada:  
  
-   Entidades enlazadas a esquema  
  
-   Entidades no enlazadas a esquema  
  
-   Entidades entre servidores y entre bases de datos  
  
-   Dependencias de nivel de columna en entidades enlazadas y no enlazadas a esquema  
  
-   Tipos definidos por el usuario (alias y CLR UDT)  
  
-   colecciones de esquemas XML  
  
-   Funciones de partición  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_sql_referenced_entities (  
    ' [ schema_name. ] referencing_entity_name ' , ' <referencing_class> ' )  
  
<referencing_class> ::=  
{  
    OBJECT  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *schema_name*. ] *referencing_entity_name*  
 Es el nombre de la entidad que hace la referencia. *schema_name* es necesaria si la clase de referencia es OBJECT.  
  
 *schema_name.referencing_entity_name* es **nvarchar (517)**.  
  
 *< Referencing_class >* :: = {objeto | DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER}  
 Es la clase de la entidad de referencia especificada. Solo se puede especificar una clase por instrucción.  
  
 *< referencing_class >* es **nvarchar (60)**.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|referencing_minor_id|**int**|Identificador de la columna cuando la entidad de referencia es una columna; en caso contrario, es 0. No admite valores NULL.|  
|referenced_server_name|**sysname**|Nombre del servidor de la entidad a la que se hace referencia.<br /><br /> Esta columna se rellena para las dependencias entre servidores especificadas con un nombre de cuatro partes válido. Para obtener información sobre los nombres de varias partes, vea [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41; ](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).<br /><br /> NULL para las dependencias no enlazadas a esquema para las que se hizo referencia a la entidad sin especificar un nombre de cuatro partes.<br /><br /> NULL para las entidades enlazadas a esquema porque deben estar en la misma base de datos y, por tanto, solo pueden definirse con dos partes (*esquema.objeto*) nombre.|  
|referenced_database_name|**sysname**|Nombre de la base de datos de la entidad a la que se hace referencia.<br /><br /> Esta columna se rellena para las referencias entre bases de datos o entre servidores especificadas con un nombre válido de tres o cuatro partes.<br /><br /> NULL para las referencias no enlazadas a esquema especificadas con un nombre de una o dos partes.<br /><br /> NULL para las entidades enlazadas a esquema porque deben estar en la misma base de datos y, por tanto, solo pueden definirse con dos partes (*esquema.objeto*) nombre.|  
|referenced_schema_name|**sysname**|Esquema al que pertenece la entidad a la que se hace referencia.<br /><br /> NULL para las referencias no enlazadas a esquema en las que se hacía referencia a la entidad sin especificar el nombre del esquema.<br /><br /> Nunca es NULL para las referencias enlazadas a un esquema.|  
|referenced_entity_name|**sysname**|Nombre de la entidad a la que se hace referencia. No admite valores NULL.|  
|referenced_minor_name|**sysname**|Nombre de la columna cuando la entidad a la que se hace referencia es una columna; en caso contrario, es NULL. Por ejemplo, referenced_minor_name es NULL en la fila que contiene la propia entidad a la que se hace referencia.<br /><br /> Una entidad a la que se hace referencia es una columna cuando una columna se identifica mediante un nombre en la entidad de referencia o cuando la entidad primaria se usa en una instrucción SELECT *.|  
|referenced_id|**int**|Identificador de la entidad a la que se hace referencia. Cuando el valor de referenced_minor_id no es 0, referenced_id es la entidad en la que se define la columna.<br /><br /> Siempre es NULL para las referencias entre servidores.<br /><br /> NULL para las referencias entre bases de datos cuando no se puede determinar el identificador porque la base de datos está sin conexión o no se puede enlazar la entidad.<br /><br /> NULL para las referencias dentro de la base de datos si no se puede determinar el identificador. Para las referencias enlazadas a esquema, no se puede resolver el identificador cuando la entidad que se hace referencia no existe en la base de datos o cuando la resolución de nombres es dependiente del autor de llamada.  En este último caso, is_caller_dependent se establece en 1.<br /><br /> Nunca es NULL para las referencias enlazadas a un esquema.|  
|referenced_minor_id|**int**|Identificador de la columna cuando la entidad a la que se hace referencia es una columna; en caso contrario, es 0. Por ejemplo, referenced_minor_name es 0 en la fila que contiene la propia entidad a la que se hace referencia.<br /><br /> Para las referencias no enlazadas a esquema, se notifican las dependencias de las columnas únicamente cuando se pueden enlazar todas las entidades a las que se hace referencia. Si no se pueden enlazar todas las entidades a las que se hace referencia, no se notifican las dependencias del nivel de columna y referenced_minor_id es 0. Vea el ejemplo D.|  
|referenced_class|**tinyint**|Clase de la entidad a la que se hace referencia.<br /><br /> 1 = Objeto o columna<br /><br /> 6 = Tipo<br /><br /> 10 = Colección de esquemas XML<br /><br /> 21 = Función de partición|  
|referenced_class_desc|**nvarchar (60)**|Descripción de la clase de la entidad a la que se hace referencia.<br /><br /> OBJECT_OR_COLUMN<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> PARTITION_FUNCTION|  
|is_caller_dependent|**bit**|Indica que el enlace de esquema de la entidad a la que se hace referencia se realiza en tiempo de ejecución; por consiguiente, la resolución del identificador de la entidad depende del esquema del autor de la llamada. Esto ocurre cuando la entidad a la que se hace referencia es un procedimiento almacenado, un procedimiento almacenado extendido o una función definida por el usuario llamada en una instrucción EXECUTE.<br /><br /> 1 = La entidad a la que se hace referencia es dependiente del autor de la llamada y se resuelve en tiempo de ejecución. En este caso, referenced_id es NULL.<br /><br /> 0 = El identificador de la entidad a la que se hace referencia no es dependiente del autor de la llamada. Es siempre 0 para las referencias enlazadas a esquema y para las referencias entre bases de datos o entre servidores que especifican explícitamente un nombre de esquema. Por ejemplo, una referencia a una entidad con el formato `EXEC MyDatabase.MySchema.MyProc` no es dependiente del autor de la llamada. Sin embargo, una referencia con el formato `EXEC MyDatabase..MyProc` es dependiente del autor de la llamada.|  
|is_ambiguous|**bit**|Indica la referencia es ambigua y se puede resolver en tiempo de ejecución a una función definida por el usuario, un tipo definido por el usuario (UDT) o una referencia xquery a una columna de tipo **xml**. Por ejemplo, supongamos que la instrucción `SELECT Sales.GetOrder() FROM Sales.MySales` está definida en un procedimiento almacenado. Hasta que no se ejecute el procedimiento almacenado, no se sabrá si `Sales.GetOrder()` es una función definida por el usuario en el esquema `Sales` o en la columna con nombre `Sales` de tipo UDT con un método denominado `GetOrder()`.<br /><br /> 1 = La referencia a una función definida por el usuario o el método de tipo definido por el usuario (UDT) de columna es ambiguo.<br /><br /> 0 = La referencia no es ambigua o la entidad puede enlazarse correctamente cuando se llama a la función.<br /><br /> Siempre es 0 para las referencias enlazadas a esquema.|  
|is_selected|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Se ha seleccionado el objeto o la columna.|  
|is_updated|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Se ha modificado el objeto o la columna.|  
|is_select_all|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1= El objeto se usa en la cláusula SELECT * (solo en el nivel de objeto).|  
|is_all_columns_found|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = Se pueden encontrar todas las dependencias de columna del objeto.<br /><br /> 0 = No se pueden encontrar las dependencias de columna del objeto.|
|is_insert_all|**bit**|**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = el objeto se usa en una instrucción INSERT sin una lista de columnas (solo nivel de objeto).|  
|is_incomplete|**bit**|**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = el objeto o columna tiene un error de enlace y está incompleta.|
  
## <a name="exceptions"></a>Excepciones  
 Devuelve un conjunto de resultados vacío si se da alguna de las condiciones siguientes:  
  
-   Se especifica un objeto del sistema.  
  
-   La entidad especificada no existe en la base de datos actual.  
  
-   La entidad especificada no hace referencia a ninguna entidad.  
  
-   Se pasó un parámetro no válido.  
  
 Devuelve un error si la entidad especificada de referencia es un procedimiento almacenado numerado.  
  
 Devuelve el error 2020 cuando no se pueden resolver las dependencias de columna. Este error no impide que la consulta devuelva dependencias de nivel de objeto.  
  
## <a name="remarks"></a>Comentarios  
 Se puede ejecutar esta función en el contexto de cualquier base de datos para devolver las entidades que hacen referencia a un desencadenador DDL de servidor.  
  
 La tabla siguiente enumera los tipos de entidades para las que se crea y mantiene la información de dependencia. La información de dependencia no se crea ni mantiene para reglas, valores predeterminados, tablas temporales, procedimientos almacenados temporales u objetos del sistema.  
  
|Tipo de entidad|Entidad que hace la referencia|Entidad a la que se hace referencia|  
|-----------------|------------------------|-----------------------|  
|Tabla|Sí*|Sí|  
|Ver|Sí|Sí|  
|Procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)]**|Sí|Sí|  
|procedimiento almacenado CLR|No|Sí|  
|Función definida por el usuario de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|Sí|  
|Función CLR definida por el usuario|No|Sí|  
|Desencadenador CLR (DML y DDL)|No|No|  
|Desencadenador DML de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|No|  
|Desencadenador DDL de nivel de base de datos de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|No|  
|Desencadenador DDL de nivel de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sí|No|  
|Procedimientos almacenados extendidos|No|Sí|  
|Cola|No|Sí|  
|Synonym (Sinónimo)|No|Sí|  
|Tipo (tipo CLR y alias definido por el usuario)|No|Sí|  
|Colección de esquemas XML|No|Sí|  
|Función de partición|No|Sí|  
  
 \*Una tabla se realiza un seguimiento como una entidad de referencia sólo cuando se hace referencia una [!INCLUDE[tsql](../../includes/tsql-md.md)] module, tipo definido por el usuario o la colección de esquemas XML en la definición de una columna calculada, una restricción CHECK o una restricción DEFAULT.  
  
 ** No se realiza el seguimiento de los procedimientos almacenados numerados con un valor entero mayor que 1 como la entidad que hace referencia ni como la entidad a la que se hace referencia.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso SELECT en sys.dm_sql_referenced_entities y el permiso VIEW DEFINITION en la entidad de referencia. De forma predeterminada, se concede el permiso SELECT a public. Requiere el permiso VIEW DEFINITION en la base de datos o el permiso ALTER DATABASE DDL TRIGGER en la base de datos si la entidad de referencia es un desencadenador DDL de base de datos. Requiere el permiso VIEW ANY DEFINITION en el servidor si la entidad de referencia es un desencadenador DDL de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-entities-that-are-referenced-by-a-database-level-ddl-trigger"></a>A. Devolver las entidades a las que se hace referencia mediante un desencadenador DDL de nivel de base de datos  
 El ejemplo siguiente devuelve las entidades (tablas y columnas) a las que hace referencia el desencadenador DDL de base de datos `ddlDatabaseTriggerLog`.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc  
FROM sys.dm_sql_referenced_entities ('ddlDatabaseTriggerLog', 'DATABASE_DDL_TRIGGER');  
GO  
```  
  
### <a name="b-returning-entities-that-are-referenced-by-an-object"></a>B. Devolver las entidades a las que hace referencia un objeto  
 El ejemplo siguiente devuelve las entidades a las que hace referencia la función definida por el usuario `dbo.ufnGetContactInformation`.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT referenced_schema_name, referenced_entity_name, referenced_minor_name,   
    referenced_minor_id, referenced_class_desc, is_caller_dependent, is_ambiguous  
FROM sys.dm_sql_referenced_entities ('dbo.ufnGetContactInformation', 'OBJECT');  
GO  
```  
  
### <a name="c-returning-column-dependencies"></a>C. Devolver las dependencias de las columnas  
 El ejemplo siguiente crea la tabla `Table1` con la columna calculada `c`, definida como la suma de las columnas `a` y `b`. A continuación, se llama a la vista `sys.dm_sql_referenced_entities`. La vista devuelve dos filas, una para cada columna definida en la columna calculada.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.Table1 (a int, b int, c AS a + b);  
GO  
SELECT referenced_schema_name AS schema_name,  
    referenced_entity_name AS table_name,  
    referenced_minor_name AS referenced_column,  
    COALESCE(COL_NAME(OBJECT_ID(N'dbo.Table1'),referencing_minor_id), 'N/A') AS referencing_column_name  
FROM sys.dm_sql_referenced_entities ('dbo.Table1', 'OBJECT');  
GO

-- Remove the table.  
DROP TABLE dbo.Table1;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 schema_name table_name referenced_column referencing_column  
 ----------- ---------- ----------------- ------------------  
 dbo         Table1     a                 c  
 dbo         Table1     b                 c  
```

### <a name="d-returning-non-schema-bound-column-dependencies"></a>D. Devolver dependencias de las columnas no enlazadas a esquema  
 En el ejemplo siguiente se quita `Table1` y se crea `Table2` y el procedimiento almacenado `Proc1`. El procedimiento hace referencia a `Table2` y a la tabla no existente `Table1`. La vista `sys.dm_sql_referenced_entities` se ejecuta con el procedimiento almacenado especificado como la entidad de referencia. El conjunto de resultados muestra una fila para `Table1` y tres filas para `Table2`. Como `Table1` no existe, no se pueden resolver las dependencias de columna y se devuelve el error 2020. La columna `is_all_columns_found` devuelve 0 para `Table1`, lo que indica que había columnas que no se pudieron detectar.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'dbo.Table1', 'U' ) IS NOT NULL   
    DROP TABLE dbo.Table1;  
GO  
CREATE TABLE dbo.Table2 (c1 int, c2 int);  
GO  
CREATE PROCEDURE dbo.Proc1 AS  
    SELECT a, b, c FROM Table1;  
    SELECT c1, c2 FROM Table2;  
GO  
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name AS referenced_column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1  
 935674381     Table2       C1                      1  
 935674381     Table2       C2                      1  
 NULL          Table1       NULL                    0  

 Msg 2020, Level 16, State 1, Line 1The dependencies reported for entity "dbo.Proc1" might not include references to all columns. This is either because the entity references an object that does not exist or because of an error in one or more statements in the entity.  Before rerunning the query, ensure that there are no errors in the entity and that all objects referenced by the entity exist.
 ```
  
### <a name="e-demonstrating-dynamic-dependency-maintenance"></a>E. Ejemplo de mantenimiento dinámico de las dependencias  
 El ejemplo siguiente amplía el ejemplo D y muestra cómo se mantienen dinámicamente las dependencias. En primer lugar, el ejemplo vuelve a crear `Table1`, que se quitó en el ejemplo D. A continuación, se ejecuta de nuevo `sys.dm_sql_referenced_entities` con el procedimiento almacenado especificado como entidad de referencia. El conjunto de resultados muestra que se devuelven las tablas y sus columnas respectivas definidas en el procedimiento almacenado. Además, la columna `is_all_columns_found` devuelve un 1 para todos los objetos y columnas.  
  
```t-sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (a int, b int, c AS a + b);  
GO   
SELECT referenced_id, referenced_entity_name AS table_name, referenced_minor_name as column_name, is_all_columns_found  
FROM sys.dm_sql_referenced_entities ('dbo.Proc1', 'OBJECT');  
GO  
DROP TABLE Table1, Table2;  
DROP PROC Proc1;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referenced_id table_name   referenced_column_name  is_all_columns_found  
 ------------- ------------ ----------------------- --------------------  
 935674381     Table2       NULL                    1 
 935674381     Table2       c1                      1 
 935674381     Table2       c2                      1 
 967674495     Table1       NULL                    1 
 967674495     Table1       a                       1  
 967674495     Table1       b                       1  
 967674495     Table1       c                       1  
 ```
 
### <a name="f-returning-object-or-column-usage"></a>F. Devolución del uso de objetos o columnas  
 El ejemplo siguiente devuelve los objetos y las dependencias de columna del procedimiento almacenado `HumanResources.uspUpdateEmployeePersonalInfo`. Este procedimiento actualiza las columnas `NationalIDNumber`, `BirthDate,``MaritalStatus`, y `Gender` de la `Employee` tabla según un determinado `BusinessEntityID` valor. Otro procedimiento almacenado, `upsLogError`, se define en un bloque TRY…CATCH para capturar cualquier error de ejecución. Las columnas `is_selected`, `is_updated` y `is_select_all` devuelven información sobre cómo se utilizan estos objetos y columnas  dentro del objeto de referencia. La tabla y las columnas que se modifican se indican mediante un 1 en la columna is_updated. La columna `BusinessEntityID` solo se selecciona y el procedimiento almacenado `uspLogError` ni se selecciona ni se modifica.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```t-sql  
SELECT referenced_entity_name AS table_name, referenced_minor_name as column_name, is_selected, is_updated, is_select_all  
FROM sys.dm_sql_referenced_entities ('HumanResources.uspUpdateEmployeePersonalInfo', 'OBJECT');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 table_name    column_name         is_selected is_updated is_select_all  
 ------------- ------------------- ----------- ---------- -------------  
 uspLogError   NULL                0           0          0  
 Employee      NULL                0           1          0  
 Employee      BusinessEntityID    1           0          0  
 Employee      NationalIDNumber    0           1          0  
 Employee      BirthDate           0           1          0  
 Employee      MaritalStatus       0           1          0  
 Employee      Gender              0           1          0
 ```
  
## <a name="see-also"></a>Vea también  
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
