---
title: Números de secuencia | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sequence number object, overview
- sequence [Database Engine]
- autonumbers, sequences
- sequence numbers [SQL Server]
- sequence number object
ms.assetid: c900e30d-2fd3-4d5f-98ee-7832f37e79d1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d0446aaf5508ad0d2655245f441d4da81a6c79c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106865"
---
# <a name="sequence-numbers"></a>Números de secuencia
  Una secuencia es un objeto enlazado a un esquema definido por el usuario que genera una secuencia de valores numéricos según la especificación con la que se creó la secuencia. La secuencia de valores numéricos se genera en orden ascendente o descendente en un intervalo definido y puede repetirse cuando se solicite. Las secuencias, a diferencia de las columnas de identidad, no se asocian a tablas. Una aplicación hace referencia a un objeto de secuencia para recibir su valor siguiente. La aplicación controla la relación entre las secuencias y tablas. Las aplicaciones de usuario pueden hacer referencia a un objeto de secuencia y coordinar las claves de valores entre varias filas y tablas.  
  
 Una secuencia se crea independientemente de las tablas utilizando la instrucción **CREATE SEQUENCE** . Las opciones permiten controlar el incremento, los valores máximo y mínimo, el punto de inicio, la capacidad de reinicio automático y el almacenamiento en caché para aumentar el rendimiento. Para obtener información acerca de las opciones, vea [CREATE SEQUENCE](/sql/t-sql/statements/create-sequence-transact-sql).  
  
 A diferencia de los valores de columnas de identidad que se generan cuando se insertan filas, una aplicación puede obtener el número de secuencia siguiente sin insertar la fila llamando a la función [NEXT VALUE FOR](/sql/t-sql/functions/next-value-for-transact-sql) . Se asigna el número de secuencia cuando se llama a NEXT VALUE FOR aun cuando el número nunca se inserta en una tabla. La función NEXT VALUE FOR se puede utilizar como valor predeterminado para una columna en una definición de tabla. Use [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) para obtener un rango de varios números de secuencia de una sola vez.  
  
 Una secuencia se puede definir como cualquier tipo de datos enteros. Si no se especifica el tipo de datos, una secuencia tiene como valor predeterminado `bigint`.  
  
## <a name="using-sequences"></a>Utilizar secuencias  
 Utilice secuencias en lugar de columnas de identidad en los siguientes escenarios:  
  
-   La aplicación requiere un número antes de realizar la inserción en la tabla.  
  
-   La aplicación requiere compartir una serie única de números entre varias tablas o varias columnas de una tabla.  
  
-   La aplicación debe reiniciar la serie de números cuando se alcanza un número especificado. Por ejemplo, después de asignar valores entre 1 y 10, la aplicación comienza de nuevo a asignar valores entre 1 y 10.  
  
-   La aplicación requiere que los valores de secuencia se ordenen por otro campo. La función NEXT VALUE FOR puede aplicar la cláusula OVER a la llamada a la función. La cláusula OVER garantiza que los valores devueltos se generen en el orden de la cláusula OVER BY de la cláusula ORDER.  
  
-   Una aplicación requiere que se asignen varios números al mismo tiempo. Por ejemplo, una aplicación necesita reservar cinco números secuenciales. Al solicitar los valores de identidad, podrían producirse lagunas en la serie si se emitieron números simultáneamente para otros procesos. Al llamar a sp_sequence_get_range se pueden recuperar de una sola vez varios números de la secuencia.  
  
-   Necesita cambiar la especificación de la secuencia, como, por ejemplo, el valor de incremento.  
  
## <a name="limitations"></a>Limitaciones  
 A diferencia de las columnas de identidad, cuyos valores no se pueden cambiar, los valores de secuencia no se protegen automáticamente después de la inserción en la tabla. Para evitar que se cambien los valores de secuencia, utilice un desencadenador de actualización en la tabla para revertir los cambios.  
  
 La singularidad no se aplica automáticamente para los valores de la secuencia. La capacidad de reutilizar los valores de secuencia es por diseño. Si es necesario que los valores de secuencia de una tabla sean únicos, cree un índice único en la columna. Si se requiere que los valores de secuencia de una tabla sean únicos en todo un grupo de tablas, cree desencadenadores para evitar los duplicados debidos a las instrucciones de actualización o al ciclo del número de secuencia  
  
 El objeto de secuencia genera los números según su definición, pero el objeto de secuencia no controla cómo se utilizan los números. Los números de secuencia insertados en una tabla pueden tener lagunas cuando se revierte una transacción, cuando varias tablas comparten un objeto de secuencia o cuando los números de secuencia se asignan sin utilizarlos en tablas. Cuando se crea con la opción CACHE, un cierre inesperado, como un error de alimentación, puede perder los números de secuencia de la memoria caché.  
  
 Si hay varias instancias de la función `NEXT VALUE FOR` que especifica el mismo generador de secuencias dentro de una única instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)], todas esas instancias devuelven el mismo valor para una fila determinada procesada por esa instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Este comportamiento es coherente con el estándar ANSI.  
  
