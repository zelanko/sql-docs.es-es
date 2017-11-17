---
title: Alias (almacenamiento de datos SQL Azure, almacenamiento de datos paralelos) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: edc81ce4377f490b482d920871ad361c98f961c5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>Alias (almacenamiento de datos SQL Azure, almacenamiento de datos en paralelo)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  El aliasing permite la sustitución temporal de una cadena breve y fácil de recordar en lugar de un nombre de tabla o columna en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [!INCLUDE[DWsql](../../includes/dwsql-md.md)] consultas. Alias de tabla se utilizan a menudo en consultas de combinación porque la sintaxis de unión requiere nombres de objeto completo al hacer referencia a columnas.  
  
 Los alias deben ser las palabras individuales que se ajuste a las reglas de nomenclatura de objetos. Para obtener más información, vea "Reglas de nomenclatura de objetos" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Alias no pueden contener espacios en blanco y no se pueden ir entre comillas simples o dobles.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>Argumentos  
 *object_source*  
 El nombre de la tabla de origen o la columna.  
  
 AS  
 Una preposición alias opcional. Cuando se trabaja con alias de variable de rango, se prohíbe la palabra clave AS.  
  
 *alias*  
 El nombre de referencia temporal deseado para la tabla o columna. Puede utilizarse cualquier nombre de objeto válido. Para obtener más información, vea "Reglas de nomenclatura de objetos" en el [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se muestra una consulta con varias combinaciones. Alias de tabla y columna se muestran en este ejemplo.  
  
-   Alias de columna: Ambas columnas y expresiones que implican las columnas en la lista de selección se tiene un alias en este ejemplo. `SalesTerritoryRegion AS SalesTR`muestra un alias de columna simple. `Sum(SalesAmountQuota) AS TotalSales`muestra  
  
-   Alias de tabla: `dbo.DimSalesTerritory AS st` muestra la creación de la `st` alias para el `dbo.DimSalesTerritory` tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 La palabra clave AS puede excluirse, tal y como se muestra a continuación, pero a menudo se incluye para mejorar la legibilidad.  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

