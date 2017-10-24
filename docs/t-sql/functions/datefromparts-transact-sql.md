---
title: DATEFROMPARTS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEFROMPARTS_TSQL
- DATEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATEFROMPARTS function
ms.assetid: 5b885376-87aa-41f1-9e18-04987aead250
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: a94584788187162e4cd7d433d71653a04c5103e2
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="datefromparts-transact-sql"></a>DATEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Devuelve un **fecha** valor para el año, mes y día.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATEFROMPARTS ( year, month, day )  
```  
  
## <a name="arguments"></a>Argumentos  
*año*  
Expresión entera que especifica un año.
  
*mes*  
Expresión entera que especifica un mes, de 1 a 12.
  
*día*  
Expresión entera que especifica un día.
  
## <a name="return-types"></a>Tipos de valor devuelto
**date**
  
## <a name="remarks"></a>Comentarios  
**DATEFROMPARTS** devuelve un **fecha** valor con la parte de la fecha establecida en el año, mes y día y la parte de hora con el valor predeterminado. Si los argumentos no son válidos, se produce un error. Si los argumentos necesarios son NULL, se devuelve un valor NULL.
  
Esta función se puede enviar de forma remota a servidores de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y superiores. No se puede enviar de forma remota a servidores con una versión inferior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se muestra la **DATEFROMPARTS** (función).
  
```sql
SELECT DATEFROMPARTS ( 2010, 12, 31 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
----------------------------------  
2010-12-31  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)
  
  


