---
title: Usar parámetros con valores de tabla (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- DECLARE
- CREATE TYPE
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce96eb2e0cad45e15e03f48bbb27afb5cb61938b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37223215"
---
# <a name="use-table-valued-parameters-database-engine"></a>Usar parámetros con valores de tabla (motor de base de datos)
  Los parámetros con valores de tabla se declaran utilizando tipos de tabla definidos por el usuario. Puede utilizar parámetros con valores de tabla para enviar varias filas de datos a una rutina o una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] , como un procedimiento almacenado o una función, sin crear una tabla temporal o muchos parámetros.  
  
 Los parámetros con valores de tabla son como las matrices de parámetros en OLE DB y ODBC, pero proporcionan más flexibilidad y una integración más estrecha con [!INCLUDE[tsql](../../includes/tsql-md.md)]. Los parámetros con valores de tabla también tienen la ventaja de poder participar en operaciones basadas en conjuntos.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] pasa parámetros con valores de tabla a rutinas por referencia para evitar la realización de una copia de los datos de entrada. Puede crear y ejecutar rutinas [!INCLUDE[tsql](../../includes/tsql-md.md)] con parámetros con valores de tabla y llamarlas desde código de [!INCLUDE[tsql](../../includes/tsql-md.md)] , clientes nativos y administrados en cualquier lenguaje administrado.  
  
 **En este tema:**  
  
 [Ventajas](#Benefits)  
  
 [Restricciones](#Restrictions)  
  
 [Parámetros con valores de tabla frente a operaciones BULK INSERT](#BulkInsert)  
  
 [Ejemplo](#Example)  
  
##  <a name="Benefits"></a> Ventajas  
 Un parámetro con valores de tabla está incluido en el ámbito de procedimiento almacenado, función o texto [!INCLUDE[tsql](../../includes/tsql-md.md)] dinámico, exactamente igual que los demás parámetros. Del mismo modo, una variable de tipo de tabla tiene el mismo ámbito que cualquier otra variable local creada mediante una instrucción DECLARE. Puede declarar variables con valores de tabla en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] dinámicas y pasar estas variables como parámetros con valores de tabla a procedimientos almacenados y funciones.  
  
 Los parámetros con valores de tabla proporcionan más flexibilidad y, en algunos casos, un rendimiento mayor que las tablas temporales u otros medios para pasar una lista de parámetros. Los parámetros con valores de tabla proporcionan las ventajas siguientes:  
  
-   No adquieren bloqueos para el rellenado inicial de datos de un cliente.  
  
-   Proporcionan un modelo de programación simple.  
  
-   Permiten la inclusión de lógica comercial compleja en una rutina única.  
  
-   Reducen los viajes de ida y vuelta al servidor.  
  
-   Pueden tener una estructura de tabla de cardinalidad diferente.  
  
-   Tienen establecimiento inflexible de tipos.  
  
-   Permiten al cliente especificar un criterio de ordenación y claves únicas.  
  
-   Se almacenan en caché como una tabla temporal cuando se usa en un procedimiento almacenado. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los parámetros con valores de tabla también se almacenan en caché para las consultas con parámetros.  
  
##  <a name="Restrictions"></a> Restricciones  
 Los parámetros con valores de tabla tienen las restricciones siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mantiene estadísticas en las columnas de parámetros con valores de tabla.  
  
-   Los parámetros con valores de tabla se deben pasar como parámetros READONLY de entrada a rutinas [!INCLUDE[tsql](../../includes/tsql-md.md)] . No se pueden realizar operaciones de DML como UPDATE, DELETE o INSERT en un parámetro con valores de tabla en el cuerpo de una rutina.  
  
-   No se puede utilizar un parámetro con valores de tabla como destino de una instrucción SELECT INTO o INSERT EXEC. Un parámetro con valores de tabla puede estar en la cláusula FROM de SELECT INTO o en el procedimiento almacenado o la cadena INSERT EXEC.  
  
##  <a name="BulkInsert"></a> Parámetros con valores de tabla frente a operaciones BULK INSERT  
 El uso de parámetros con valores de tabla es comparable a otras formas de uso de variables basadas en conjuntos; sin embargo, el uso de parámetros con valores de tabla puede ser con frecuencia más rápido para grandes conjuntos de datos. Si se comparan con operaciones masivas que tienen un costo de inicio mayor que los parámetros con valores de tabla, el comportamiento de los parámetros con valores de tabla es excelente cuando se insertan menos de 1.000 filas.  
  
 Los parámetros con valores de tabla que se vuelven a utilizar se benefician del almacenamiento en caché de tablas temporales. Este almacenamiento en memoria caché de tablas proporciona una escalabilidad mejor que en el caso de operaciones BULK INSERT equivalentes. Si se usan pequeñas operaciones de inserción de filas, se puede conseguir una ligera mejora del rendimiento utilizando listas de parámetros o instrucciones por lotes en lugar de operaciones BULK INSERT o parámetros con valores de tabla. Sin embargo, estos métodos son menos apropiados para programar, y el rendimiento disminuye rápidamente cuando aumentan las filas.  
  
 Los parámetros con valores de tabla se comportan tan bien o mejor que una implementación de matriz de parámetros equivalente.  
  
##  <a name="Example"></a> Ejemplo  
 En el ejemplo siguiente se utiliza [!INCLUDE[tsql](../../includes/tsql-md.md)] y se muestra la forma de crear un tipo de parámetro con valores de tabla, declarar una variable para hacer referencia a ella, rellenar la lista de parámetros y, a continuación, pasar los valores a un procedimiento almacenado.  
  
```  
USE AdventureWorks2012;  
GO  
  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE dbo. usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO AdventureWorks2012.Production.Location  
           (Name  
           ,CostRate  
           ,Availability  
           ,ModifiedDate)  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
        GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT Name, 0.00  
    FROM AdventureWorks2012.Person.StateProvince;  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)   
 [sys.parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)   
 [sys.parameter_type_usages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
  
