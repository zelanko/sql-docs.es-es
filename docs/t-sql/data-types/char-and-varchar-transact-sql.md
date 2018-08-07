---
title: char y varchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 48
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a8e8eb43fd5dffa9ae1047730bcb17075d2204d8
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454889"
---
# <a name="char-and-varchar-transact-sql"></a>char y varchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Estos tipos de datos son de longitud fija o variable.  
  
## <a name="arguments"></a>Argumentos  
**char** [ ( *n* ) ] Datos de cadena no Unicode de longitud fija. *n* define la longitud de la cadena y debe ser un valor entre 1 y 8.000. El tamaño de almacenamiento es de *n* bytes. El sinónimo ISO para **char** es **character**.
  
**varchar** [ ( *n* | **max** ) ] Datos de cadena no Unicode de longitud variable. *n* define la longitud de la cadena y puede ser un valor entre 1 y 8.000. **max** indica que el tamaño máximo de almacenamiento es de 2^31-1 bytes (2 GB). El tamaño de almacenamiento es la longitud real de los datos especificados + 2 bytes. Los sinónimos ISO para **varchar** son **charvarying** o **charactervarying**.
  
## <a name="remarks"></a>Notas  
Cuando no se especifica el argumento *n* en una instrucción de definición de datos o de declaración de variable, la longitud predeterminada es 1. Cuando no se especifica *n* al usar las funciones CAST y CONVERT, la longitud predeterminada es 30.
  
Los objetos que utilizan **char** o **varchar** se asignan a la intercalación predeterminada de la base de datos, a menos que se asigne una intercalación específica por medio de la cláusula COLLATE. La intercalación controla la página de códigos utilizada para almacenar los datos de caracteres.
  
Si tiene sitios que admiten varios idiomas, considere el uso de tipos de datos Unicode **nchar** o **nvarchar** para reducir al mínimo los problemas de conversión de caracteres. Si usa **char** o **varchar**, siga estas recomendaciones:
- Utilice **char** cuando los tamaños de las entradas de datos de columna sean coherentes.  
- Use **varchar** cuando los tamaños de las entradas de datos de columna varíen considerablemente.  
- Utilice **varchar(max)** cuando los tamaños de las entradas de datos de columna varíen de forma considerable y se pudieran superar los 8000 bytes.  
  
Si SET ANSI_PADDING es OFF cuando se ejecuta CREATE TABLE o ALTER TABLE, una columna de tipo **char** definida como NULL se trata como si fuera de tipo **varchar**.
  
Si la página de códigos de la intercalación usa caracteres de doble byte, el tamaño de almacenamiento sigue siendo de *n* bytes. Dependiendo de la cadena de caracteres, el tamaño de almacenamiento de *n* bytes puede ser inferior a *n* caracteres.

> [!WARNING]
> Cada columna varchar(max) o nvarchar(max) cuyo valor no sea NULL requiere 24 bytes de asignación fija adicional que se descuentan del límite de 8060 bytes de las filas durante una operación de ordenación. Esto puede crear un límite implícito del número de columnas varchar(max) o varchar(max) cuyo valor no sea NULL que es posible crear en una tabla.  
No se produce ningún error especial cuando se crea la tabla (más allá de la advertencia habitual de que el tamaño máximo de la fila supera el máximo permitido de 8060 bytes) ni en el momento de la inserción de los datos. Este tamaño de fila grande puede provocar errores (como el error 512) durante algunas operaciones normales, como una actualización de claves de índices agrupados u ordenaciones del conjunto completo de columnas, que los usuarios no pueden prever hasta que lleven a cabo alguna operación.
  
##  <a name="_character"></a> Convertir datos de caracteres  
Cuando se convierten expresiones de caracteres a un tipo de datos de caracteres de un tamaño distinto, se truncan los valores que son demasiado grandes para el nuevo tipo de datos. El tipo **uniqueidentifier** se considera un tipo de carácter para la conversión desde una expresión de caracteres y, por tanto, está sujeto a las reglas de truncamiento para la conversión a un tipo de carácter. Vea la sección Ejemplos que aparece más adelante.
  
