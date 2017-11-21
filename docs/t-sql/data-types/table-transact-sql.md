---
title: tabla (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table data type [SQL Server]
- table variables [SQL Server]
ms.assetid: 1ef0b60e-a64c-4e97-847b-67930e3973ef
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b22ecfa04f949af77df974abc3359b7bc5144a82
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="table-transact-sql"></a>table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Es un tipo de datos especial que se puede utilizar para almacenar un conjunto de resultados para procesar en otro momento. **tabla** se utiliza principalmente para el almacenamiento temporal de un conjunto de filas devuelto como el conjunto de resultados de una función con valores de tabla. Las funciones y variables se pueden declarar como de tipo **tabla**. **tabla** las variables pueden usarse en las funciones, procedimientos almacenados y lotes. Para declarar las variables de tipo **tabla**, use [DECLARE @local_variable ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  

**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
table_type_definition ::=   
    TABLE ( { <column_definition> | <table_constraint> } [ ,...n ] )   
  
<column_definition> ::=   
    column_name scalar_data_type   
    [ COLLATE <collation_definition> ]   
    [ [ DEFAULT constant_expression ] | IDENTITY [ ( seed , increment ) ] ]   
    [ ROWGUIDCOL ]   
    [ column_constraint ] [ ...n ]   
  
 <column_constraint> ::=   
    { [ NULL | NOT NULL ]   
    | [ PRIMARY KEY | UNIQUE ]   
    | CHECK ( logical_expression )   
    }   
  
<table_constraint> ::=   
     { { PRIMARY KEY | UNIQUE } ( column_name [ ,...n ] )  
     | CHECK ( logical_expression )   
     }   
```  
  
## <a name="arguments"></a>Argumentos  
*table_type_definition*  
Es el mismo subconjunto de información que se utiliza para definir una tabla en CREATE TABLE. La declaración de tabla incluye definiciones de columna, nombres, tipos de datos y restricciones. Solo se permiten los tipos de restricciones PRIMARY KEY, UNIQUE KEY y NULL.  
Para obtener más información acerca de la sintaxis, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md), [Crear función &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md), y [DECLARE @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md).
  
*collation_name*  
Es la intercalación de la columna que se compone de un [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuración regional de Windows y un estilo de comparación, una configuración regional de Windows y la notación binaria o una [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intercalación. Si *collation_name* no se especifica, la columna hereda la intercalación de la base de datos actual. Si la columna se ha definido como un tipo definido por el usuario CLR (Common Language Runtime), la columna hereda la intercalación del tipo definido por el usuario.
  
## <a name="remarks"></a>Comentarios  
**tabla** variables pueden hacer referencia a por su nombre en la cláusula FROM de un lote, tal y como se muestra en el ejemplo siguiente:
  
```sql
SELECT Employee_ID, Department_ID FROM @MyTableVar;  
```  
  
Fuera de una cláusula FROM, **tabla** variables deben hacer referencia mediante un alias, tal como se muestra en el ejemplo siguiente:
  
```sql
SELECT EmployeeID, DepartmentID   
FROM @MyTableVar m  
JOIN Employee on (m.EmployeeID =Employee.EmployeeID AND  
   m.DepartmentID = Employee.DepartmentID);  
```  
  
**tabla** las variables proporcionan las siguientes ventajas para las consultas a pequeña escala que tienen planes de consulta que no cambian y cuando dominantes recompilación es:
-   A **tabla** variable se comporta como una variable local. Tiene un ámbito bien definido. Dicho ámbito es la función, el procedimiento almacenado o el lote en que se declara.   
     Dentro de su ámbito, una **tabla** variable puede utilizarse como una tabla normal. Puede aplicarse en cualquier lugar de las instrucciones SELECT, INSERT, UPDATE y DELETE donde se utilice una tabla o expresión de tabla. Sin embargo, **tabla** no se puede usar en la siguiente instrucción:  
  
```sql
SELECT select_list INTO table_variable;
```
  
**tabla** variables se limpian automáticamente al final de la función, procedimiento almacenado o lote en que se definen.
  
-   **tabla** las variables utilizadas en los procedimientos almacenados causan menos recompilaciones de los procedimientos almacenados que cuando se utilizan tablas temporales cuando no hay ningún opciones basadas en costo que afectan al rendimiento.  
-   Las transacciones que implican **tabla** variables del último solo durante el transcurso de una actualización en el **tabla** variable. Por lo tanto, **tabla** variables requieren menos recursos de registro y bloqueo.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones
**Tabla** variables no tienen estadísticas de distribución, no desencadenarán recompilaciones. Por tanto, en muchos casos, el optimizador generará un programa de consultas basándose en que la variable table no tiene filas. Por este motivo, las variables table deben usarse con precaución si se espera una gran cantidad de filas (más de 100). En estos casos, las tablas Temp pueden representar una mejor solución. O bien, para las consultas que se unen a la variable de tabla con otras tablas, utilice la sugerencia RECOMPILE, lo que hará que el optimizador utilice la cardinalidad correcta para la variable de tabla.
  
**tabla** variables no se admiten en los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modelo de razonamiento basado en costos del optimizador. Por lo tanto, no se deben usar cuando se requieren opciones basadas en costos para lograr un plan de consultas eficaz. Se prefieren las tablas temporales cuando se requieren opciones basadas en costos. Esto incluye normalmente consultas con uniones, decisiones de paralelismo y opciones de selección de índice.
  
Las consultas que modifican **tabla** variables no generan planes de ejecución de consultas en paralelo. Rendimiento puede verse afectado cuando gran **tabla** variables, o **tabla** se modifican las variables en consultas complejas. En estas situaciones, puede optar por utilizar tablas temporales. Para obtener más información, vea [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md). Las consultas que leen **tabla** variables sin modificarlas pueden generarse en paralelo.
  
Índices no se pueden crear explícitamente en **tabla** variables y no hay ninguna estadística se mantiene en **tabla** variables. En determinados casos, el rendimiento puede mejorar si se utilizan tablas temporales, las cuales admiten índices y estadísticas. Para obtener más información acerca de las tablas temporales, vea [CREATE TABLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-table-transact-sql.md).
  
Compruebe las restricciones, valores predeterminados y las columnas calculadas de la **tabla** declaración de tipo no puede llamar a funciones definidas por el usuario.
  
Operación de asignación entre **tabla** variables no se admite.
  
Dado que **tabla** variables tienen un ámbito limitado y no forman parte de la base de datos persistente, no se ven afectados por reversiones de transacciones.
  
Las variables de tabla no se pueden modificar una vez creadas.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-declaring-a-variable-of-type-table"></a>A. Declarar una variable de tipo table  
El ejemplo siguiente crea una variable `table` que almacena los valores especificados en la cláusula OUTPUT de la instrucción UPDATE. Las dos instrucciones `SELECT` que le siguen devuelven los valores en `@MyTableVar` y los resultados de la operación de actualización en la tabla `Employee`. Tenga en cuenta que los resultados en la `INSERTED.ModifiedDate` columna difieren de los valores en el `ModifiedDate` columna en el `Employee` tabla. Esto se debe a que el desencadenador `AFTER UPDATE`, que actualiza el valor de `ModifiedDate` a la fecha actual, se define en la tabla `Employee`. Sin embargo, las columnas que devuelve `OUTPUT` reflejan los datos anteriores a la activación de los desencadenadores. Para obtener más información, vea [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).
  
```sql
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25   
OUTPUT INSERTED.BusinessEntityID,  
       DELETED.VacationHours,  
       INSERTED.VacationHours,  
       INSERTED.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
--Note that ModifiedDate reflects the value generated by an  
--AFTER UPDATE trigger.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Crear una función alineada con valores de tabla  
En el siguiente ejemplo se devuelve una función alineada con valores de tabla. Devuelve tres columnas `ProductID`, `Name` y la suma de los totales del año hasta la fecha por tienda como `YTD Total` para cada producto vendido en el almacén.
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Sales.ufn_SalesByStore', N'IF') IS NOT NULL  
    DROP FUNCTION Sales.ufn_SalesByStore;  
GO  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```  
  
Para invocar la función, ejecute esta consulta.
  
```sql
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
## <a name="see-also"></a>Vea también
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
[Funciones definidas por el usuario](../../relational-databases/user-defined-functions/user-defined-functions.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[Usar con valores de tabla parámetros &#40; motor de base de datos &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
[Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)
  
  

