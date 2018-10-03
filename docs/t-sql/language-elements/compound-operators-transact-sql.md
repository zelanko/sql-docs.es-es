---
title: Operadores compuestos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators
- compound operators, described
ms.assetid: 5072fe91-02d3-42a7-831f-756eff714a17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bdd527404381156dbe23db1554b081bdd40e6620
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47835083"
---
# <a name="compound-operators-transact-sql"></a>Operadores compuestos (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Los operadores compuestos ejecutan operaciones y establecen un valor original en el resultado de dichas operaciones. Por ejemplo, si una variable @x es igual a 35, @x += 2 toma el valor original de @x, suma 2 y establece @x en el nuevo valor (37).  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] proporciona los operadores compuestos siguientes:  
  
|Operador|Más información|Acción|  
|--------------|------------------------------|------------|  
|+=|[+= &#40;Asignación de suma&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-equals-transact-sql.md)|Agrega una cantidad al valor original y establece este en el resultado de la operación.|  
|-=|[-= &#40;Subtract Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/subtract-equals-transact-sql.md) (-= [Asignación de resta] [Transact-SQL])|Resta una cantidad del valor original y establece este en el resultado de la operación.|  
|*=|[&#42;= &#40;Multiply Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/multiply-equals-transact-sql.md) (&#42;= [Asignación de multiplicación] [Transact-SQL])|Multiplica por una cantidad y establece el valor original en el resultado de la operación.|  
|/=|[&#40;Divide Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/divide-equals-transact-sql.md)|Divide por una cantidad y establece el valor original en el resultado de la operación.|  
|%=|[Modulus Assignment &#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md) (Asignación de módulo [Transact-SQL])|Divide por una cantidad y establece el valor original en el módulo.|  
|&=|[&= &#40;Asignación de AND bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)|Realiza una operación AND bit a bit y establece el valor original en el resultado de la operación.|  
|^=|[^= &#40;Asignación de OR exclusivo bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)|Realiza una operación OR exclusiva bit a bit y establece el valor original en el resultado de la operación.|  
|&#124;=|[&#124;= &#40;Bitwise OR Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md) (&#124;= [Asignación de OR bit a bit] [Transact-SQL])|Realiza una operación OR bit a bit y establece el valor original en el resultado de la operación.|  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
expression operator expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) válida de uno de los tipos de datos de la categoría numérica.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Notas  
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
  
## <a name="see-also"></a>Ver también  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
  
  