## <a name="typical-use"></a>Uso típico  
 Para crear un número de secuencia entero que se incremente en 1 de -2.147.483.648 a 2.147.483.647, utilice la siguiente instrucción.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    INCREMENT BY 1 ;  
```  
  
 Para crear un número de secuencia entero similar a una columna de identidad que se incrementa en 1 de 1 a 2.147.483.647, utilice la siguiente instrucción.  
  
```  
CREATE SEQUENCE Schema.SequenceName  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
  
```  
  
## <a name="managing-sequences"></a>Administrar secuencias  
 Para obtener información sobre las secuencias, consulte [sys.sequences](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql).  
  
## <a name="examples"></a>Ejemplos  
 Encontrará más ejemplos en los temas [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql), [NEXT VALUE FOR &#40;Transact-SQL&#41;](/sql/t-sql/functions/next-value-for-transact-sql) y [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql).  
  
### <a name="a-using-a-sequence-number-in-a-single-table"></a>A. Usar un número de secuencia en una sola tabla  
 En el siguiente ejemplo se crea un esquema denominado Test, una tabla denominada Orders y una secuencia denominada CountBy1 y, después, se insertan filas en la tabla mediante la función NEXT VALUE FOR.  
  
```  
--Create the Test schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Orders  
    (OrderID int PRIMARY KEY,  
    Name varchar(20) NOT NULL,  
    Qty int NOT NULL);  
GO  
  
-- Create a sequence  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
-- Insert three records  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Tire', 2) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Seat', 1) ;  
INSERT test.Orders (OrderID, Name, Qty)  
    VALUES (NEXT VALUE FOR Test.CountBy1, 'Brake', 1) ;  
GO  
  
-- View the table  
SELECT * FROM Test.Orders ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../../includes/ssresult-md.md)]  
  
 `OrderID  Name    Qty`  
  
 `1        Tire    2`  
  
 `2        Seat    1`  
  
 `3        Brake   1`  
  
### <a name="b-calling-next-value-for-before-inserting-a-row"></a>B. Llamar a NEXT VALUE FOR antes de insertar una fila  
 Utilizando la tabla `Orders` creada en el ejemplo A, el siguiente ejemplo declara una variable denominada `@nextID`y, a continuación, utiliza la función NEXT VALUE FOR para establecer la variable como el siguiente número de secuencia disponible. Se supone que la aplicación realiza cierto procesamiento del pedido, como, por ejemplo, proporcionar al cliente el número de `OrderID` de su pedido potencial y, a continuación, valida el pedido. Con independencia de cuánto tiempo pueda llevar este procesamiento y de cuántos pedidos se agreguen durante el proceso, el número original se conserva para que lo utilice esta conexión. Finalmente, la instrucción `INSERT` agrega el pedido a la tabla `Orders` .  
  
```  
DECLARE @NextID int ;  
SET @NextID = NEXT VALUE FOR Test.CountBy1;  
-- Some work happens  
INSERT Test.Orders (OrderID, Name, Qty)  
    VALUES (@NextID, 'Rim', 2) ;  
GO  
  
```  
  
### <a name="c-using-a-sequence-number-in-multiple-tables"></a>C. Usar un número de secuencia en varias tablas  
 En este ejemplo se supone que un proceso de supervisión de la línea de producción recibe una notificación de los eventos que se producen en el taller. Cada evento recibe un número `EventID` único que se incrementa de forma continua. Todos los eventos utilizan el mismo número de secuencia `EventID` para que los informes que combinan todos los eventos puedan identificar cada evento de forma única. Sin embargo, los datos de evento se almacenan en tres tablas diferentes, dependiendo del tipo de evento. El ejemplo de código crea un esquema denominado `Audit`, una secuencia denominada `EventCounter`y tres tablas, cada una de las cuales utiliza la secuencia `EventCounter` como valor predeterminado. A continuación el ejemplo agrega las filas a las tres tablas y consulta los resultados.  
  
