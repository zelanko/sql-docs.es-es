---
title: binary y varbinary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 8/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: eb67f7bbfe21b1e213e5ef166b54f91ae4b3513c
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39454999"
---
# <a name="binary-and-varbinary-transact-sql"></a>binary y varbinary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Tipos de datos binarios de longitud fija o variable.
  
## <a name="arguments"></a>Argumentos  
**binary** [ (*n*) ] Datos binarios de longitud fija con una longitud de *n* bytes, donde *n* es un valor que oscila entre 1 y 8000. El tamaño de almacenamiento es de *n* bytes.
  
**varbinary** [ (*n* | **max**) ] Datos binarios de longitud variable. *n* puede ser un valor de 1 a 8000. **max** indica que el tamaño máximo de almacenamiento es de 2^31-1 bytes. El tamaño de almacenamiento es la longitud real de los datos especificados + 2 bytes. Los datos especificados pueden tener una longitud de 0 bytes. El sinónimo de ANSI SQL para **varbinary** es **binary varying**.
  
## <a name="remarks"></a>Notas  
Cuando no se especifica el argumento *n* en una instrucción de definición de datos o de declaración de variable, la longitud predeterminada es 1. Cuando no se especifica *n* con la función CAST, la longitud predeterminada es 30.

| Tipo de datos | Usar cuando... |
| --- | --- |
| **binario** | los tamaños de las entradas de datos de columna sean coherentes.|
| **varbinary** | los tamaños de las entradas de datos de columna varíen considerablemente.|
| **varbinary(max)** | las entradas de datos de columna superen los 8000 bytes.|


## <a name="converting-binary-and-varbinary-data"></a>Convertir datos binary y varbinary
Cuando se convierten datos de un tipo de datos de cadena (**char**, **varchar**, **nchar**, **nvarchar**, **binary**, **varbinary**, **text**, **ntext** o **image**) a un tipo de datos **binary** o **varbinary** de diferente longitud, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rellena o trunca los datos por la derecha. Cuando se convierten a **binary** o **varbinary** otros tipos de datos, los datos se rellenan o se truncan por la izquierda. El relleno se realiza con ceros hexadecimales.
  
La conversión de datos a tipos de datos **binary** y **varbinary** es útil si el dato **binary** es la forma más sencilla de mover datos. Cuando se convierte un valor de cualquier tipo a un valor binario de tamaño suficiente y, después, se convierte de nuevo al tipo original, el resultado es el mismo valor si ambas conversiones usan la misma versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La representación binaria de un valor puede cambiar entre versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
Puede convertir tipos de datos **int**, **smallint** y **tinyint** en **binary** o **varbinary**, pero si convierte de nuevo el valor **binary** a un valor entero, este será distinto del valor entero original si se ha producido un truncamiento. Por ejemplo, la siguiente instrucción SELECT muestra que el valor entero `123456` se almacena normalmente como un valor `0x0001e240` binario:
  
```sql
SELECT CAST( 123456 AS BINARY(4) );  
```  
  
En cambio, en la siguiente instrucción `SELECT` se muestra que, si el destino de tipo **binary** es demasiado pequeño para contener el valor completo, los dígitos a la izquierda se truncarán sin avisar; de esta forma, el mismo número se almacena como `0xe240`:
  
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
>  No se garantiza que las conversiones entre cualquier tipo de datos y los tipos de datos **binary** sean las mismas entre diferentes versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Conversiones de tipos de datos &#40;motor de base de datos&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
