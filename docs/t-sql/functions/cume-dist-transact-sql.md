---
title: CUME_DIST (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CUME_DIST
- CUME_DIST_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CUME_DIST function
- analytic functions, CUME_DIST
ms.assetid: 491b07f3-9ffd-4cdd-93e5-5abb636fc5ef
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6cf5d594312b73cba8db2d949ce54afce75ac29c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075269"
---
# <a name="cumedist-transact-sql"></a>CUME_DIST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta función calcula la distribución acumulativa de un valor en un grupo de valores. Es decir, `CUME_DIST` calcula la posición relativa de un valor especificado en un grupo de valores. Suponiendo un orden ascendente, el `CUME_DIST` de un valor en la fila *r* se define como el número de filas con valores menores o iguales que el valor de la fila *r*, dividido entre el número de filas evaluadas en la partición o el conjunto de resultados de la consulta. `CUME_DIST` es similar a la función `PERCENT_RANK`.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CUME_DIST( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
  
```  
  
## <a name="arguments"></a>Argumentos  
OVER **(** [ *partition_by_clause* ] *order_by_clause*)  

El argumento *partition_by_clause* divide el conjunto de resultados de la cláusula FROM en particiones, a las que se aplica la función. Si no se especifica el argumento *partition_by_clause*, `CUME_DIST` trata todas las filas del conjunto de resultados de la consulta como un único grupo. *order_by_clause* determina el orden lógico en el que tiene lugar la operación. `CUME_DIST` requiere *order_by_clause*. `CUME_DIST` no aceptará las \<filas o cláusula de rango> de la sintaxis OVER. Para más información, consulte [Cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valores devueltos
**float(53)**
  
## <a name="remarks"></a>Notas  
`CUME_DIST` devuelve un intervalo de valores mayor que 0 y menor o igual que 1. Los valores equivalentes siempre se evalúan como el mismo valor de distribución acumulativa. `CUME_DIST` incluye valores NULL de forma predeterminada y los trata como los posibles valores más bajos.
  
`CUME_DIST` sea no determinista. Para más información, consulte [Funciones deterministas y no deterministas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se usa la función `CUME_DIST` para calcular el percentil de salario de cada empleado dentro de un departamento determinado. `CUME_DIST` devuelve un valor que representa el porcentaje de empleados que tienen un salario menor o igual que el empleado actual del mismo departamento. La función `PERCENT_RANK` calcula el intervalo de porcentaje de salario del empleado dentro de un departamento. Para crear particiones de las filas del conjunto de resultados por departamento, el ejemplo especifica el valor de *partition_by_clause*. La cláusula ORDER BY de la cláusula OVER ordena lógicamente las filas de cada partición. La cláusula ORDER BY de la instrucción SELECT determina el orden de presentación del conjunto de resultados.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[PERCENT_RANK &#40;Transact-SQL&#41;](../../t-sql/functions/percent-rank-transact-sql.md)
  
  
