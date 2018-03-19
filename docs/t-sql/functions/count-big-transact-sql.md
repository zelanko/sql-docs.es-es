---
title: COUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COUNT_BIG_TSQL
- COUNT_BIG
dev_langs:
- TSQL
helpviewer_keywords:
- totals [SQL Server], COUNT_BIG function
- counting items in group
- groups [SQL Server], number of items in
- number of group items
- COUNT_BIG function
ms.assetid: f2e3601f-487e-4917-bb01-47b1047908cd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ad2b7e5343547bb65c6d81de8c6586ef5209e52a
ms.sourcegitcommit: 0e305dce04dcd1aa83c39328397524b352c96386
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/22/2017
---
# <a name="countbig--sql"></a>COUNT_BIG (-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el número de elementos de un grupo. COUNT_BIG funciona como COUNT. La única diferencia entre ambas funciones está en los valores devueltos. COUNT_BIG siempre devuelve un valor de tipo de datos **bigint**. COUNT siempre devuelve un valor de tipo de datos **int**.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Syntax for SQL Server and Azure SQL Database  
  
COUNT_BIG ( { [ ALL | DISTINCT ] expression } | * )  
   [ OVER ( [ partition_by_clause ] [ order_by_clause ] ) ]  
```  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Aggregation Function Syntax  
COUNT_BIG ( { [ [ ALL | DISTINCT ] expression ] | * } )  
  
-- Analytic Function Syntax  
COUNT_BIG ( { expression | * } ) OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
ALL  
Aplica la función de agregado a todos los valores. ALL es el valor predeterminado.
  
DISTINCT  
Especifica que COUNT_BIG devuelva el número de valores únicos no NULL.
  
*expression*  
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo. No se permiten funciones de agregado ni subconsultas.
  
*\**  
Especifica que se deben contar todas las filas para devolver el número total de filas de una tabla. COUNT_BIG(*\**) no usa parámetros y no se puede usar con DISTINCT. COUNT_BIG(*\**) no requiere el parámetro *expression* porque, por definición, no usa información sobre ninguna columna concreta. COUNT_BIG(*\**) devuelve el número de filas de una tabla especificada sin eliminar las duplicadas. Cuenta cada fila por separado. Esto incluye las filas que contienen valores NULL.
  
ALL  
Aplica la función de agregado a todos los valores. ALL es el valor predeterminado.
  
DISTINCT  
Especifica que AVG se ejecute solo en cada instancia única de un valor, sin importar el número de veces que aparezca el valor.
  
*expression*  
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos **bit**. No se permiten funciones de agregado ni subconsultas.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* divide el conjunto de resultados generado por la cláusula FROM en particiones a las que se aplica la función. Si no se especifica, la función trata todas las filas del conjunto de resultados de la consulta como un único grupo. *order_by_clause* determina el orden lógico en el que se realiza la operación. Para más información, vea [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valores devueltos
**bigint**
  
## <a name="remarks"></a>Notas  
COUNT_BIG(*) devuelve el número de elementos de un grupo. Esto incluye los valores NULL y los duplicados
  
COUNT_BIG (ALL *expression*) evalúa *expression* en todas las filas del grupo y devuelve el número de valores no NULL.
  
COUNT_BIG (DISTINCT *expression*) evalúa *expression* en todas las filas del grupo y devuelve el número de valores únicos no NULL.
  
COUNT_BIG es una función determinista cuando no se utiliza con las cláusulas OVER y ORDER BY. Es no determinista si se especifica con las cláusulas OVER y ORDER BY. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Ejemplos  
Para obtener ejemplos, vea [COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[Funciones de agregado &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
