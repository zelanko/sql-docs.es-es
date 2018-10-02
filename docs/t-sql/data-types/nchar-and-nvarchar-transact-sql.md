---
title: nchar y nvarchar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nvarchar data type
- nchar data type
ms.assetid: 81ee5637-ee31-4c4d-96d0-56c26a742354
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ca8eb44756561bd8a4a4a0ddce43f6f321bdf72
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47733503"
---
# <a name="nchar-and-nvarchar-transact-sql"></a>nchar y nvarchar (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos de caracteres para datos Unicode de longitud fija, **nchar** o de longitud variable, **nvarchar**, y que usan el juego de caracteres UNICODE UCS-2.
  
## <a name="arguments"></a>Argumentos  
**nchar** [ ( n ) ]  
Datos de cadena Unicode de longitud fija. *n* define la longitud de la cadena y debe ser un valor entre 1 y 4.000. El tamaño de almacenamiento es dos veces *n* bytes. Si la página de códigos de la intercalación usa caracteres de doble byte, el tamaño de almacenamiento sigue siendo de *n* bytes. Dependiendo de la cadena, el tamaño de almacenamiento de *n* bytes puede ser inferior al valor especificado para *n*. Los sinónimos ISO de **nchar** son **national char** y **national character**.
  
**nvarchar** [ ( n | **max** ) ]  
Datos de cadena Unicode de longitud variable. *n* define la longitud de la cadena y puede ser un valor entre 1 y 4.000. **max** indica que el tamaño máximo de almacenamiento es de 2^30-1 caracteres.  El tamaño de almacenamiento máximo en bytes es de 2 GB. El tamaño de almacenamiento real, en bytes, es dos veces el número de caracteres especificado + 2 bytes. Los sinónimos ISO de **nvarchar** son **national char varying** y **national character varying**.
  
## <a name="remarks"></a>Notas  
Cuando no se especifica el argumento *n* en una instrucción de definición de datos o de declaración de variable, la longitud predeterminada es 1. Cuando no se especifica *n* con la función CAST, la longitud predeterminada es 30.
  
Use **nchar** cuando sea probable que el tamaño de las entradas de datos de las columnas sea similar.
  
Use **nvarchar** cuando sea probable que el tamaño de las entradas de datos de las columnas varíe.
  
**sysname** es un tipo de datos definido por el usuario y suministrado por el sistema que es funcionalmente equivalente a **nvarchar(128)**, excepto que no acepta valores NULL. **sysname** se usa para hacer referencia a nombres de objetos de base de datos.
  
Los objetos que usan **nchar** o **nvarchar** se asignan a la intercalación predeterminada de la base de datos, a menos que se asigne una intercalación específica por medio de la cláusula COLLATE.
  
SET ANSI_PADDING siempre es ON para **nchar** y **nvarchar**. SET ANSI_PADDING OFF no se aplica a los tipos de datos **nchar** ni **nvarchar**.
  
Anteponga el prefijo N en las constantes de cadena de caracteres Unicode. Sin este prefijo, la cadena se convierte en la página de códigos predeterminada de la base de datos. Esta página de códigos predeterminada puede no reconocer determinados caracteres.
 
> [!NOTE]  
>  Cuando se antepone un prefijo con la letra N en una constante de cadena, la conversión implícita dará como resultado una cadena Unicode si la constante que se convierte no supera la longitud máxima de un tipo de datos de cadena Unicode (4000). En caso contrario, la conversión implícita generará un valor grande de Unicode (max).
  
> [!WARNING]  
>  Cada columna **varchar(max)** o **nvarchar(max)** cuyo valor no sea NULL requiere 24 bytes de asignación fija adicional, que se descuentan del límite de 8.060 bytes de las filas durante una operación de ordenación. Estos bytes adicionales pueden crear un límite implícito del número de columnas **varchar(max)** o **nvarchar(max)** cuyo valor no sea NULL en una tabla. No se produce ningún error especial cuando se crea la tabla (más allá de la advertencia habitual de que el tamaño máximo de la fila supera el máximo permitido de 8060 bytes) ni en el momento de la inserción de los datos. Este gran tamaño de fila puede provocar errores (como el error 512) que los usuarios no puedan prever durante algunas operaciones habituales.  Dos ejemplos de operaciones son las actualizaciones de la clave de índice agrupado o las ordenaciones del conjunto de columnas completo.
  
## <a name="converting-character-data"></a>Convertir datos de caracteres  
Para más información sobre cómo convertir datos de caracteres, vea [char y varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md).
  
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
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)
  
  
