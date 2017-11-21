---
title: Funciones de agregado (Transact-SQL) | Documentos de Microsoft
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
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], aggregate
- aggregate functions [SQL Server], about aggregate functions
- summarizing functions
- aggregate functions [SQL Server]
ms.assetid: 0c06ae42-eb0a-4d77-9d74-aa1e7f344009
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a97d68c641d2a3deb1d3fd3a674f65cafc3854c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="aggregate-functions-transact-sql"></a>Funciones de agregado (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Las funciones de agregado realizan un cálculo sobre un conjunto de valores y devuelven un solo valor. Si exceptuamos la función COUNT, todas las funciones de agregado ignoran los valores NULL. Las funciones de agregado se suelen utilizar con la cláusula GROUP BY de la instrucción SELECT.
  
Todas las funciones de agregado son deterministas. Esto significa que las funciones de agregado devuelven el mismo valor cada vez que se las llama con un conjunto específico de valores de entrada. Para obtener más información acerca del determinismo de función, vea [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). El [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md) puede seguir todas las funciones agregadas excepto GROUPING y GROUPING_ID.
  
Las funciones de agregado solo se pueden utilizar como expresiones en:
-   La lista de selección de una instrucción SELECT (una subconsulta o una consulta externa).  
-   Cláusula HAVING.  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] proporciona las siguientes funciones de agregado:
  
|||  
|-|-|  
|[AVG](../../t-sql/functions/avg-transact-sql.md)|[MIN](../../t-sql/functions/min-transact-sql.md)|  
|[CHECKSUM_AGG](../../t-sql/functions/checksum-agg-transact-sql.md)|[SUMA](../../t-sql/functions/sum-transact-sql.md)|  
|[RECUENTO](../../t-sql/functions/count-transact-sql.md)|[STDEV](../../t-sql/functions/stdev-transact-sql.md)|  
|[COUNT_BIG](../../t-sql/functions/count-big-transact-sql.md)|[STDEVP](../../t-sql/functions/stdevp-transact-sql.md)|  
|[AGRUPACIÓN](../../t-sql/functions/grouping-transact-sql.md)|[VAR](../../t-sql/functions/var-transact-sql.md)|  
|[GROUPING_ID](../../t-sql/functions/grouping-id-transact-sql.md)|[VARP](../../t-sql/functions/varp-transact-sql.md)|  
|[MAX](../../t-sql/functions/max-transact-sql.md)||  
  
## <a name="see-also"></a>Vea también
[Funciones integradas &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[EN cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

