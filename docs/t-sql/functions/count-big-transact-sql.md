---
title: COUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 44
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 550dc639c3b949926c1bd95b7c89e04823b68f68
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781258"
---
# <a name="countbig--sql"></a>COUNT_BIG (-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Esta función devuelve el número de elementos encontrados en un grupo. `COUNT_BIG` funciona como la función [COUNT](../../t-sql/functions/count-transact-sql.md). Estas funciones difieren solo en los tipos de datos de sus valores devueltos. `COUNT_BIG` siempre devuelve un valor de tipo de datos **bigint**. `COUNT` siempre devuelve un valor de tipo de datos **int**.
  
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
Aplica la función de agregado a todos los valores. ALL sirve como valor predeterminado.
  
DISTINCT  
Especifica que `COUNT_BIG` devuelva el número de valores únicos no NULL.
  
*expression*  
Una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo. Tenga en cuenta que `COUNT_BIG` no admite funciones de agregado ni subconsultas en una expresión.
  
*\**  
Especifica que `COUNT_BIG` debe contar todas las filas para determinar el total de filas de la tabla a devolver. `COUNT_BIG(*)` no toma ningún parámetro y no admite el uso de DISTINCT. `COUNT_BIG(*)` no requiere el parámetro *expression* porque, por definición, no usa información sobre ninguna columna concreta. `COUNT_BIG(*)` devuelve el número de filas de una tabla especificada y conserva las filas duplicadas. Cuenta cada fila por separado. Esto incluye las filas que contienen valores NULL.
  
OVER **(** [ *partition_by_clause* ] [ *order_by_clause* ] **)**  
*partition_by_clause* divide el conjunto de resultados generado por la cláusula `FROM` en particiones a las que se aplica la función `COUNT_BIG`. Si no se especifica, la función trata todas las filas del conjunto de resultados de la consulta como un único grupo. *order_by_clause* determina el orden lógico de la operación. Para más información, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valores devueltos
**bigint**
  
## <a name="remarks"></a>Notas  
COUNT_BIG(\*) devuelve el número de elementos de un grupo. Esto incluye los valores NULL y los duplicados
  
COUNT_BIG (ALL *expresión*) evalúa *expresión* en todas las filas del grupo y devuelve el número de valores no NULL.
  
COUNT_BIG (DISTINCT *expresión*) evalúa *expresión* en todas las filas del grupo y devuelve el número de valores únicos no NULL.
  
COUNT_BIG es una función determinista cuando se utiliza ***sin*** las cláusulas OVER y ORDER BY. Es no determinista si se especifica ***con*** las cláusulas OVER y ORDER BY. Para más información, consulte [Funciones deterministas y no deterministas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Ejemplos  
Para ver algunos ejemplos, consulte [COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[Funciones de agregado &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[COUNT &#40;Transact-SQL&#41;](../../t-sql/functions/count-transact-sql.md)  
[int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
[Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
