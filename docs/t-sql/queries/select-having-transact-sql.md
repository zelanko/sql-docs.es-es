---
title: HAVING (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/28/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HAVING
- HAVING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restricting conditions for result set
- search conditions [SQL Server], HAVING clause
- HAVING clause
- HAVING clause, about HAVING clause
ms.assetid: 55650709-001e-42f4-902f-ead09a3c34af
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5ec700e859eda5b1a6313183a7485686ce3727ce
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="select---having-transact-sql"></a>SELECT - HAVING (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Especifica una condición de búsqueda para un grupo o agregado. HAVING solo se puede utilizar con la instrucción SELECT. HAVING se utiliza normalmente con una cláusula GROUP BY. Cuando no se usa GROUP BY, hay un grupo único y agregado implícito.   
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
[ HAVING <search condition> ]  
```  
  
## <a name="arguments"></a>Argumentos  
\<search_condition > especifica uno o más predicados para grupos o agregados satisfacer. Para obtener más información sobre predicados y las condiciones de búsqueda, vea [condición de búsqueda &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 El **texto**, **imagen**, y **ntext** tipos de datos no se puede usar en una cláusula HAVING.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, donde se utiliza una cláusula `HAVING` simple, se recupera el total de cada `SalesOrderID` de la tabla `SalesOrderDetail` que exceda `$100000.00`.  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail  
GROUP BY SalesOrderID  
HAVING SUM(LineTotal) > 100000.00  
ORDER BY SalesOrderID ;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se usa un `HAVING` cláusula para recuperar el total de cada `SalesAmount` desde el `FactInternetSales` tabla cuando la `OrderDateKey` está en el año 2004 o una versión posterior.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING SUM(SalesAmount) > 80000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Vea también  
 [GROUP BY &#40;Transact-SQL&#41;](../../t-sql/queries/select-group-by-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

