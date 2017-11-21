---
title: ASIN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASIN_TSQL
- ASIN
dev_langs:
- TSQL
helpviewer_keywords:
- ASIN function
- sine
- arcsine
ms.assetid: 6256dd7d-83d5-486e-a933-1d59afc7e417
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1ddfa04e926b4fd0e99455ea91774c31d34b0601
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="asin-transact-sql"></a>ASIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el ángulo, en radianes, cuyo seno es el especificado **float** expresión. También se denomina arco seno.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ASIN ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression*  
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) del tipo **float** o de un tipo que pueda convertirse implícitamente a float, con un valor de -1 a 1. Con valores fuera de este intervalo se devuelve NULL y se notifica un error del dominio.
  
## <a name="return-types"></a>Tipos de valor devuelto
**float**
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente se toma una **float** expresión y devuelve el valor de ASIN del ángulo especificado.
  
```sql
/* The first value will be -1.01. This fails because the value is   
outside the range.*/  
DECLARE @angle float  
SET @angle = -1.01  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is -1.00.  
DECLARE @angle float  
SET @angle = -1.00  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
  
-- The next value is 0.1472738.  
DECLARE @angle float  
SET @angle = 0.1472738  
SELECT 'The ASIN of the angle is: ' + CONVERT(varchar, ASIN(@angle))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-------------------------  
.Net SqlClient Data Provider: Msg 3622, Level 16, State 1, Line 3  
A domain error occurred.  
  
---------------------------------   
The ASIN of the angle is: -1.5708                          
  
(1 row(s) affected)  
  
----------------------------------   
The ASIN of the angle is: 0.147811                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
En el ejemplo siguiente se devuelve el arcoseno de 1,00.
  
```sql
SELECT ASIN(1.00) AS asinCalc;  
```  
  
En el ejemplo siguiente se devuelve un error, porque lo solicita el arcoseno de un valor fuera del intervalo permitido.
  
```sql
SELECT ASIN(1.1472738) AS asinCalc;  
```  
  
## <a name="see-also"></a>Vea también
[CEILING &#40; Transact-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)  
[Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[SET ARITHIGNORE &#40; Transact-SQL &#41;](../../t-sql/statements/set-arithignore-transact-sql.md)  
[SET ARITHABORT &#40; Transact-SQL &#41;](../../t-sql/statements/set-arithabort-transact-sql.md)
  
  