```  
CREATE SCHEMA Audit ;  
GO  
CREATE SEQUENCE Audit.EventCounter  
    AS int  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
CREATE TABLE Audit.ProcessEvents  
(  
    EventID int PRIMARY KEY CLUSTERED   
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EventCode nvarchar(5) NOT NULL,  
    Description nvarchar(300) NULL  
) ;  
GO  
  
CREATE TABLE Audit.ErrorEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NULL,  
    ErrorNumber int NOT NULL,  
    EventDesc nvarchar(256) NULL  
) ;  
GO  
  
CREATE TABLE Audit.StartStopEvents  
(  
    EventID int PRIMARY KEY CLUSTERED  
        DEFAULT (NEXT VALUE FOR Audit.EventCounter),  
    EventTime datetime NOT NULL DEFAULT (getdate()),  
    EquipmentID int NOT NULL,  
    StartOrStop bit NOT NULL  
) ;  
GO  
  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 0) ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (72, 0) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (2735,   
    'Clean room temperature 18 degrees C.') ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (18, 'Spin rate threashold exceeded.') ;  
INSERT Audit.ErrorEvents (EquipmentID, ErrorNumber, EventDesc)   
    VALUES (248, 82, 'Feeder jam') ;  
INSERT Audit.StartStopEvents (EquipmentID, StartOrStop)   
    VALUES (248, 1) ;  
INSERT Audit.ProcessEvents (EventCode, Description)   
    VALUES (1841, 'Central feed in bypass mode.') ;  
-- The following statement combines all events, though not all fields.  
SELECT EventID, EventTime, Description FROM Audit.ProcessEvents   
UNION SELECT EventID, EventTime, EventDesc FROM Audit.ErrorEvents   
UNION SELECT EventID, EventTime,   
CASE StartOrStop   
    WHEN 0 THEN 'Start'   
    ELSE 'Stop'  
END   
FROM Audit.StartStopEvents  
ORDER BY EventID ;  
GO  
  
```  
  
 [!INCLUDE[ssResult](../../../includes/ssresult-md.md)]  
  
 `EventID  EventTime                Description`  
  
 `1        2009-11-02 15:00:51.157  Start`  
  
 `2        2009-11-02 15:00:51.160  Start`  
  
 `3        2009-11-02 15:00:51.167  Clean room temperature 18 degrees C.`  
  
 `4        2009-11-02 15:00:51.167  Spin rate threshold exceeded.`  
  
 `5        2009-11-02 15:00:51.173  Feeder jam`  
  
 `6        2009-11-02 15:00:51.177  Stop`  
  
 `7        2009-11-02 15:00:51.180  Central feed in bypass mode.`  
  
### <a name="d-generating-repeating-sequence-numbers-in-a-result-set"></a>D. Generar números de secuencia repetidos en un conjunto de resultados  
 En el siguiente ejemplo se muestran dos características de los números de secuencia: recorrer y utilizar `NEXT VALUE FOR` en una instrucción SELECT.  
  
```  
CREATE SEQUENCE CountBy5  
   AS tinyint  
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 5  
    CYCLE ;  
GO  
  
SELECT NEXT VALUE FOR CountBy5 AS SurveyGroup, Name FROM sys.objects ;  
GO  
```  
  
### <a name="e-generating-sequence-numbers-for-a-result-set-by-using-the-over-clause"></a>E. Generar números de secuencia para un conjunto de resultados mediante la cláusula OVER  
 En el ejemplo siguiente se utiliza la cláusula `OVER` para ordenar el conjunto de resultados por `Name` antes de agregar la columna de número de secuencia.  
  
