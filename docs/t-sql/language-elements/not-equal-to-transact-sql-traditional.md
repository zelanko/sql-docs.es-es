---
title: '&lt;&gt;(No es igual a) (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 03/13/2017
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
- <>
- <>_TSQL
- Not Equal To
- Not Equal
- <>(Not Equal To)
- NOT
- Equal
dev_langs:
- TSQL
helpviewer_keywords:
- not equal to operator (<>)
- <> (not equal to operator)
ms.assetid: 34cf9b38-d589-4be9-925a-116e224609a0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: ffacad3e57cd9c9ab1331e0dbe52335ae1d6ddf1
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="not-equal-to-transact-sql---traditional"></a>No es igual a (Transact SQL) - tradicional
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Compara dos expresiones (es un operador de comparación). Cuando se comparan expresiones que no son NULL, el resultado es TRUE si el operando de la izquierda es distinto del operando de la derecha; de lo contrario, el resultado es FALSE. Si uno o ambos operandos son NULL, vea el tema [SET ANSI_NULLS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression <> expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md). Ambas expresiones deben tener tipos de datos que se puedan convertir implícitamente. La conversión depende de las reglas de [prioridad de tipo de datos](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using--in-a-simple-query"></a>A. Uso de <> en una consulta simple  
 En el ejemplo siguiente se devuelven todas las filas de la tabla `Production.ProductCategory` que no tienen un valor en `ProductCategoryID` que es igual que el valor 3 o el valor 2.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductCategoryID, Name  
FROM Production.ProductCategory  
WHERE ProductCategoryID <> 3 AND ProductCategoryID <> 2;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Name  
----------------- --------------------------------------------------  
1                 Bikes  
4                 Accessories  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Comparison Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)  
  
  
