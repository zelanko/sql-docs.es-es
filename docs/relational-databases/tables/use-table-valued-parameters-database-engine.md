---
description: Usar parámetros con valores de tabla (motor de base de datos)
title: Usar parámetros con valores de tabla (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ea6b58a75488aa4d46e9b1c2a71226c2e63f42a1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482295"
---
# <a name="use-table-valued-parameters-database-engine"></a>Usar parámetros con valores de tabla (motor de base de datos)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Los parámetros con valores de tabla se declaran utilizando tipos de tabla definidos por el usuario. Puede utilizar parámetros con valores de tabla para enviar varias filas de datos a una rutina o una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] , como un procedimiento almacenado o una función, sin crear una tabla temporal o muchos parámetros.

Los parámetros con valores de tabla son como las matrices de parámetros en OLE DB y ODBC, pero proporcionan más flexibilidad y una integración más estrecha con [!INCLUDE[tsql](../../includes/tsql-md.md)]. Los parámetros con valores de tabla también tienen la ventaja de poder participar en operaciones basadas en conjuntos.

[!INCLUDE[tsql](../../includes/tsql-md.md)] pasa parámetros con valores de tabla a rutinas por referencia para evitar la realización de una copia de los datos de entrada. Puede crear y ejecutar rutinas [!INCLUDE[tsql](../../includes/tsql-md.md)] con parámetros con valores de tabla y llamarlas desde código de [!INCLUDE[tsql](../../includes/tsql-md.md)] , clientes nativos y administrados en cualquier lenguaje administrado.

 **En este tema:**

[Ventajas](#Benefits)

[Restricciones](#Restrictions)

[Parámetros con valores de tabla frente a operaciones BULK INSERT](#BulkInsert)

[Ejemplo](#Example)

## <a name="benefits"></a><a name="Benefits"></a> Ventajas

Un parámetro con valores de tabla está incluido en el ámbito de procedimiento almacenado, función o texto [!INCLUDE[tsql](../../includes/tsql-md.md)] dinámico, exactamente igual que los demás parámetros. Del mismo modo, una variable de tipo de tabla tiene el mismo ámbito que cualquier otra variable local creada mediante una instrucción DECLARE. Puede declarar variables con valores de tabla en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] dinámicas y pasar estas variables como parámetros con valores de tabla a procedimientos almacenados y funciones.

Los parámetros con valores de tabla proporcionan más flexibilidad y, en algunos casos, un rendimiento mayor que las tablas temporales u otros medios para pasar una lista de parámetros. Los parámetros con valores de tabla proporcionan las ventajas siguientes:

- No adquieren bloqueos para el rellenado inicial de datos de un cliente.
- Proporcionan un modelo de programación simple.
- Permiten la inclusión de lógica comercial compleja en una rutina única.
- Reducen los viajes de ida y vuelta al servidor.
- Pueden tener una estructura de tabla de cardinalidad diferente.
- Tienen establecimiento inflexible de tipos.
- Permiten al cliente especificar un criterio de ordenación y claves únicas.
- Se almacenan en caché como una tabla temporal cuando se usa en un procedimiento almacenado. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los parámetros con valores de tabla también se almacenan en caché para las consultas con parámetros.

## <a name="permissions"></a><a name="Permissions"></a> Permisos
Para crear una instancia de un tipo de tabla definido por el usuario o llamar a un procedimiento almacenado con un parámetro con valores de tabla, el usuario debe tener el permiso EXECUTE en el tipo o en el esquema o la base de datos que contiene el tipo.

## <a name="restrictions"></a><a name="Restrictions"></a> Restricciones

Los parámetros con valores de tabla tienen las restricciones siguientes:

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no mantiene estadísticas en las columnas de parámetros con valores de tabla.
- Los parámetros con valores de tabla se deben pasar como parámetros READONLY de entrada a rutinas [!INCLUDE[tsql](../../includes/tsql-md.md)] . No se pueden realizar operaciones de DML como UPDATE, DELETE o INSERT en un parámetro con valores de tabla en el cuerpo de una rutina.
- No se puede utilizar un parámetro con valores de tabla como destino de una instrucción SELECT INTO o INSERT EXEC. Un parámetro con valores de tabla puede estar en la cláusula FROM de SELECT INTO o en el procedimiento almacenado o la cadena INSERT EXEC.

## <a name="table-valued-parameters-vs-bulk-insert-operations"></a><a name="BulkInsert"></a> Parámetros con valores de tabla frente a operaciones BULK INSERT

El uso de parámetros con valores de tabla es comparable a otras formas de uso de variables basadas en conjuntos; sin embargo, el uso de parámetros con valores de tabla puede ser con frecuencia más rápido para grandes conjuntos de datos. Si se comparan con operaciones masivas que tienen un costo de inicio mayor que los parámetros con valores de tabla, el comportamiento de los parámetros con valores de tabla es excelente cuando se insertan menos de 1.000 filas.

Los parámetros con valores de tabla que se vuelven a utilizar se benefician del almacenamiento en caché de tablas temporales. Este almacenamiento en memoria caché de tablas proporciona una escalabilidad mejor que en el caso de operaciones BULK INSERT equivalentes. Si se usan pequeñas operaciones de inserción de filas, se puede conseguir una ligera mejora del rendimiento utilizando listas de parámetros o instrucciones por lotes en lugar de operaciones BULK INSERT o parámetros con valores de tabla. Sin embargo, estos métodos son menos apropiados para programar, y el rendimiento disminuye rápidamente cuando aumentan las filas.

Los parámetros con valores de tabla se comportan tan bien o mejor que una implementación de matriz de parámetros equivalente.

## <a name="example"></a><a name="Example"></a> Ejemplo

En el ejemplo siguiente se utiliza [!INCLUDE[tsql](../../includes/tsql-md.md)] y se muestra la forma de crear un tipo de parámetro con valores de tabla, declarar una variable para hacer referencia a ella, rellenar la lista de parámetros y, a continuación, pasar los valores a un procedimiento almacenado en la base de datos de AdventureWorks.

```sql
/* Create a table type. */
CREATE TYPE LocationTableType 
   AS TABLE
      ( LocationName VARCHAR(50)
      , CostRate INT );
GO
/* Create a procedure to receive data for the table-valued parameter. */
CREATE PROCEDURE dbo. usp_InsertProductionLocation
   @TVP LocationTableType READONLY
      AS
      SET NOCOUNT ON
      INSERT INTO AdventureWorks2012.Production.Location
         (
            Name
            , CostRate
            , Availability
            , ModifiedDate
         )
      SELECT *, 0, GETDATE()
      FROM @TVP;
GO
/* Declare a variable that references the type. */
DECLARE @LocationTVP AS LocationTableType;
/* Add data to the table variable. */
INSERT INTO @LocationTVP (LocationName, CostRate)
   SELECT Name, 0.00
   FROM AdventureWorks2012.Person.StateProvince;
  
/* Pass the table variable data to a stored procedure. */
EXEC usp_InsertProductionLocation @LocationTVP;
```

## <a name="see-also"></a>Consulte también

- [CREATE TYPE](../../t-sql/statements/create-type-transact-sql.md)
- [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
- [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
- [sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)
- [sys.parameter_type_usages](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)
- [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)
- [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md)  
