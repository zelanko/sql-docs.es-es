---
title: '| (OR bit a bit) (Transact-SQL) | Documentos de Microsoft'
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
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs: TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 47d4b177e93d028ccf0afffec6a9480928e11cb0
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="-bitwise-or-transact-sql"></a>| (OR bit a bit) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Realiza una operación OR bit a bit lógica entre dos valores de tipo entero especificados tal y como aparecen traducidos en expresiones binarias en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```   
expression | expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de la categoría de tipo de datos entero, o la **bits**, **binario**, o **varbinary** tipos de datos. *expresión* se trata como un número binario para la operación bit a bit.  
  
> [!NOTE]  
>  Solo un *expresión* puede ser del **binario** o **varbinary** tipo de datos en una operación bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve un **int** si los valores de entrada son **int**, **smallint** si los valores de entrada son **smallint**, o un **tinyint** si los valores de entrada son **tinyint**.  
  
## <a name="remarks"></a>Comentarios  
 El operador | de bit a bit realiza una operación OR lógica de bit a bit entre las dos expresiones y, para ello, toma cada bit correspondiente de ambas expresiones. Los bits del resultado se establecen en 1 si alguno o ambos bits (para el bit actual que se resuelve) de las expresiones de entrada tienen el valor 1; si ninguno de los bits de la expresión de entrada es 1, el bit del resultado se establece en 0.  
  
 Si las expresiones izquierdas y derecha tienen tipos de datos enteros diferentes (por ejemplo, a la izquierda *expresión* es **smallint** y el derecho *expresión* es  **int**), el argumento del tipo de datos más pequeño se convierte al tipo de datos mayor. En este ejemplo, el **smallint***expresión* se convierte en una **int**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una tabla con **int** datos tipos que se van a mostrar los valores originales y se coloca en la tabla en una fila.  
  
```tsql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 La siguiente consulta realiza la operación OR bit a bit en el **a_int_value** y **b_int_value** columnas.  
  
```  
SELECT a_int_value | b_int_value  
FROM bitwise;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-----------   
235           
  
(1 row(s) affected)  
```  
  
 La representación binaria de 170 (**a_int_value** o `A`, a continuación) es `0000 0000 1010 1010`. La representación binaria de 75 (**b_int_value** o `B`, a continuación) es `0000 0000 0100 1011`. Al realizar la operación OR bit a bit en estos dos valores, se produce el resultado binario `0000 0000 1110 1011`, que es 235 en decimal.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124; = &#40; OR bit a bit asignación &#41; &#40; Transact-SQL &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


