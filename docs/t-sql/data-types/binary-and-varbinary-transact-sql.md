---
title: binary y varbinary (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 8/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- binary_TSQL
- varbinary_TSQL
- binary
- varbinary
dev_langs:
- TSQL
helpviewer_keywords:
- varbinary data type
- binary [SQL Server], about binary data type
ms.assetid: bcce65f9-10db-4b3e-bfaf-dfc06c6f820f
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6aaf00b8e846316c92897360932703a013150e8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="binary-and-varbinary-transact-sql"></a>binary y varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos binarios de longitud fija o variable.
  
## <a name="arguments"></a>Argumentos  
**binario** [(  *n*  )] datos binarios de longitud fija con una longitud de  *n*  bytes, donde  *n*  es un valor entre 1 y 8.000. El tamaño de almacenamiento es  *n*  bytes.
  
**varbinary** [(  *n*   |  **max**)] datos binarios de longitud Variable. *n*puede ser un valor entre 1 y 8.000. **max** indica que el tamaño máximo de almacenamiento es 2 ^ 31-1 bytes. El tamaño de almacenamiento es la longitud real de los datos especificados + 2 bytes. Los datos especificados pueden tener una longitud de 0 bytes. El sinónimo de ANSI SQL para **varbinary** es **variable binario**.
  
## <a name="remarks"></a>Comentarios  
Cuando  *n*  no se especifica en una definición de datos o la instrucción de declaración de variable, la longitud predeterminada es 1. Cuando  *n*  no se especifica con la función CAST, la longitud predeterminada es 30.

| Tipo de datos | Se utiliza si... |
| --- | --- |
| **binario** | los tamaños de las entradas de datos de columna son coherentes.|
| **varbinary** | los tamaños de las entradas de datos de columna varíen considerablemente.|
| **varbinary(max)** | las entradas de datos de columna superen los 8.000 bytes.|


## <a name="converting-binary-and-varbinary-data"></a>Convertir datos binary y varbinary
Cuando se convierten datos de un tipo de datos de cadena (**char**, **varchar**, **nchar**, **nvarchar**, **binario**, **varbinary**, **texto**, **ntext**, o **imagen**) a un **binario** o **varbinary** tipo de datos de diferente longitud, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena o trunca los datos de la derecha. Cuando los otros tipos de datos se convierten en **binario** o **varbinary**, los datos se rellenan o se truncan por la izquierda. El relleno se realiza con ceros hexadecimales.
  
Convertir datos en el **binario** y **varbinary** tipos de datos es útil si **binario** datos están la manera más fácil de mover datos. Convertir un valor de cualquier tipo a un valor binario de gran tamaño suficiente y, a continuación, al tipo, siempre produce el mismo valor si ambas conversiones tienen lugar en la misma versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La representación binaria de un valor puede cambiar entre versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Puede convertir **int**, **smallint**, y **tinyint** a **binario** o **varbinary**, pero si se convertir el **binario** valor a un valor entero, este valor será diferente del valor entero original si se ha producido truncamiento. Por ejemplo, la siguiente instrucción SELECT muestra que el valor entero `123456` se almacena normalmente como un valor `0x0001e240` binario:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
Sin embargo, la siguiente `SELECT` instrucción muestra que, si la **binario** destino es demasiado pequeño para contener el valor completo, los dígitos a la izquierda se truncarán sin avisar para que el mismo número se almacene como `0xe240`:
  
```sql
SELECT CAST( 123456 AS BINARY(2) );  
```  
  
El siguiente lote muestra que este truncamiento puede afectar a las operaciones aritméticas sin generar un error:
  
```sql
DECLARE @BinaryVariable2 BINARY(2);  
  
SET @BinaryVariable2 = 123456;  
SET @BinaryVariable2 = @BinaryVariable2 + 1;  
  
SELECT CAST( @BinaryVariable2 AS INT);  
GO  
```  
  
El resultado final es `57921` y no `123457`.
  
> [!NOTE]  
>  Las conversiones entre los datos de cualquier tipo y el **binario** tipos de datos no se garantiza que sea el mismo entre distintas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

