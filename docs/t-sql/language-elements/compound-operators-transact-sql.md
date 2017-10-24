---
title: Operadores (Transact-SQL) compuesta | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server (starting with 2008)
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2e5fde8cd4265359722f33400d834b0a301718ef
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="compound-operators-transact-sql"></a>Operadores compuestos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Los operadores compuestos ejecutan operaciones y establecen un valor original en el resultado de dichas operaciones. Por ejemplo, si una variable @x es igual a 35, a continuación, @x += 2 toma el valor original de @x, agregar 2 y establece @x en el nuevo valor (37).  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] proporciona los operadores compuestos siguientes:  
  
|Operador|Más información|Acción|  
|--------------|------------------------------|------------|  
|+=|[+= &#40; Agregar es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|Agrega una cantidad al valor original y establece este en el resultado de la operación.|  
|-=|[-= &#40; Restar igual &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md)|Resta una cantidad del valor original y establece este en el resultado de la operación.|  
|*=|[&#42; = &#40; Multiplicar igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md)|Multiplica por una cantidad y establece el valor original en el resultado de la operación.|  
|/=|[&#40; dividir es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|Divide por una cantidad y establece el valor original en el resultado de la operación.|  
|%=|[Módulo igual &#40; Transact-SQL &#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)|Divide por una cantidad y establece el valor original en el módulo.|  
|&=|[& = &#40; AND bit a bit igual &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|Realiza una operación AND bit a bit y establece el valor original en el resultado de la operación.|  
|^=|[^ = &#40; Bit a bit OR exclusivo es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|Realiza una operación OR exclusiva bit a bit y establece el valor original en el resultado de la operación.|  
|&#124;=|[&#124; = &#40; OR bit a bit igual &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)|Realiza una operación OR bit a bit y establece el valor original en el resultado de la operación.|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de uno de los datos de tipos de la categoría numérica.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información, consulte los temas relacionados con cada operador.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes, se muestran las operaciones compuestas.  
  
```  
DECLARE @x1 int = 27;  
SET @x1 += 2 ;  
SELECT @x1 AS Added_2;  
  
DECLARE @x2 int = 27;  
SET @x2 -= 2 ;  
SELECT @x2 AS Subtracted_2;  
  
DECLARE @x3 int = 27;  
SET @x3 *= 2 ;  
SELECT @x3 AS Multiplied_by_2;  
  
DECLARE @x4 int = 27;  
SET @x4 /= 2 ;  
SELECT @x4 AS Divided_by_2;  
  
DECLARE @x5 int = 27;  
SET @x5 %= 2 ;  
SELECT @x5 AS Modulo_of_27_divided_by_2;  
  
DECLARE @x6 int = 9;  
SET @x6 &= 13 ;  
SELECT @x6 AS Bitwise_AND;  
  
DECLARE @x7 int = 27;  
SET @x7 ^= 2 ;  
SELECT @x7 AS Bitwise_Exclusive_OR;  
  
DECLARE @x8 int = 27;  
SET @x8 |= 2 ;  
SELECT @x8 AS Bitwise_OR;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  

