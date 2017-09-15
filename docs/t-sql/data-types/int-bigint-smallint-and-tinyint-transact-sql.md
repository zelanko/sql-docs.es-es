---
title: int, bigint, smallint y tinyint (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bigint_TSQL
- smallint
- bigint
- smallint_TSQL
- tinyint_TSQL
- int_TSQL
- int
- tinyint
dev_langs:
- TSQL
helpviewer_keywords:
- exact numeric data [SQL Server]
- numeric data
- tinyint data type
- int data type
- smallint data type
ms.assetid: 9bda5b0b-2380-4931-a1c8-f362fdefa99b
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 46ac51971b07b38b73ef18d8a953674fc77b4b17
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="int-bigint-smallint-and-tinyint-transact-sql"></a>int, bigint, smallint y tinyint (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos numéricos exactos que utilizan datos enteros. Para ahorrar espacio en la base de datos, utilice el tipo de datos más pequeño que puede contener de forma confiable todos los valores posibles. Por ejemplo, tinyint sería suficiente para una antigüedad de las personas, ya que nadie vive a tener más de 255 años. Pero tinyint no sería suficiente para una antigüedad de edificios, dado que un edificio puede ser más de 255 años de antigüedad.
  
|Tipo de datos|Intervalo|Almacenamiento|  
|---|---|---|
|**bigint**|De -2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807)|8 bytes|  
|**int**|De -2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647)|4 bytes|  
|**smallint**|De -2^15 (-32.768) a 2^15-1 (32.767)|2 bytes|  
|**tinyint**|De 0 a 255|1 byte|  
  
## <a name="remarks"></a>Comentarios  
El **int** tipo de datos es el tipo de datos entero principal en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El **bigint** tipo de datos está pensado para su uso cuando valores enteros pueden exceder el intervalo que sea compatible con la **int** tipo de datos.
  
**bigint** se encuentra entre **smallmoney** y **int** en el gráfico de precedencia del tipo de datos.
  
Las funciones devuelven **bigint** sólo si la expresión de parámetro es un **bigint** tipo de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no promueve automáticamente otros tipos de datos enteros (**tinyint**, **smallint**, y **int**) a **bigint**.
  
> [!CAUTION]  
>  Cuando se usa el +, -, \*, /, o % operadores aritméticos para realizar la conversión implícita o explícita de **int**, **smallint**, **tinyint**, o ** bigint** valores constantes para el **float**, **real**, **decimal** o **numérico** tipos de datos, las reglas que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplica al calcular el tipo de datos y la precisión de los resultados de la expresión difieren en función de si la consulta tiene parámetros automáticos o no.  
>   
>  Por lo tanto, expresiones similares en las consultas pueden generar resultados diferentes. Cuando una consulta no tiene parámetros automáticos, el valor constante primero se convierte en **numérico**, cuya precisión es suficientemente grande como para contener el valor de la constante, antes de convertir al tipo de datos especificado. Por ejemplo, el valor constante 1 se convierte en **numeric (1, 0)**, y el valor constante 250 se convierte en **numeric (3, 0)**.  
>   
>  Cuando una consulta tiene parámetros automáticos, el valor constante siempre se convierte en **numeric (10, 0)** antes de convertir al tipo de datos final. Cuando se utiliza el operador /, no solo puede diferir la precisión del tipo de los resultados entre consultas similares, sino que también puede variar el valor de los resultados. Por ejemplo, el valor de resultado de una consulta con parámetros automáticos que incluye la expresión `SELECT CAST (1.0 / 7 AS float)`, difiere del valor de resultado de la misma consulta que no tenga parámetros automáticos, porque los resultados de la consulta con parámetros automáticos, se trunca para ajustarse al el **numeric (10, 0)** tipo de datos.  
  
## <a name="converting-integer-data"></a>Convertir datos enteros
Cuando se convierten implícitamente enteros en un tipo de datos de caracteres, si el entero es demasiado grande para ajustarse al campo de carácter, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe el carácter ASCII 42, el asterisco (*).
  
Constantes de enteros mayores que 2.147.483.647 se convierten a la **decimal** tipo de datos, no el **bigint** tipo de datos. En el ejemplo siguiente se muestra que, cuando se supera el valor de umbral, el tipo de datos del resultado cambia de un **int** a una **decimal**.
  
```sql
SELECT 2147483647 / 2 AS Result1, 2147483649 / 2 AS Result2 ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result1      Result2  
1073741823   1073741824.500000  
```  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se crea una tabla con el **bigint**, **int**, **smallint**, y **tinyint** tipos de datos. Se insertan valores en cada columna y se devuelven en la instrucción SELECT.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyBigIntColumn bigint  
,MyIntColumn  int
,MySmallIntColumn smallint
,MyTinyIntColumn tinyint
);  
  
GO  
  
INSERT INTO dbo.MyTable VALUES (9223372036854775807, 2147483647,32767,255);  
 GO  
SELECT MyBigIntColumn, MyIntColumn, MySmallIntColumn, MyTinyIntColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyBigIntColumn       MyIntColumn MySmallIntColumn MyTinyIntColumn  
-------------------- ----------- ---------------- ---------------  
9223372036854775807  2147483647  32767            255  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

