---
title: Las intercalaciones y páginas de códigos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db4148f2dfa7ce8d0520f71f5027e16c789f62fc
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394545"
---
# <a name="collations-and-code-pages"></a>Intercalaciones y páginas de códigos
  [!INCLUDE[hek_2](../includes/hek-2-md.md)] tiene restricciones en cuanto a las páginas de códigos compatibles para las columnas (var)char en las tablas optimizadas para memoria y las intercalaciones compatibles empleadas en índices y procedimientos almacenados compilados de forma nativa.  
  
 La página de códigos para un valor (var)char determina la asignación entre los caracteres y la representación de bytes que se almacena en la tabla. Por ejemplo, con la página de códigos del alfabeto Latin 1 de Windows (1252; el valor predeterminado de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]), el carácter 'a' corresponde al byte 0x61.  
  
 La página de códigos de un valor (var)char determina la intercalación asociada al valor. Por ejemplo, la intercalación SQL_Latin1_General_CP1_CI_AS tiene la página de códigos asociada 1252.  
  
 La intercalación de un valor se hereda de la intercalación de la base de datos o se puede especificar explícitamente mediante la palabra clave COLLATE. La intercalación de base de datos no se puede cambiar si la base de datos contiene tablas optimizadas para memoria o procedimientos almacenados compilados de forma nativa. El ejemplo siguiente establece la intercalación de base de datos y crea una tabla, que tiene una columna con una intercalación diferente. La base de datos utiliza la intercalación sin distinción entre mayúsculas y minúsculas latina.  
  
 Los índices se pueden crear en columnas de cadena si utilizan una intercalación BIN2. La variable LastName utiliza la intercalación BIN2. FirstName utiliza el valor predeterminado de la base de datos, que es CI_AS (sin distinción entre mayúsculas y minúsculas, y con distinción de acentos).  
  
> [!IMPORTANT]  
>  No puede usar order by o group by en columnas de cadena de índice que no empleen la intercalación BIN2.  
  
```tsql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 Las restricciones siguientes se aplican a las tablas optimizadas para memoria y a los procedimientos almacenados compilados de forma nativa:  
  
-   Las columnas (var)char de las tablas optimizadas para memoria deben utilizar la intercalación de la página de códigos 1252. Esta restricción no se aplica a las columnas n(var)char. El código siguiente recupera todas las intercalaciones 1252:  
  
    ```tsql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     Si necesita almacenar caracteres que no sean Latin, use columnas n(var)char.  
  
-   Los índices en columnas (n)(var)char solo se pueden especificar con intercalaciones BIN2 (vea el primer ejemplo). La consulta siguiente recupera todas las intercalaciones BIN2 admitidas:  
  
    ```tsql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     Si tiene acceso a la tabla con [!INCLUDE[tsql](../includes/tsql-md.md)]interpretado, puede utilizar la palabra clave `COLLATE` para cambiar la intercalación con expresiones o con operaciones de ordenación. Vea el ejemplo anterior para obtener un ejemplo de esto.  
  
-   Los procedimientos almacenados compilados de forma nativa no pueden utilizar parámetros, variables locales ni constantes de cadena de tipo (var)char si la intercalación de base de datos no es una intercalación de página de códigos 1252.  
  
-   Todas las expresiones y operaciones de ordenación dentro de procedimientos almacenados compilados de forma nativa deben utilizar intercalaciones BIN2. La implicación es que todas las comparaciones y las operaciones de ordenación están basadas en los puntos de código Unicode de los caracteres (representaciones binarias). Por ejemplo, toda la clasificación distingue entre mayúsculas y minúsculas (la “Z” va antes de la “a”). Si fuera necesario, utilice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretado para la ordenación sin distinción entre mayúsculas y minúsculas y la comparación.  
  
-   El truncamiento de los datos UTF-16 no se admite dentro de procedimientos almacenados compilados de forma nativa. Esto significa que char n (var) (*n*) los valores no se puede convertir al tipo n (var) char (*i*), si *i* < *n*, si el intercalación tiene la propiedad _SC. Por ejemplo, la siguiente vista no se admite:  
  
    ```tsql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     Las funciones de manipulación de cadenas, como LEN, SUBSTRING, LTRIM y RTRIM y con datos UTF-16 no son procedimientos almacenados compilados de forma nativa admitidos. No puede utilizar estas funciones de manipulación de cadenas para valores n(var)char que tengan una intercalación _SC.  
  
     Declare las variables con tipos lo suficientemente grandes para evitar el truncamiento.  
  
 El ejemplo siguiente muestra algunas de las implicaciones y las soluciones alternativas para las limitaciones de la intercalación en OLTP en memoria. El ejemplo utiliza la tabla employees especificada anteriormente. En este ejemplo se enumeran todos los empleados. Observe que, para LastName, debido a la intercalación binaria, los nombres en mayúsculas se clasifican antes que los nombres en minúsculas. Por consiguiente, 'Thomas' viene antes de 'nolan' porque los caracteres en mayúsculas tienen puntos de código inferiores. FirstName tiene una intercalación sin distinción entre mayúsculas y minúsculas. Así, la clasificación se realiza según la letra del alfabeto, no por el punto de código de los caracteres.  
  
```tsql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
