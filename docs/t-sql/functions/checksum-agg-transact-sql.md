---
title: CHECKSUM_AGG (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b202009c2920dfbcdd068ec3d7ab95de13caa7b4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve la suma de comprobación de los valores de un grupo. Se omiten los valores NULL. Puede ir seguida de la [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>Argumentos  
**ALL**  
Aplica la función de agregado a todos los valores. ALL es el valor predeterminado.
  
DISTINCT  
Especifica que CHECKSUM_AGG devuelve la suma de comprobación de valores únicos.
  
*expression*  
Es un número entero [expresión](../../t-sql/language-elements/expressions-transact-sql.md). No se permiten funciones de agregado ni subconsultas.
  
## <a name="return-types"></a>Tipos de valor devuelto
Devuelve la suma de comprobación de todos los *expresión* valores como **int**.
  
## <a name="remarks"></a>Comentarios  
CHECKSUM_AGG se puede utilizar para detectar cambios en una tabla.
  
El orden de las filas en la tabla no afecta al resultado de CHECKSUM_AGG. Además, las funciones CHECKSUM_AGG se pueden utilizar con la palabra clave DISTINCT y la cláusula GROUP BY.
  
Si uno de los valores de la lista de expresiones cambia, la suma de comprobación de la lista generalmente también cambia. No obstante, existe una pequeña posibilidad de que la suma de comprobación no cambie.
  
CHECKSUM_AGG tiene una función similar a otras funciones de agregado. Para obtener más información, vea [funciones de agregado &#40; Transact-SQL &#41; ](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente utiliza `CHECKSUM_AGG` para detectar cambios en la columna `Quantity` de la tabla `ProductInventory` en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>Vea también
[Suma de comprobación &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[EN cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

