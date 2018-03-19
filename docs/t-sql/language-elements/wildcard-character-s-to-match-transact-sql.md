---
title: "[ ] (caracteres comodín para coincidencia) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Match
- wildcard
- '[ ]'
- '[_]_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- wildcard characters [SQL Server]
- '[ ] (wildcard - character(s) to match)'
ms.assetid: 57817576-0bf1-49ed-b05d-fac27e8fed7a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 04fcf0d9e76db380430bfbf4c4ed6e5fadf14afb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="--wildcard---characters-to-match-transact-sql"></a>\[ \] (caracteres comodín para coincidencia) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Halla coincidencias con cada uno de los caracteres del intervalo o conjunto especificado entre corchetes `[ ]`. Estos caracteres comodín se pueden usar en comparaciones de cadenas donde se buscan coincidencias de patrón, como sucede con `LIKE` y `PATINDEX`.  
  
## <a name="examples"></a>Ejemplos  
### <a name="a-simple-example"></a>A: Ejemplo sencillo   
En el siguiente ejemplo se devuelven los nombres que comienzan por la letra `m`. `[n-z]` especifica que la segunda letra debe estar en alguna parte del intervalo entre `n` y `z`. El carácter comodín de porcentaje `%` permite cualquier carácter que comience por el tercer carácter. Las bases de datos `model` y `msdb` cumplen este criterio, pero no la base de datos `master`, de modo que se excluye del conjunto de resultados.
 
```sql
SELECT name FROM sys.databases
WHERE name LIKE 'm[n-z]%';
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]  

```
name
-----
model
msdb
```   
 Es posible que tenga instaladas más bases de datos aplicables.


### <a name="b-more-complex-example"></a>B: Ejemplo más complejo   
 En el ejemplo siguiente se utiliza el operador [] para buscar los identificadores y nombres de todos los empleados de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] cuyas direcciones tienen un código postal de cuatro dígitos.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT e.BusinessEntityID, p.FirstName, p.LastName, a.PostalCode  
FROM HumanResources.Employee AS e  
INNER JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
INNER JOIN Person.Address AS a ON a.AddressID = ea.AddressID  
WHERE a.PostalCode LIKE '[0-9][0-9][0-9][0-9]';  
```  
  
 El conjunto de resultados es:  
  
```  
EmployeeID      FirstName      LastName      PostalCode  
----------      ---------      ---------     ----------  
290             Lynn           Tsoflias      3000  
```  



  
## <a name="see-also"></a>Ver también  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% &#40;caracteres comodín para coincidencia&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91;^&#93; &#40;caracteres comodín para no coincidencia&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [\_ &#40;comodín, coincidir un carácter&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
