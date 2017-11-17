---
title: ^ (Bit a bit OR exclusivo) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 01/10/2017
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
- ^_TSQL
- Bitwise Exclusive OR
- Exclusive
- ^
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- ^ (bitwise exclusive OR operator)
- OR operator
- exclusive OR mathematical operations
- bitwise exclusive OR (^)
ms.assetid: f38f0ad4-46d0-40ea-9851-0f928fda5293
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 635cdf87939b15fad65ba4cc103166bff2ba04d2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="-bitwise-exclusive-or-transact-sql"></a>^ (OR exclusivo bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Lleva a cabo una operación de OR exclusivo bit a bit entre dos valores enteros.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression ^ expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquiera de los tipos de datos de la categoría de tipo de datos entero, o la **bits**, o la **binario** o **varbinary** tipos de datos. *expresión* se trata como un número binario para la operación bit a bit.  
  
> [!NOTE]  
>  Solo un *expresión* puede ser del **binario** o **varbinary** tipo de datos en una operación bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** si los valores de entrada son **int**.  
  
 **smallint** si los valores de entrada son **smallint**.  
  
 **tinyint** si los valores de entrada son **tinyint**.  
  
## <a name="remarks"></a>Comentarios  
 El  **^**  operador bit a bit realiza un operador lógico OR exclusivo bit a bit entre las dos expresiones, toma cada bit de ambas expresiones correspondiente. Los bits del resultado se establecen en 1 si alguno (pero no ambos) de los bits (en el caso del bit actual que se resuelve) de las expresiones de entrada tiene el valor 1. Si ambos bits son 0 ó 1, el bit del resultado se establece en el valor 0.  
  
 Si las expresiones izquierdas y derecha tienen tipos de datos enteros diferentes (por ejemplo, a la izquierda *expresión* es **smallint** y el derecho *expresión* es  **int**), el argumento del tipo de datos más pequeño se convierte al tipo de datos mayor. En este caso, el **smallint***expresión* se convierte en una **int**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una tabla con el **int** datos escriba para almacenar los valores originales y se insertan dos valores en una fila.  
  
```  
CREATE TABLE bitwise  
(   
a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 En la consulta siguiente se lleva a cabo la operación de OR exclusivo bit a bit entre las columnas `a_int_value` y `b_int_value`.  
  
```  
SELECT a_int_value ^ b_int_value  
FROM bitwise;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
-----------   
225           
  
(1 row(s) affected)  
```  
  
 La representación binaria de 170 (`a_int_value` o `A`) es `0000 0000 1010 1010`. La representación binaria de 75 (`b_int_value` o `B`) es `0000 0000 0100 1011`. Realizar la operación de OR exclusivo bit a bit sobre estos dos valores produce el resultado binario `0000 0000 1110 0001`, que es el decimal 225.  
  
```  
(A ^ B)     
         0000 0000 1010 1010  
         0000 0000 0100 1011  
         -------------------  
         0000 0000 1110 0001  
```  
  

  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^ = &#40; Bit a bit OR exclusivo es igual a &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  



