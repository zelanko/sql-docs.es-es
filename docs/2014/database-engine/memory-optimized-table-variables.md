---
title: Las Variables de tabla optimizado para memoria | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 485f481819a9712f822f969c04d8e7050ad43bae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774434"
---
# <a name="memory-optimized-table-variables"></a>Variables de tabla con optimización para memoria
  Además de las tablas optimizadas para memoria (para el acceso eficaz a los datos) y los procedimientos almacenados compilados de forma nativa (para el procesamiento de consultas y la ejecución de lógica de negocios de forma eficaz), [!INCLUDE[hek_2](../includes/hek-2-md.md)] presenta una tercera clase de objeto: el tipo de tabla optimizada para memoria. Una variable de tabla creada mediante un tipo de tabla optimizada para memoria es una variable de tabla optimizada para memoria.  
  
 Las variables de tabla con optimización para memoria proporcionan las ventajas siguientes en comparación con las variables de tabla basadas en disco:  
  
-   Las variables solo se almacenan en memoria. El acceso a los datos es más eficaz porque el tipo de tabla optimizada para memoria usa el mismo algoritmo optimizado para memoria y las mismas estructuras de datos usadas para las tablas optimizadas para memoria, especialmente cuando se utilizan las variables en los procedimientos almacenados compilados de forma nativa.  
  
-   Con variables de tabla optimizada para memoria, no se utiliza tempdb. Las variables de tabla no se almacenan en tempdb y no se utiliza ningún recurso de tempdb.  
  
 Los escenarios habituales de uso para las variables de tabla optimizada para memoria son:  
  
-   Almacenar resultados intermedios y crear conjuntos de resultados únicos basándose en varias consultas en procedimientos almacenados compilados de forma nativa.  
  
-   Pasar parámetros con valores de tabla en procedimientos almacenados compilados de forma nativa y procedimientos almacenados interpretados.  
  
-   Reemplazar las variables de tabla basadas en disco y, en algunos casos, las tablas #temp que son locales a un procedimiento almacenado. Esto es especialmente útil si hay mucha contención de tempdb en el sistema.  
  
-   Se pueden usar variables de tabla para simular cursores en los procedimientos almacenados compilados de forma nativa, lo que puede ayudarle a evitar limitaciones del área expuesta en procedimientos almacenados compilados de forma nativa.  
  
 Igual que las tablas optimizadas para memoria, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] genera un archivo DLL para cada tipo de tabla optimizada para memoria. (Compilación se invoca cuando se crea el tipo de tabla optimizada para memoria y no cuando se utiliza para crear las variables de tabla optimizada para memoria). Este archivo DLL incluye las funciones para obtener acceso a los índices y recuperar los datos de las variables de tabla. Cuando una variable de tabla optimizada para memoria se declara basándose en el tipo de tabla, se crea una instancia de las estructuras de tabla y de índice correspondientes al tipo de tabla en la sesión de usuario. La variable de tabla se puede usar del mismo modo que las variables de tabla basadas en disco. Puede insertar, actualizar y eliminar filas en la variable de tabla, y puede usar las variables en las consultas de [!INCLUDE[tsql](../includes/tsql-md.md)] . También puede pasar las variables a procedimientos almacenados compilados de forma nativa e interpretados, como parámetros con valores de tabla (TVP).  
  
 En el ejemplo siguiente se muestra un tipo de tabla optimizada para memoria del ejemplo de OLTP en memoria basado en AdventureWorks ([Ejemplo de OLTP en memoria de SQL Server 2014](https://msftdbprodsamples.codeplex.com/releases/view/114491)).  
  
```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 El ejemplo muestra que la sintaxis de los tipos de tabla optimizada para memoria es similar a los tipos de tabla basados en disco, con las siguientes excepciones:  
  
-   `MEMORY_OPTIMIZED=ON` indica que el tipo de tabla está optimizada para memoria.  
  
-   El tipo debe tener al menos un índice. Como con tablas optimizadas para memoria, puede usar índices de hash e índices no clúster.  
  
     Para un índice de hash, el número de cubos debe ser aproximadamente de una a dos veces el número de claves de índice único esperadas. Para obtener más información, vea [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md).  
  
-   Las restricciones de tipo de datos y restricciones en las tablas optimizadas para memoria se aplican también a los tipos de tabla optimizada para memoria. Por ejemplo, en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] se admiten las restricciones predeterminadas, pero las restricciones CHECK no.  
  
 Al igual que las tablas optimizadas para memoria, las variables de tabla optimizada para memoria  
  
-   No admiten planes paralelos.  
  
-   Deben caber en memoria y no usar recursos de disco.  
  
 Existen variables de tabla basadas en disco en tempdb. Las variables de tabla con optimización para memoria existen en la base de datos de usuario (solo no usan almacenamiento y no se recuperan).  
  
 No puede crear una variable de tabla optimizada para memoria mediante la sintaxis en línea. A diferencia de las variables de tabla basadas en disco, debe crear un tipo en primer lugar.  
  
## <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 El script de ejemplo siguiente muestra la declaración de una variable de tabla como el tipo de tabla optimizada para memoria `Sales.SalesOrderDetailType_inmem`, la inserción de tres filas en la variable y el paso de la variable como un TVP a `Sales.usp_InsertSalesOrder_inmem`.  
  
```sql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 Los tipos de tabla con optimización para memoria se pueden usar como tipo de los parámetros con valores de tabla (TVP) de procedimientos almacenados y los clientes pueden hacer referencia a ellos exactamente igual que los tipos de tabla basados en disco y los TVP. Por tanto, la invocación de procedimientos almacenados con los TVP optimizados para memoria y los procedimientos almacenados compilados de forma nativa funciona exactamente igual que la invocación de procedimientos almacenados interpretados con TVP basados en disco.  
  
## <a name="temp-table-replacement"></a>Reemplazo de la tabla #temp  
 El ejemplo siguiente muestra tipos de tabla de ejemplo optimizadas para memoria y variables de tabla como una sustitución de tablas #temp locales a un procedimiento almacenado.  
  
```sql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>Crear un único conjunto de resultados  
 El ejemplo siguiente muestra cómo almacenar los resultados intermedios y crear conjuntos de resultados únicos basados en varias consultas en procedimientos almacenados compilados de forma nativa. El ejemplo está calculando la unión `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2`.  
  
```sql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>Consumo de memoria para las variables de tabla  
 El consumo de memoria para las variables de tabla es similar al de las tablas optimizadas para memoria, a excepción de los índices no clúster. Si se insertan muchas filas en variables de tabla optimizada para memoria con índices no clúster y si las claves de índice son grandes, estas variables de tabla utilizarán una cantidad de memoria desproporcionada. Los índices no clúster en variables de tabla grandes requieren proporcionalmente más memoria que un índice no clúster necesitaría para el mismo número de filas insertadas en una tabla (más memoria en las páginas de índice).  
  
 La memoria para las variables de tabla procede del grupo de recursos de servidor del Regulador de recursos de la base de datos.  
  
 A diferencia de las tablas optimizadas para memoria, la memoria consumida (incluidas las filas eliminadas) por las variables de tabla se libera cuando la variable de tabla sale del ámbito.  
  
 La memoria se cuenta como parte del único consumidor de memoria PGPOOL de la base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad de Transact-SQL con OLTP en memoria](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
