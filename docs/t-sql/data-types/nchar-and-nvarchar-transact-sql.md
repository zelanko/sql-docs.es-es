---
title: nchar y nvarchar (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc7de3b64519f3d0fd1f2e9557ccf7196e3f07a8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar y nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos que son de longitud fija, caracteres **nchar**, o de longitud variable, **nvarchar**, juego de caracteres de datos Unicode y use el UNICODE UCS-2.
  
## <a name="arguments"></a>Argumentos  
**nchar** [(n)]  
Datos de cadena Unicode de longitud fija. *n*define la longitud de cadena y debe estar comprendido entre 1 y 4.000. El tamaño de almacenamiento es dos veces  *n*  bytes. Cuando la página de códigos de la intercalación utiliza caracteres de doble byte, el tamaño de almacenamiento sigue siendo  *n*  bytes. Dependiendo de la cadena, el tamaño de almacenamiento de  *n*  bytes puede ser menor que el valor especificado para  *n* . Los sinónimos ISO de **nchar** son **national char** y **caracteres no nacionales**...
  
**nvarchar** [(n | **max** )]  
Datos de cadena Unicode de longitud variable. *n*define la longitud de cadena y puede ser un valor entre 1 y 4.000. **max** indica que el tamaño máximo de almacenamiento es 2 ^ 31-1 bytes (2 GB). El tamaño de almacenamiento, en bytes, es dos veces la longitud real de los datos especificados + 2 bytes. Los sinónimos ISO de **nvarchar** son **variación car** y **national character varying de**.
  
## <a name="remarks"></a>Comentarios  
Cuando  *n*  no se especifica en una definición de datos o la instrucción de declaración de variable, la longitud predeterminada es 1. Cuando  *n*  no se especifica con la función CAST, la longitud predeterminada es 30.
  
Use **nchar** cuando los tamaños de las entradas de datos de columna probablemente se van a ser similares.
  
Use **nvarchar** cuando los tamaños de las entradas de datos de columna probablemente va a variar considerablemente.
  
**sysname** es un tipo de datos proporcionado por sistema definido por el usuario que es funcionalmente equivalente a **nvarchar (128)**, salvo que no acepta valores NULL. **sysname** se usa para hacer referencia a nombres de objeto de base de datos.
  
Objetos que utilizan **nchar** o **nvarchar** se asigna la intercalación predeterminada de la base de datos a menos que se asigne una intercalación específica mediante la cláusula COLLATE.
  
SET ANSI_PADDING está siempre activado para **nchar** y **nvarchar**. SET ANSI_PADDING OFF no se aplica a la **nchar** o **nvarchar** tipos de datos.
  
Prefijo de las constantes de cadena de caracteres Unicode con la letra N. Sin el prefijo N, la cadena se convierte en la página de códigos predeterminada de la base de datos. Esta página de códigos predeterminada puede no reconocer determinados caracteres.
 
> [!NOTE]  
>  Cuando un prefijo de una constante de cadena con la letra N, se producirá la conversión implícita en una cadena Unicode si la constante para convertir no supera la longitud máxima para un tipo de datos de cadena Unicode (4.000). En caso contrario, se producirá la conversión implícita en un Unicode valores grandes (max).
  
> [!WARNING]  
>  Cada usuario que no sea null **varchar (max)** o **nvarchar (max)** columna requiere 24 bytes de asignación fija adicional que se descuentan del límite de 8.060 bytes de filas durante una operación de ordenación. Esto puede crear un límite al número de no null implícito **varchar (max)** o **nvarchar (max)** columnas que se pueden crear en una tabla. No se produce ningún error especial cuando se crea la tabla (más allá de la advertencia habitual de que el tamaño máximo de la fila supera el máximo permitido de 8060 bytes) ni en el momento de la inserción de los datos. Este tamaño de fila grande puede provocar errores (como el error 512) durante algunas operaciones normales, como una actualización de claves de índices agrupados u ordenaciones del conjunto completo de columnas, que los usuarios no pueden prever hasta que lleven a cabo alguna operación.  
  
## <a name="converting-character-data"></a>Convertir datos de caracteres  
Para obtener información sobre cómo convertir datos de caracteres, vea [char y varchar &#40; Transact-SQL &#41; ](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyNCharColumn nchar(15)  
,MyNVarCharColumn nvarchar(20)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (N'Test data', N'More test data');  
GO  
SELECT MyNCharColumn, MyNVarCharColumn  
FROM dbo.MyTable;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyNCharColumn   MyNVarCharColumn  
--------------- --------------------  
Test data       More test data  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40; Transact-SQL &#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
  
  

