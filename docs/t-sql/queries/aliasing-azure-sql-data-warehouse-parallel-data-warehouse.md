---
title: Creación de alias (Azure SQL Data Warehouse, Almacenamiento de datos paralelos) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4762900ff07c7849e7f058915573ca33bc4c1093
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045893"
---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>Creación de alias (Azure SQL Data Warehouse, Almacenamiento de datos paralelos)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  La creación de alias permite la sustitución temporal de una cadena breve y fácil de recordar en lugar de un nombre de tabla o columna en consultas de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)]. Los alias de tabla se usan a menudo en consultas JOIN porque la sintaxis de JOIN requiere nombres de objeto completos al hacer referencia a columnas.  
  
 Los alias deben ser palabras individuales que se ajusten a las reglas de nomenclatura de objetos. Para obtener más información, vea "Reglas de nomenclatura de objetos" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]. Los alias no pueden contener espacios en blanco y no se pueden incluir entre comillas simples o dobles.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>Argumentos  
 *origen_del_objeto*  
 El nombre de la tabla o columna de origen.  
  
 AS  
 Una preposición alias opcional. Cuando se trabaja con alias de variable de rango, se prohíbe la palabra clave AS.  
  
 *alias*  
 El nombre de referencia temporal deseado para la tabla o columna. Se puede usar cualquier nombre de objeto válido. Para obtener más información, vea "Reglas de nomenclatura de objetos" en la [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se muestra una consulta con varias combinaciones. En este ejemplo se describen tanto los alias de tabla como los de columna.  
  
-   Alias de columna: en este ejemplo, se crean alias de las columnas y las expresiones que implican columnas en la lista de selección. `SalesTerritoryRegion AS SalesTR` muestra un alias de columna simple. `Sum(SalesAmountQuota) AS TotalSales` muestra  
  
-   la creación de alias de tabla: `dbo.DimSalesTerritory AS st` muestra la creación del alias `st` para la tabla `dbo.DimSalesTerritory`.  
  
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
  
 La palabra clave AS se puede excluir, tal y como se muestra a continuación, pero a menudo se incluye para mejorar la legibilidad.  
  
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
  
## <a name="see-also"></a>Ver también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  
