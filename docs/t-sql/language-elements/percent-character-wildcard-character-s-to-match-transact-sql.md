---
description: Carácter de porcentaje (caracteres comodín para coincidir) (Transact-SQL)
title: Búsqueda con caracteres comodín (%)
ms.custom: seo-lt-2019
ms.date: 12/06/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '%'
- '%_TSQL'
- wildcard
dev_langs:
- TSQL
helpviewer_keywords:
- conditions [SQL Server], wildcards
- '% (wildcard - character(s) to match)'
- matching conditions [SQL Server]
- wildcard characters [SQL Server]
- characters [SQL Server], wildcard
ms.assetid: d4cbc1a9-37e1-4101-97fb-e6ac30c1223e
author: rothja
ms.author: jroth
ms.openlocfilehash: 3b9a47ebd388c5720a8016763d36eac3b913ce14
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92191259"
---
# <a name="percent-character-wildcard---characters-to-match-transact-sql"></a>Carácter de porcentaje (caracteres comodín para coincidir) (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Coincide con cualquier cadena que tenga cero o más caracteres. Este carácter comodín puede utilizarse como prefijo y como sufijo.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve todos los nombres de las personas que aparecen en la tabla `Person` de `AdventureWorks2012` y que empiezan con `Dan`.  
  
```syntaxsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName  
FROM Person.Person  
WHERE FirstName LIKE 'Dan%';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
 [&#91; &#93; (caracteres comodín para coincidencia)](../../t-sql/language-elements/wildcard-character-s-to-match-transact-sql.md)   
  [&#91;^&#93; (caracteres comodín para no coincidencia)](../../t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql.md)     
 [_ (Comodín - Un carácter para coincidir)](../../t-sql/language-elements/wildcard-match-one-character-transact-sql.md)  
    
  