```  
USE AdventureWorks2012 ;  
GO  
  
CREATE SCHEMA Samples ;  
GO  
  
CREATE SEQUENCE Samples.IDLabel  
    AS tinyint  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="f-resetting-the-sequence-number"></a>F. Restablecer el número de secuencia  
 El ejemplo E consumió los primeros 79 números de secuencia de `Samples.IDLabel`. (Su versión de `AdventureWorks2012` puede devolver un número de resultados diferente). Ejecute lo siguiente para consumir los 79 números de secuencia siguientes (del 80 al 158).  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
 Ejecute la instrucción siguiente para reiniciar la secuencia `Samples.IDLabel` .  
  
```  
ALTER SEQUENCE Samples.IDLabel  
RESTART WITH 1 ;  
```  
  
 Ejecute la instrucción SELECT de nuevo para comprobar que la secuencia `Samples.IDLabel` se ha reiniciado con el número 1.  
  
```  
SELECT NEXT VALUE FOR Samples.IDLabel OVER (ORDER BY Name) AS NutID, ProductID, Name, ProductNumber FROM Production.Product  
WHERE Name LIKE '%nut%' ;  
```  
  
### <a name="g-changing-a-table-from-identity-to-sequence"></a>G. Cambiar una tabla de identidad a secuencia  
 En el siguiente ejemplo se crean un esquema y una tabla que contiene tres filas para el ejemplo. A continuación el ejemplo agrega una nueva columna y quita la columna anterior.  
  
```  
-- Create a schema  
CREATE SCHEMA Test ;  
GO  
  
-- Create a table  
CREATE TABLE Test.Department  
    (  
        DepartmentID smallint IDENTITY(1,1) NOT NULL,  
        Name nvarchar(100) NOT NULL,  
        GroupName nvarchar(100) NOT NULL  
    CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC)   
    ) ;  
GO  
  
-- Insert three rows into the table  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Engineering', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Tool Design', 'Research and Development');  
GO  
  
INSERT Test.Department(Name, GroupName)  
    VALUES ('Sales', 'Sales and Marketing');  
GO  
  
-- View the table that will be changed  
SELECT * FROM Test.Department ;  
GO  
  
-- End of portion creating a sample table  
--------------------------------------------------------  
-- Add the new column that does not have the IDENTITY property  
ALTER TABLE Test.Department   
    ADD DepartmentIDNew smallint NULL  
GO  
  
-- Copy values from the old column to the new column  
UPDATE Test.Department  
    SET DepartmentIDNew = DepartmentID ;  
GO  
  
-- Drop the primary key constraint on the old column  
ALTER TABLE Test.Department  
    DROP CONSTRAINT [PK_Department_DepartmentID];  
-- Drop the old column  
ALTER TABLE Test.Department  
    DROP COLUMN DepartmentID ;  
GO  
  
-- Rename the new column to the old columns name  
EXEC sp_rename 'Test.Department.DepartmentIDNew',   
    'DepartmentID', 'COLUMN';  
GO  
  
-- Change the new column to NOT NULL  
ALTER TABLE Test.Department  
    ALTER COLUMN DepartmentID smallint NOT NULL ;  
-- Add the unique primary key constraint  
ALTER TABLE Test.Department  
    ADD CONSTRAINT PK_Department_DepartmentID PRIMARY KEY CLUSTERED   
         (DepartmentID ASC) ;  
-- Get the highest current value from the DepartmentID column   
-- and create a sequence to use with the column. (Returns 3.)  
SELECT MAX(DepartmentID) FROM Test.Department ;  
-- Use the next desired value (4) as the START WITH VALUE;  
CREATE SEQUENCE Test.DeptSeq  
    AS smallint  
    START WITH 4  
    INCREMENT BY 1 ;  
GO  
  
-- Add a default value for the DepartmentID column  
ALTER TABLE Test.Department  
    ADD CONSTRAINT DefSequence DEFAULT (NEXT VALUE FOR Test.DeptSeq)   
        FOR DepartmentID;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;   
-- Test insert  
INSERT Test.Department (Name, GroupName)  
    VALUES ('Audit', 'Quality Assurance') ;  
GO  
  
-- View the result  
SELECT DepartmentID, Name, GroupName  
FROM Test.Department ;  
GO  
  
```  
  
 Las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] que utilizan `SELECT *` recibirán la nueva columna como última columna, no como primera. Si esto no es aceptable, debe crear una tabla completamente nueva, mover los datos a ella y, a continuación, volver a crear los permisos en la nueva tabla.  
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql)  
  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql)  
  
 [DROP SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-sequence-transact-sql)  
  
 [IDENTITY &#40;propiedad de Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)  
  
  
