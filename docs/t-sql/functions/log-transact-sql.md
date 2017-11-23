---
title: REGISTRO (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs: TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab2d021e583c3f4bec009e7959ea4fccfea8c5a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="log-transact-sql"></a>LOG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el logaritmo natural del elemento especificado **float** expresión en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
LOG ( float_expression [, base ] )  
```  
  
```  
-- Syntax for Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de tipo **float** o de un tipo que pueda convertirse implícitamente a **float**.  
  
 *base*  
 Argumento entero opcional que establece la base del logaritmo.  
  
**Se aplica a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
## <a name="return-types"></a>Tipos devueltos  
 **float**  
  
## <a name="remarks"></a>Comentarios  
 De forma predeterminada, **LOG()** devuelve el logaritmo natural. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede cambiar la base del logaritmo a otro valor mediante el uso opcional *base* parámetro.  
  
 El logaritmo natural es el logaritmo en base **e**, donde **e** es una constante irracional aproximadamente igual a 2,718281828.  
  
 El logaritmo natural del valor exponencial de un número es el número de sí misma: registro (EXP (  *n*  )) =  *n* . Y el valor exponencial del logaritmo natural de un número es el número propio: EXP (registro (  *n*  )) =  *n* .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. Calcular el logaritmo de un número  
 En el ejemplo siguiente se calcula el `LOG` para el elemento especificado **float** expresión.  
  
```  
DECLARE @var float = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(varchar, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. Calcular el logaritmo del exponente de un número  
 En el ejemplo siguiente se calcula el `LOG` del exponente de un número.  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. Calcular el logaritmo de un número  
 En el ejemplo siguiente se calcula el `LOG` para el elemento especificado **float** expresión.  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>Vea también  
 [Funciones matemáticas &#40; Transact-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40; Transact-SQL &#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40; Transact-SQL &#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