Cuando una expresión de caracteres se convierte a una expresión de caracteres de un tipo de datos o tamaño distinto (como de **char(5)** a **varchar(5)** o de **char(20)** a **char(15)**), se asigna la intercalación del valor de entrada al valor convertido. Si una expresión que no es de carácter se convierte a un tipo de datos de carácter, se asigna al valor convertido la intercalación predeterminada de la base de datos actual. En cualquiera de los casos, puede asignar una intercalación específica mediante la cláusula [COLLATE](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9).
  
> [!NOTE]  
>  Las traducciones de páginas de códigos se admiten para los tipos de datos **char** y **varchar**, pero no para el tipo de datos **text**. Al igual que en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], las pérdidas de datos durante las conversiones de la página de códigos no se notifican.  
  
Las expresiones de carácter que se convierten a un tipo de datos **numeric** aproximado pueden incluir una notación exponencial opcional (una e minúscula o una E mayúscula seguida de un signo más (+) o menos (-) opcional y un número).
  
Las expresiones de carácter que se convierten a un tipo de datos **numeric** exacto se componen de dígitos, un separador decimal y un signo más (+) o menos (-) opcional. Los espacios en blanco iniciales se omiten. En la cadena no se permiten los separadores de coma (como el separador de miles en algunas representaciones de 123,456.00).
  
Las expresiones de caracteres que se convierten a los tipos de datos **money** o **smallmoney** pueden incluir también un separador decimal opcional y un símbolo de dólar ($). Los separadores de coma (por ejemplo, $123,456.00) están permitidos.
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-showing-the-default-value-of-n-when-used-in-variable-declaration"></a>A. Mostrar el valor predeterminado de n cuando se usa en una declaración de variable.  
En el ejemplo siguiente se muestra que el valor predeterminado de *n* es 1 para los tipos de datos `char` y `varchar` cuando se usan en una declaración de variable.
  
```sql
DECLARE @myVariable AS varchar = 'abc';  
DECLARE @myNextVariable AS char = 'abc';  
--The following returns 1  
SELECT DATALENGTH(@myVariable), DATALENGTH(@myNextVariable);  
GO  
```  
  
### <a name="b-showing-the-default-value-of-n-when-varchar-is-used-with-cast-and-convert"></a>B. Mostrar el valor predeterminado de n cuando varchar se usa con CAST y CONVERT.  
En el ejemplo siguiente se muestra que el valor predeterminado de *n* es 30 cuando se usa el tipo de datos `char` o `varchar` con las funciones `CAST` y `CONVERT`.
  
```sql
DECLARE @myVariable AS varchar(40);  
SET @myVariable = 'This string is longer than thirty characters';  
SELECT CAST(@myVariable AS varchar);  
SELECT DATALENGTH(CAST(@myVariable AS varchar)) AS 'VarcharDefaultLength';  
SELECT CONVERT(char, @myVariable);  
SELECT DATALENGTH(CONVERT(char, @myVariable)) AS 'VarcharDefaultLength';  
```  
  
### <a name="c-converting-data-for-display-purposes"></a>C. Convertir datos para mostrarlos  
En el ejemplo siguiente se convierten dos columnas a tipos de caracteres y se aplica un estilo que aplica un formato concreto a los datos mostrados. Un tipo **money** se convierte en datos de caracteres y se aplica el estilo 1, que muestra los valores con comas cada tres dígitos a la izquierda del separador decimal y dos dígitos a la derecha del separador decimal. Un tipo **datetime** se convierte en datos de caracteres y se aplica el estilo 3, que muestra los datos en el formato dd/mm/aa. En la cláusula WHERE, un tipo **money** se convierte en un tipo de caracteres para realizar una operación de comparación de cadenas.
  
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
  
En el ejemplo siguiente se muestra el truncamiento de los datos cuando el valor es demasiado largo para el tipo de datos al que se va a convertir. Como el tipo **uniqueidentifier** tiene un límite de 36 caracteres, se truncan los caracteres que superan esa longitud.
  
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
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[Conversiones de tipos de datos &#40;motor de base de datos&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)
  
  
