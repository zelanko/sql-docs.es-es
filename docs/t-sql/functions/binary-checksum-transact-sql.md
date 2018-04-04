---
title: BINARY_CHECKSUM  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BINARY_CHECKSUM
- BINARY_CHECKSUM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- BINARY_CHECKSUM function
- binary [SQL Server], checksum values
ms.assetid: 07fece4d-58e3-446e-a3b5-92fe24d2d1fb
caps.latest.revision: 21
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9ff8368877b3fb2153685554f1484b5fbbcc7c3a
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2018
---
# <a name="binarychecksum--transact-sql"></a>BINARY_CHECKSUM  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Devuelve el valor binario de suma de comprobación calculado en una fila de una tabla o en una lista de expresiones.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
BINARY_CHECKSUM ( * | expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*\**  
Especifica que el cálculo se realiza en todas las columnas de la tabla. BINARY_CHECKSUM no incluye en el cálculo las columnas que tienen tipos de datos no comparables. Entre los tipos de datos no comparables se incluyen **text**, **ntext**, **image**, **cursor**, **xml** y los tipos definidos por el usuario no comparables de Common Language Runtime (CLR).
  
*expression*  
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo. BINARY_CHECKSUM no incluye en el cálculo las expresiones que tienen tipos de datos no comparables.

## <a name="return-types"></a>Tipos devueltos  
 **int**
  
## <a name="remarks"></a>Notas  
BINARY_CHECKSUM(*), calculado en cualquier fila de una tabla, devuelve el mismo valor siempre que la fila no se modifique posteriormente. BINARY_CHECKSUM cumple las propiedades de una función hash: si se aplica BINARY_CHECKSUM sobre dos listas de expresiones, devuelve el mismo valor si los elementos correspondientes de las dos listas tienen el mismo tipo y son iguales cuando se comparan utilizando el operador igual (=). En esta definición, la comparación de valores NULL de un tipo específico se consideran como iguales. Si uno de los valores de la lista de expresiones cambia, la suma de comprobación de la lista generalmente también cambia. No obstante, existe una pequeña posibilidad de que la suma de comprobación no cambie. Por este motivo, no se recomienda usar BINARY_CHECKSUM para detectar si han cambiado los valores, a menos que la aplicación pueda tolerar perder un cambio ocasionalmente. Es más aconsejable usar HashBytes. Cuando se especifica un algoritmo hash MD5, la probabilidad de que HashBytes devuelva el mismo resultado de dos entradas diferentes es mucho menor que la de que lo haga BINARY_CHECKSUM.
  
BINARY_CHECKSUM se puede aplicar a una lista de expresiones y devuelve el mismo valor para una lista especificada. BINARY_CHECKSUM aplicado a dos listas de expresiones cualquiera devuelve el mismo valor si los elementos correspondientes de ambas listas tienen el mismo tipo y la misma representación de bytes. Para esta definición, los valores NULL de un tipo especificado se considera que tienen la misma representación de bytes.
  
BINARY_CHECKSUM y CHECKSUM son funciones similares: se pueden utilizar para calcular un valor de suma de comprobación en una lista de expresiones; el orden de las expresiones afecta al valor del resultado. El orden de las columnas utilizadas en BINARY_CHECKSUM(*) es el orden de las columnas especificado en la definición de la tabla o la vista. Incluyen columnas calculadas.
  
CHECKSUM y BINARY_CHECKSUM devuelven valores distintos para los tipos de datos de cadena, donde la configuración regional puede hacer que cadenas con una presentación distinta se comparen como iguales. Los tipos de datos de cadena son **char**, **varchar**, **nchar**, **nvarchar** o **sql_variant** (si el tipo de base de **sql_variant** es un tipo de cadena de datos). Por ejemplo, los valores de BINARY_CHECKSUM para las cadenas "McCavity" y "Mccavity" son distintos. Por el contrario, en un servidor que no distingue entre mayúsculas y minúsculas, CHECKSUM devuelve los mismos valores de suma de comprobación para ambas cadenas. Los valores de CHECKSUM no se deben comparar con los valores de BINARY_CHECKSUM.
 
BINARY_CHECKSUM admite hasta 8000 caracteres de tipo **varbinary(max)** y un máximo de 255 caracteres de tipo **nvarchar(max)**.
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se utiliza `BINARY_CHECKSUM` para detectar cambios en una fila de una tabla.
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE myTable (column1 int, column2 varchar(256));  
GO  
INSERT INTO myTable VALUES (1, 'test');  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
UPDATE myTable set column2 = 'TEST';  
GO  
SELECT BINARY_CHECKSUM(*) from myTable;  
GO  
```  
  
## <a name="see-also"></a>Vea también
[Funciones de agregado &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)
  
  
