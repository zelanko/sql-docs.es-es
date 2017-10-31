---
title: LOG10 (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG10
- LOG10_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- LOG10 function
- base-10 logarithms
- logarithm of expression
ms.assetid: 1eb7fb34-1937-4a39-a936-f5c0c7c7e06f
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d8cc5b0ef6af319e55744a3ca373f0e6b11e230b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="log10-transact-sql"></a>LOG10 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el logaritmo en base 10 del elemento especificado **float** expresión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
LOG10 ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de tipo **float** o de un tipo que pueda convertirse implícitamente a **float**.  
  
## <a name="return-types"></a>Tipos devueltos  
 **float**  
  
## <a name="remarks"></a>Comentarios  
 Las funciones LOG10 y POWER están relacionadas inversamente entre sí. Por ejemplo, 10 ^ LOG10 (*n*) =  *n* .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calculating-the-base-10-logarithm-for-a-variable"></a>A. Calcular el logaritmo en base 10 para una variable  
 En el siguiente ejemplo se calcula el `LOG10` de la variable especificada.  
  
```  
DECLARE @var float;  
SET @var = 145.175643;  
SELECT 'The LOG10 of the variable is: ' + CONVERT(varchar,LOG10(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The LOG10 of the variable is: 2.16189      
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-result-of-raising-a-base-10-logarithm-to-a-specified-power"></a>B. Calcular el resultado de elevar un logaritmo en base 10 a una potencia especificada  
 En el siguiente ejemplo se devuelve el resultado de elevar un logaritmo en base 10 a una potencia especificada.  
  
```  
SELECT POWER (10, LOG10(5));   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------  
5  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-base-10-logarithm-for-a-value"></a>C: calcular el logaritmo en base 10 de un valor.  
 En el ejemplo siguiente se calcula el `LOG10` del valor especificado.  
  
```  
SELECT LOG10(145.175642);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
-------------------  
2.16
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [ALIMENTACIÓN &#40; Transact-SQL &#41;](../../t-sql/functions/power-transact-sql.md)   
 [Registro &#40; Transact-SQL &#41;](../../t-sql/functions/log-transact-sql.md)  
  
  


