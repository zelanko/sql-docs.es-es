---
title: char y varchar (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- varchar
- varchar_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fixed-length data types [SQL Server]
- character data type
- char data type
- varchar(max) data type
- variable-length data types [SQL Server]
- varchar data type
ms.assetid: 282cd982-f4fb-4b22-b2df-9e8478f13f6a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 4c383e3b3ff5b79604454f80443c9042633797bf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="char-and-varchar-transact-sql"></a>char y varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Estos tipos de datos son de longitud fija o de longitud variable.  
  
## <a name="arguments"></a>Argumentos  
**char** [(  *n*  )] longitud fija, datos de cadena no Unicode. *n*define la longitud de cadena y debe ser un valor entre 1 y 8.000. El tamaño de almacenamiento es  *n*  bytes. El sinónimo ISO para **char** es **caracteres**.
  
**varchar** [(  *n*   |  **max** )] longitud Variable, datos de cadena no Unicode. *n*define la longitud de cadena y puede ser un valor entre 1 y 8.000. **max** indica que el tamaño máximo de almacenamiento es 2 ^ 31-1 bytes (2 GB). El tamaño de almacenamiento es la longitud real de los datos especificados + 2 bytes. Los sinónimos ISO de **varchar** son **charvarying** o **charactervarying**.
  
## <a name="remarks"></a>Comentarios  
Cuando  *n*  no se especifica en una definición de datos o la instrucción de declaración de variable, la longitud predeterminada es 1. Cuando  *n*  no se especifica al utilizar las funciones CAST y CONVERT, la longitud predeterminada es 30.
  
Objetos que utilizan **char** o **varchar** se asigna la intercalación predeterminada de la base de datos, a menos que se asigne una intercalación específica mediante la cláusula COLLATE. La intercalación controla la página de códigos utilizada para almacenar los datos de caracteres.
  
Si tiene sitios que admiten varios idiomas, considere el uso de Unicode **nchar** o **nvarchar** tipos de datos para minimizar los problemas de conversión de caracteres. Si usa **char** o **varchar**, se recomienda lo siguiente:
- Use **char** cuando los tamaños de las entradas de datos de columna son coherentes.  
- Use **varchar** cuando los tamaños de las entradas de datos de columna varíen considerablemente.  
- Use **varchar (max)** cuando los tamaños de las entradas de datos de columna varíen considerablemente y el tamaño puede superar los 8.000 bytes.  
  
Si SET ANSI_PADDING es OFF cuando se ejecuta CREATE TABLE o ALTER TABLE, un **char** columna definida como NULL se trata como **varchar**.
  
Cuando la página de códigos de la intercalación utiliza caracteres de doble byte, el tamaño de almacenamiento sigue siendo  *n*  bytes. Dependiendo de la cadena de caracteres, el tamaño de almacenamiento de  *n*  bytes puede ser inferior a  *n*  caracteres.

> [!WARNING]
> Cada no null varchar (max) o nvarchar (max) columna requiere 24 bytes de asignación fija adicional que se descuentan del límite de 8.060 bytes de filas durante una operación de ordenación. Esto puede crear un límite implícito en el número de columnas de nvarchar (max) que se pueden crear en una tabla o no null varchar (max).  
No se produce ningún error especial cuando se crea la tabla (más allá de la advertencia habitual de que el tamaño máximo de la fila supera el máximo permitido de 8060 bytes) ni en el momento de la inserción de los datos. Este tamaño de fila grande puede provocar errores (como el error 512) durante algunas operaciones normales, como una actualización de claves de índices agrupados u ordenaciones del conjunto completo de columnas, que los usuarios no pueden prever hasta que lleven a cabo alguna operación.
  
##  <a name="_character"></a>Convertir datos de caracteres  
Cuando se convierten expresiones de caracteres a un tipo de datos de caracteres de un tamaño distinto, se truncan los valores que son demasiado grandes para el nuevo tipo de datos. El **uniqueidentifier** tipo se considera un tipo de carácter para los fines de conversión de una expresión de caracteres y, por tanto, está sujeto a las reglas de truncamiento para convertir a un tipo de carácter. Vea la sección Ejemplos que aparece más adelante.
  
Cuando una expresión de caracteres se convierte en una expresión de caracteres de un tipo de datos diferente o el tamaño, como de **char (5)** a **varchar (5)**, o **char(20)** a **char (15)**, se asigna la intercalación del valor de entrada para el valor convertido. Si una expresión que no es de carácter se convierte a un tipo de datos de carácter, se asigna al valor convertido la intercalación predeterminada de la base de datos actual. En cualquier caso, puede asignar una intercalación específica mediante la [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9) cláusula.
  
> [!NOTE]  
>  Traducción de página de códigos se admite para **char** y **varchar** tipos de datos, pero no para **texto** tipo de datos. Al igual que en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las pérdidas de datos durante las conversiones de la página de códigos no se notifican.  
  
Expresiones de carácter que se convierten a un valor aproximado **numérico** tipo de datos puede incluir una notación exponencial opcional (una e minúscula o E mayúscula seguida de un signo opcional más (+) o menos (-) inicio de sesión y, a continuación, un número).
  
Expresiones de carácter que se convierten a un exacta **numérico** tipo de datos puede contener dígitos, un separador decimal y un elemento opcional más (+) o menos (-). Los espacios en blanco iniciales se omiten. En la cadena no se permiten los separadores de coma (como el separador de miles en algunas representaciones de 123,456.00).
  
Carácter que se va a convertir en las expresiones **dinero** o **smallmoney** tipos de datos también pueden incluir un punto decimal opcional y un signo de dólar ($). Los separadores de coma (por ejemplo, $123,456.00) están permitidos.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. Mostrar el valor predeterminado de n cuando se usa en una declaración de variable.  
En el ejemplo siguiente se muestra el valor predeterminado de  *n*  es 1 para el `char` y `varchar` tipos de datos cuando se utilizan en la declaración de variable.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. Mostrar el valor predeterminado de n cuando varchar se usa con CAST y CONVERT.  
En el ejemplo siguiente se muestra que el valor predeterminado de  *n*  es 30 cuando la `char` o `varchar` tipos de datos se usan con la `CAST` y `CONVERT` funciones.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. Convertir datos para mostrarlos  
En el ejemplo siguiente se convierten dos columnas a tipos de caracteres y se aplica un estilo que aplica un formato concreto a los datos mostrados. A **dinero** tipo se convierte en datos de caracteres y se aplica el estilo 1, que muestra los valores con comas cada tres dígitos a la izquierda del separador decimal y dos dígitos a la derecha del separador decimal. A **datetime** tipo se convierte en datos de caracteres y se aplica el estilo 3, que muestra los datos en el formato mm/dd/aa. En la cláusula WHERE, una **dinero** tipo se convierte en un tipo de carácter para realizar una operación de comparación de cadenas.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  BusinessEntityID,   
   SalesYTD,   
   CONVERT (varchar(12),SalesYTD,1) AS MoneyDisplayStyle1,   
   GETDATE() AS CurrentDate,   
   CONVERT(varchar(12), GETDATE(), 3) AS DateDisplayStyle3  
FROM Sales.SalesPerson  
WHERE CAST(SalesYTD AS varchar(20) ) LIKE '1%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
BusinessEntityID SalesYTD              DisplayFormat CurrentDate             DisplayDateFormat  
---------------- --------------------- ------------- ----------------------- -----------------  
278              1453719.4653          1,453,719.47  2011-05-07 14:29:01.193 07/05/11  
280              1352577.1325          1,352,577.13  2011-05-07 14:29:01.193 07/05/11  
283              1573012.9383          1,573,012.94  2011-05-07 14:29:01.193 07/05/11  
284              1576562.1966          1,576,562.20  2011-05-07 14:29:01.193 07/05/11  
285              172524.4512           172,524.45    2011-05-07 14:29:01.193 07/05/11  
286              1421810.9242          1,421,810.92  2011-05-07 14:29:01.193 07/05/11  
288              1827066.7118          1,827,066.71  2011-05-07 14:29:01.193 07/05/11  
```  
  
### <a name="d-converting-uniqueidentifer-data"></a>D. Convertir datos Uniqueidentifier  
En el ejemplo siguiente se convierte un valor `uniqueidentifier` a un tipo de datos `char`.
  
```sql
DECLARE @myid uniqueidentifier = NEWID();  
SELECT CONVERT(char(255), @myid) AS 'char';  
```  
  
En el ejemplo siguiente se muestra el truncamiento de los datos cuando el valor es demasiado largo para el tipo de datos al que se va a convertir. Dado que la **uniqueidentifier** tipo está limitado a 36 caracteres, se truncan los caracteres que superan esa longitud.
  
```sql
DECLARE @ID nvarchar(max) = N'0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong';  
SELECT @ID, CONVERT(uniqueidentifier, @ID) AS TruncatedValue;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
String                                       TruncatedValue  
-------------------------------------------- ------------------------------------  
0E984725-C51C-4BF4-9960-E1C80E27ABA0wrong    0E984725-C51C-4BF4-9960-E1C80E27ABA0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[nchar y nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  
