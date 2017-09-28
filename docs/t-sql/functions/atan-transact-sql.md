---
title: ATAN (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ATAN_TSQL
- ATAN
dev_langs:
- TSQL
helpviewer_keywords:
- arctangent
- ATAN function
- tangent
ms.assetid: 6d3dd28e-4fa6-40ba-94cf-b33c0ff614ec
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2c0604d007934327541814aedbc860671905e513
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="atan-transact-sql"></a>ATAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el ángulo en radianes cuya tangente es un determinado **float** expresión. También se denomina arcotangente.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ATAN ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression*  
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) del tipo **float** o de un tipo que pueda convertirse implícitamente a **float**.
  
## <a name="return-types"></a>Tipos de valor devuelto
**float**
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente se toma una **float** expresión y devuelve el valor de ATAN del ángulo especificado.
  
```sql
SELECT 'The ATAN of -45.01 is: ' + CONVERT(varchar, ATAN(-45.01))  
SELECT 'The ATAN of -181.01 is: ' + CONVERT(varchar, ATAN(-181.01))  
SELECT 'The ATAN of 0 is: ' + CONVERT(varchar, ATAN(0))  
SELECT 'The ATAN of 0.1472738 is: ' + CONVERT(varchar, ATAN(0.1472738))  
SELECT 'The ATAN of 197.1099392 is: ' + CONVERT(varchar, ATAN(197.1099392))  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
  
-------------------------------   
The ATAN of -45.01 is: -1.54858                         
  
(1 row(s) affected)  
  
--------------------------------   
The ATAN of -181.01 is: -1.56527                         
  
(1 row(s) affected)  
  
--------------------------------   
The ATAN of 0 is: 0                                
  
(1 row(s) affected)  
  
----------------------------------   
The ATAN of 0.1472738 is: 0.146223                         
  
(1 row(s) affected)  
  
-----------------------------------   
The ATAN of 197.1099392 is: 1.56572                          
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
El ejemplo siguiente se toma una **float** expresión y devuelve el arco tangente del ángulo especificado.
  
```sql
SELECT ATAN(45.87) AS atanCalc1,  
    ATAN(-181.01) AS atanCalc2,  
    ATAN(0) AS atanCalc3,  
    ATAN(0.1472738) AS atanCalc4,  
    ATAN(197.1099392) AS atanCalc5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`atanCalc1  atanCalc2  atanCalc3  atanCalc4  atanCalc5`
  
`---------  ---------  ---------  ---------  ---------`
  
`1.55       -1.57       0.00       0.15       1.57`
  
## <a name="see-also"></a>Vea también
[CEILING &#40; Transact-SQL &#41;](../../t-sql/functions/ceiling-transact-sql.md)  
[Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)
  
  


