---
title: PERCENTILE_DISC (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/20/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs: TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: a1e7ebdd2303108fbf63578a288d95eb2f3f7fe4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Calcula un percentil concreto para los valores ordenados de un conjunto de filas completo o dentro de particiones distintas de un conjunto de filas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para un valor de percentil *P*, PERCENTILE_DISC ordena los valores de la expresión en la cláusula ORDER BY y devuelve el valor con el menor valor CUME_DIST (con respecto a la misma especificación de ordenación) que es mayor que o igual que *P*. Por ejemplo, PERCENTILE_DISC (0.5) calculará el cincuentavo percentil (es decir, la mediana) de una expresión. PERCENTILE_DISC calcula el percentil basándose en una distribución discreta de los valores de columna; el resultado es igual a un valor específico de la columna.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *literal*  
 El percentil que se va a calcular. El valor debe estar entre 0,0 y 1,0.  
  
 EN el grupo **(** ORDER BY *order_by_expression* [ **ASC** | DESC]**)**  
 Especifica una lista de valores para ordenar y calcular el percentil con. Solo un *order_by_expression* está permitido. El criterio de ordenación predeterminado es ascendente. La lista de valores puede ser de cualquiera de los tipos de datos que son válidos para la operación de ordenación.  
  
 SOBRE **(** \<partition_by_clause > **)**  
 Divide el conjunto de resultados generado por la cláusula FROM en particiones a las que se aplica la función de percentil. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md). El \<cláusula ORDER BY > y \<filas o cláusula de intervalo > no se puede especificar en una función PERCENTILE_DISC.  
  
## <a name="return-types"></a>Tipos devueltos  
 El tipo de valor devuelto se determina por la *order_by_expression* tipo.  
  
## <a name="compatibility-support"></a>Soporte de compatibilidad  
 En el nivel de compatibilidad 110 y posteriores, WITHIN GROUP es una palabra clave reservada. Para obtener más información, vea [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="general-remarks"></a>Notas generales  
 Se omite cualquier valor NULL del conjunto de datos.  
  
 PERCENTILE_DISC es no determinista. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-basic-syntax-example"></a>A. Ejemplo de sintaxis básica  
 En el ejemplo siguiente se usa PERCENTILE_CONT y PERCENTILE_DISC para buscar el salario medio de los empleados de cada departamento. Tenga en cuenta que estas funciones pueden no devolver el mismo valor. Esto se debe a que PERCENTILE_CONT interpola el valor adecuado, tanto si existe en el conjunto de datos como si no existe, mientras que PERCENTILE_DISC siempre devuelve un valor real del conjunto.  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>B. Ejemplo de sintaxis básica  
 En el ejemplo siguiente se usa PERCENTILE_CONT y PERCENTILE_DISC para buscar el salario medio de los empleados de cada departamento. Tenga en cuenta que estas funciones pueden no devolver el mismo valor. Esto se debe a que PERCENTILE_CONT interpola el valor adecuado, tanto si existe en el conjunto de datos como si no existe, mientras que PERCENTILE_DISC siempre devuelve un valor real del conjunto.  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>Vea también  
 [PERCENTILE_CONT &#40; Transact-SQL &#41;](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


