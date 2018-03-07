---
title: "Operadores de comparación (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], testing
- operators [Transact-SQL], comparison
- testing expressions
- Boolean data type
- Boolean expressions
- comparing expressions
- comparison operators [SQL Server]
ms.assetid: b0cc68ef-3029-484c-a917-0c15dcbc230d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: cd8dcf23064d6caae62d10065c9aa3731823e99b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="comparison-operators-transact-sql"></a>Operadores de comparación (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Los operadores de comparación comprueban si dos expresiones son iguales. Operadores de comparación se pueden utilizar en todas las expresiones excepto de los **texto**, **ntext**, o **imagen** tipos de datos. En la siguiente tabla se presentan los operadores de comparación [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Operador|Significado|  
|--------------|-------------|  
|[= (Es igual a)](../../t-sql/language-elements/equals-transact-sql.md)|Igual a|  
|[> (Mayor que)](../../t-sql/language-elements/greater-than-transact-sql.md)|Mayor que|  
|[< (Menor que)](../../t-sql/language-elements/less-than-transact-sql.md)|Menor que|  
|[>= (Mayor o igual a)](../../t-sql/language-elements/greater-than-or-equal-to-transact-sql.md)|Mayor o igual que|  
|[<= (Menor o igual a)](../../t-sql/language-elements/less-than-or-equal-to-transact-sql.md)|Menor o igual que|  
|[<> (No es igual a)](../../t-sql/language-elements/not-equal-to-transact-sql-traditional.md)|No es igual a|  
|[\!= (No es igual a)](../../t-sql/language-elements/not-equal-to-transact-sql-exclamation.md)|No es igual a (no es del estándar ISO)|  
|[\!< (No menor que)](../../t-sql/language-elements/not-less-than-transact-sql.md)|No es menor que (no es del estándar ISO)|  
|[\!> (No mayor que)](../../t-sql/language-elements/not-greater-than-transact-sql.md)|No es mayor que (no es del estándar ISO)|  
  
## <a name="boolean-data-type"></a>Tipo de datos Boolean  
 El resultado de un operador de comparación tiene la **booleano** tipo de datos. Tiene tres valores: TRUE, FALSE y UNKNOWN. Las expresiones que devuelven un **booleano** tipo de datos se conocen como expresiones booleanas.  
  
 A diferencia de otras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos, un **booleano** tipo de datos no se puede especificar como el tipo de datos de una variable o columna de tabla y no se puede devolver en un conjunto de resultados.  
  
 Cuando SET ANSI_NULLS es ON, un operador con una o dos expresiones NULL devuelve UNKNOWN. Cuando SET ANSI_NULLS es OFF, se aplica la misma regla, excepto que el operador de igualdad (=) devuelve TRUE si ambas expresiones son NULL. Por ejemplo, NULL = NULL devuelve TRUE si SET ANSI_NULLS es OFF.  
  
 Expresiones con **booleano** tipos de datos se utilizan en la cláusula WHERE para filtrar las filas que se incluyen para las condiciones de búsqueda y en las instrucciones de lenguaje de control de flujo tales como IF y WHILE, por ejemplo:  
  
```  
-- Uses AdventureWorks  
  
DECLARE @MyProduct int;  
SET @MyProduct = 750;  
IF (@MyProduct <> 0)  
   SELECT ProductID, Name, ProductNumber  
   FROM Production.Product  
   WHERE ProductID = @MyProduct;  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
