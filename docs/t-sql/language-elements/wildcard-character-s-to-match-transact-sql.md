---
title: "(Comodín - caracteres para coincidir) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 12/06/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18688c96cd0369905844d79a1a109f4e5032bce3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="wildcard---characters-to-match-transact-sql"></a>(Comodín - caracteres para coincidir) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Coincide con cualquier carácter individual dentro del intervalo especificado o el conjunto que se especifica entre corchetes `[ ]`. Estos caracteres de comodín se pueden utilizar en las comparaciones de cadenas que se buscan coincidencias de patrón, como `LIKE` y `PATINDEX`.  
  
## <a name="examples"></a>Ejemplos  
### <a name="a-simple-example"></a>R: ejemplo sencillo de   
En el ejemplo siguiente devuelve los nombres de los que empiezan por la letra `m`. `[n-z]`Especifica que la segunda letra debe estar en el intervalo de `n` a `z`. El comodín de porcentaje `%` permite caracteres de cualquier o no comienzan con el carácter de 3. El `model` y `msdb` las bases de datos cumplan este criterio. El `master` base de datos no funciona y se excluye del conjunto de resultados.
 
```tsql
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
 Puede tener bases de datos adicionales aplicables instalados.


### <a name="b-more-complex-example"></a>B: ejemplo más complejo   
 En el ejemplo siguiente se utiliza el operador [] para buscar los identificadores y nombres de todos los empleados de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] cuyas direcciones tienen un código postal de cuatro dígitos.  
  
```tsql  
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



  
## <a name="see-also"></a>Vea también  
 [COMO &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)   
  [% (Caracteres comodín para coincidir)](../../t-sql/language-elements/percent-character-wildcard-character-s-to-match-transact-sql.md)   
 [&#91; ^ &#93; (Comodín - caracteres no coincidentes)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (Comodín - coincidir un carácter)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  

