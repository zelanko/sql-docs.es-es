---
title: Constructor (Transact-SQL) con valores de tabla | Documentos de Microsoft
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- inserting multiple rows
- row value expression
- row constructor [SQL Server]
- table value constructor [SQL Server]
ms.assetid: e57cd31d-140e-422f-8178-2761c27b9deb
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 87fc6196f740c0bf3cfd9fa1f94f73872942fa1a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="table-value-constructor-transact-sql"></a>Constructor con valores de tabla (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica un conjunto de expresiones de valores de fila que se va a construir en una tabla. El constructor de valor de tabla de [!INCLUDE[tsql](../../includes/tsql-md.md)] permite que se especifiquen varias filas de datos en una sola instrucción DML. El constructor con valores de tabla puede especificarse en la cláusula VALUES de la instrucción INSERT, en la opción uso \<tabla de origen > cláusula de la instrucción MERGE y en la definición de una tabla derivada en la cláusula FROM.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
VALUES ( <row value expression list> ) [ ,...n ]   
  
<row value expression list> ::=  
    {<row value expression> } [ ,...n ]  
  
<row value expression> ::=  
    { DEFAULT | NULL | expression }  
```  
  
## <a name="arguments"></a>Argumentos  
 VALUES  
 Introduce las listas de expresión de los valores de las filas. Cada lista debe aparecer entre paréntesis y separarse mediante una coma.  
  
 El número de valores especificados en cada lista debe ser el mismo y los valores deben estar en el mismo orden que las columnas de la tabla. Se debe especificar un valor para cada columna de la tabla o la lista de columnas debe especificar explícitamente las columnas para cada valor entrante.  
  
 DEFAULT  
 Hace que [!INCLUDE[ssDE](../../includes/ssde-md.md)] inserte el valor predeterminado definido para una columna. Si no existe ningún valor predeterminado para la columna y esta admite valores NULL, se inserta NULL. DEFAULT no es un valor válido para una columna de identidad. Cuando se especifica en un constructor con valores de tabla, DEFAULT solo se permite en una instrucción INSERT.  
  
 *expression*  
 Es una constante, variable o expresión. La expresión no puede contener una instrucción EXECUTE.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Constructores con valores de tabla pueden usarse en una de estas dos formas: directamente en la lista de valores de una instrucción INSERT... Se admiten como una tabla derivada desde cualquier lugar y tablas derivadas o valores de instrucción. Se devuelve el error 10738 si el número de filas supera el máximo. Para insertar más filas de las que permite el límite, use uno de los métodos siguientes:  
  
-   Crear varias instrucciones INSERT  
  
-   Usar una tabla derivada  
  
-   Importación masiva de datos mediante el uso de la **bcp** utilidad o la instrucción BULK INSERT  
  
 Como expresión de valores de fila solo se permiten valores escalares. Como expresión de valores de fila no se permiten las subconsultas que impliquen a varias columnas. Por ejemplo, el código siguiente produce un error de sintaxis porque la tercera lista de expresiones de valores de fila contiene una subconsulta con varias columnas.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE dbo.MyProducts (Name varchar(50), ListPrice money);  
GO  
-- This statement fails because the third values list contains multiple columns in the subquery.  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       (SELECT Name, ListPrice FROM Production.Product WHERE ProductID = 720);  
GO  
  
```  
  
 Sin embargo, la instrucción se puede reescribir especificando cada columna en la subconsulta independientemente. El ejemplo siguiente inserta correctamente tres filas en la tabla `MyProducts`.  
  
```  
INSERT INTO dbo.MyProducts (Name, ListPrice)  
VALUES ('Helmet', 25.50),  
       ('Wheel', 30.00),  
       ((SELECT Name FROM Production.Product WHERE ProductID = 720),  
        (SELECT ListPrice FROM Production.Product WHERE ProductID = 720));  
GO  
  
```  
  
## <a name="data-types"></a>Tipos de datos  
 Los valores especificados en una instrucción INSERT de varias filas siguen las propiedades de conversión de tipos de datos de la sintaxis de UNION ALL. Esto da como resultado la conversión implícita de tipos no coincidentes para el tipo de mayor [prioridad](../../t-sql/data-types/data-type-precedence-transact-sql.md). Si la conversión no es una conversión implícita admitida, se devuelve un error. Por ejemplo, la instrucción siguiente inserta un valor entero y un valor de carácter en una columna de tipo **char**.  
  
```  
CREATE TABLE dbo.t (a int, b char);  
GO  
INSERT INTO dbo.t VALUES (1,'a'), (2, 1);  
GO  
```  
  
 Cuando se ejecuta la instrucción INSERT, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta convertir 'a' en un entero porque la precedencia del tipo de datos indica que un entero pertenece a un tipo más alto que un carácter. Se produce un error en la conversión y se devuelve un error. Para evitar este error, puede convertir explícitamente los valores según corresponda. Por ejemplo, la instrucción anterior puede escribirse del siguiente modo.  
  
```  
INSERT INTO dbo.t VALUES (1,'a'), (2, CONVERT(CHAR,1));  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-inserting-multiple-rows-of-data"></a>A. Insertar varias filas de datos  
 En el siguiente ejemplo se crea la tabla `dbo.Departments` y, a continuación, se utiliza el constructor de valor de tabla para insertar cinco filas en la tabla. Dado que los valores para todas las columnas se suministran e incluyen en el mismo orden que las columnas de la tabla, no es necesario especificar los nombres de columna en la lista de columnas.  
  
```  
USE AdventureWorks2012;  
GO  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923'), (N'Y3', N'Cubic Yards', '20080923');  
GO  
  
```  
  
### <a name="b-inserting-multiple-rows-with-default-and-null-values"></a>B. Insertar varias filas con los valores DEFAULT y NULL  
 En el siguiente ejemplo se demuestra cómo especificar DEFAULT y NULL cuando se utiliza el constructor de valor de tabla para insertar filas en una tabla.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.MySalesReason(  
SalesReasonID int IDENTITY(1,1) NOT NULL,  
Name dbo.Name NULL ,  
ReasonType dbo.Name NOT NULL DEFAULT 'Not Applicable' );  
GO  
INSERT INTO Sales.MySalesReason   
VALUES ('Recommendation','Other'), ('Advertisement', DEFAULT), (NULL, 'Promotion');  
  
SELECT * FROM Sales.MySalesReason;  
  
```  
  
### <a name="c-specifying-multiple-values-as-a-derived-table-in-a-from-clause"></a>C. Especificar varios valores como una tabla derivada en una cláusula FROM  
 Los ejemplos siguientes usan el constructor con valores de tabla para especificar varios valores en la cláusula FROM de una instrucción SELECT.  
  
```  
SELECT a, b FROM (VALUES (1, 2), (3, 4), (5, 6), (7, 8), (9, 10) ) AS MyTable(a, b);  
GO  
-- Used in an inner join to specify values to return.  
SELECT ProductID, a.Name, Color  
FROM Production.Product AS a  
INNER JOIN (VALUES ('Blade'), ('Crown Race'), ('AWC Logo Cap')) AS b(Name)   
ON a.Name = b.Name;  
  
```  
  
### <a name="d-specifying-multiple-values-as-a-derived-source-table-in-a-merge-statement"></a>D. Especificar varios valores como una tabla de origen derivada en una instrucción MERGE  
 En el ejemplo siguiente se usa MERGE para modificar la tabla `SalesReason`, actualizando o insertando las filas. Cuando el valor de `NewName` de la tabla de origen coincide con un valor de la columna `Name` de la tabla de destino, (`SalesReason`), la columna `ReasonType` se actualiza en la tabla de destino. Cuando el valor de `NewName` no coincide, la fila del origen se inserta en la tabla de destino. La tabla de origen es una tabla derivada que usa la característica de constructor con valores de tabla de [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar varias filas en la tabla de origen.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  
