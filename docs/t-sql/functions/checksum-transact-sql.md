---
title: CHECKSUM (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_TSQL
- CHECKSUM
dev_langs:
- TSQL
helpviewer_keywords:
- hash indexes
- CHECKSUM function
- checksum values
ms.assetid: e26d3339-845c-49c2-9d89-243376874c13
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: d41736f6ac216de0ecf755cbf7ca73ba34a697b8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="checksum-transact-sql"></a>CHECKSUM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

Devuelve el valor de suma de comprobación calculado sobre una fila de una tabla o sobre una lista de expresiones. CHECKSUM se ha pensado para utilizarlo en la generación de índices hash.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CHECKSUM ( * | expression [ ,...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
\*  
Especifica que el cálculo se realiza sobre todas las columnas de la tabla. CHECKSUM devuelve un error si alguna columna tiene un tipo de datos no comparable. Los tipos de datos no comparables son **text**, **ntext**, **image**, XML y **cursor**, así como **sql_variant** con uno de los tipos anteriores como tipo base.
  
*expression*  
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo, excepto un tipo de datos no comparable.
  
## <a name="return-types"></a>Tipos de valores devueltos
 **int**  
  
## <a name="remarks"></a>Notas  
CHECKSUM calcula un valor hash, denominado suma de comprobación, sobre su lista de argumentos. El valor hash se ha pensado para utilizarlo en la generación de índices hash. Si los argumentos de CHECKSUM son columnas y se genera un índice sobre el valor CHECKSUM calculado, el resultado es un índice hash. Éste se puede utilizar para búsquedas de igualdades sobre las columnas.
  
CHECKSUM cumple las propiedades de una función hash: si se aplica CHECKSUM sobre dos listas de expresiones, devuelve el mismo valor si los elementos correspondientes de las dos listas tienen el mismo tipo y son iguales cuando se comparan utilizando el operador igual (=). En esta definición, la comparación de valores NULL de un tipo específico se consideran como iguales. Si uno de los valores de la lista de expresiones cambia, la suma de comprobación de la lista generalmente también cambia. No obstante, existe una pequeña posibilidad de que la suma de comprobación no cambie. Por este motivo, no se recomienda usar CHECKSUM para detectar si han cambiado los valores, a menos que la aplicación pueda tolerar perder un cambio ocasionalmente. Considere la posibilidad de usar [HashBytes](../../t-sql/functions/hashbytes-transact-sql.md) en su lugar. Cuando se especifica un algoritmo hash MD5, la probabilidad de que HashBytes devuelva el mismo resultado de dos entradas diferentes es mucho menor que la de que lo haga CHECKSUM.
  
El orden de las expresiones afecta el valor del resultado de CHECKSUM. El orden de las columnas usado con CHECKSUM(*) es el orden de las columnas especificado en la definición de la tabla o la vista. Esto incluye las columnas calculadas.
  
El valor de CHECKSUM depende de la intercalación. El mismo valor almacenado con una intercalación diferente devolverá un valor de CHECKSUM diferente.
  
## <a name="examples"></a>Ejemplos  
En los ejemplos siguientes se muestra cómo usar `CHECKSUM` para generar índices hash. El índice hash se genera al agregar una columna de suma de comprobación calculada a la tabla que se va a indizar y después generar un índice en la columna de suma de comprobación.
  
```sql
-- Create a checksum index.  
SET ARITHABORT ON;  
USE AdventureWorks2012;   
GO  
ALTER TABLE Production.Product  
ADD cs_Pname AS CHECKSUM(Name);  
GO  
CREATE INDEX Pname_index ON Production.Product (cs_Pname);  
GO  
```  
  
El índice de la suma de comprobación se puede utilizar como un índice hash, especialmente para mejorar la velocidad de indización cuando la columna que se va a indizar es una columna de cadenas largas de caracteres. El índice de suma de comprobación se puede utilizar para búsquedas de igualdades.
  
```sql
/*Use the index in a SELECT query. Add a second search   
condition to catch stray cases where checksums match,   
but the values are not the same.*/  
SELECT *   
FROM Production.Product  
WHERE CHECKSUM(N'Bearing Ball') = cs_Pname  
AND Name = N'Bearing Ball';  
GO  
```  
  
La creación del índice en la columna calculada se materializa en la columna de suma de comprobación y cualquier cambio en el valor de `ProductName` se propagará a la columna de suma de comprobación. Alternativamente, se podría generar un índice directamente en la columna indizada. No obstante, si los valores clave son largos, es posible que un índice normal tenga un rendimiento peor que un índice de suma de comprobación.
  
## <a name="see-also"></a>Vea también
[CHECKSUM_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-agg-transact-sql.md)  
[HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
  
  
