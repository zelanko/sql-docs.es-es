---
title: Operadores bit a bit (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 5d04924a82578040f801864bb68905feebc53e94
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="bitwise-operators-transact-sql"></a>Operadores bit a bit (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Los operadores bit a bit realizan manipulaciones de bits entre dos expresiones de cualquiera de los tipos de datos de la categoría del tipo de datos entero.  
  Operadores bit a bit convertir dos valores enteros en bits binarios, lleve a cabo la operación AND, OR, o la operación NOT en cada bit, generar un resultado. A continuación, convierte el resultado en un entero.  
  
  Por ejemplo, el entero 170 convierte a binario 1010 1010.
El 75 de entero se convierte en 0100 1011 binario.

|operador|matemáticas bit a bit|
|---- |---- |
|y <br> Si bits en cualquier ubicación están establecidos en 1, el resultado es 1. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|o <br> Si cualquiera de los bits en cualquier ubicación es 1, el resultado es 1. |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> Invierte el valor de bit en cada ubicación de bits. |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
Vea los temas siguientes:   
* [& (AND bit a bit)](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = (AND bit a bit igual)](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124; (OR bit a bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = (OR bit a bit igual)](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ (Bit a bit OR exclusivo)](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = (Igual a OR exclusivo bit a bit)](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ (NOT bit a bit)](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 Los operandos de operadores bit a bit pueden tener uno de los tipos de datos de los enteros o categorías de tipos de datos de cadena binaria (excepto para la **imagen** tipo de datos), excepto que ambos operandos no pueden ser cualquiera de los tipos de datos de la cadena binaria categoría de tipo de datos. La siguiente tabla muestra los tipos de datos de operando admitidos.  
  
|Operando izquierdo|Operando derecho|  
|------------------|-------------------|  
|[binario](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint**, o **tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**, **smallint**, **tinyint**, o **bits**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binario**, o **varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binario**, o **varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**, **smallint**, **tinyint**, **binario**, o **varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**, **smallint**, o **tinyint**|  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  

