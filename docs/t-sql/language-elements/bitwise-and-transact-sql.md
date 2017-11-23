---
title: '&amp;(AND bit a bit) (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bitwise
- '&'
- '&_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- AND, bitwise AND
- '& (bitwise AND)'
- bitwise AND (&)
ms.assetid: 20275755-4fa7-47b1-a9be-ac85606d63b0
caps.latest.revision: "42"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: d249ca1552197a5fb7e53540c40e70c864d134bb
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="amp-bitwise-and-transact-sql"></a>&amp;(AND bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Realiza una operación lógica AND bit a bit entre dos valores enteros.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression & expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquiera de los tipos de datos de la categoría de tipo de datos entero, o la **bits**, o la **binario** o **varbinary** datos tipos. *expresión* se trata como un número binario para la operación bit a bit.  
  
> [!NOTE]  
>  En una operación bit a bit, solo uno *expresión* puede ser del **binario** o **varbinary** tipo de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** si los valores de entrada son **int**.  
  
 **smallint** si los valores de entrada son **smallint**.  
  
 **tinyint** si los valores de entrada son **tinyint** o **bits**.  
  
## <a name="remarks"></a>Comentarios  
 El  **&**  operador bit a bit realiza una operación lógica AND bit a bit entre las dos expresiones, toma cada bit de ambas expresiones correspondiente. Los bits del resultado se establecen en 1 si y solo si los dos bits (para el bit actual que se resuelve) de las expresiones de entrada tienen el valor 1; de otro modo, el bit del resultado se establece en 0.  
  
 Si las expresiones izquierdas y derecha tienen tipos de datos enteros diferentes (por ejemplo, a la izquierda *expresión* es **smallint** y el derecho *expresión* es  **int**), el argumento del tipo de datos más pequeño se convierte al tipo de datos mayor. En este caso, el **smallint***expresión* se convierte en una **int**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una tabla con el **int** tipo para almacenar los valores de datos e inserta dos valores en una fila.  
  
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
  
 Esta consulta realiza una operación AND bit a bit entre las columnas `a_int_value` y `b_int_value`.  
  
```  
SELECT a_int_value & b_int_value  
FROM bitwise;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
-----------   
10            
  
(1 row(s) affected)  
```  
  
 La representación binaria de 170 (`a_int_value` o `A`) es `0000 0000 1010 1010`. La representación binaria de 75 (`b_int_value` o `B`) es `0000 0000 0100 1011`. Al realizar la operación AND bit a bit con estos dos valores, se obtiene el resultado binario `0000 0000 0000 1010`, que es el 10 en notación decimal.  
  
```  
(A & B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 0000 1010  
```  
  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [& = &#40; Asignación AND bit a bit &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


