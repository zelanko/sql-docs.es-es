---
title: '| (OR bit a bit) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '|'
- '|_TSQL'
- Bitwise OR
- bitwise
- OR
dev_langs:
- TSQL
helpviewer_keywords:
- OR operator
- bitwise OR (|)
- '| (bitwise OR operator)'
ms.assetid: 86a3b87f-9688-4eaf-a552-29f1b01d880a
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4410c086ed5fdca8fa4812a96c13bac6f692c8ae
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67942956"
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
 Es cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) válida de la categoría de tipo de datos entero o de los tipos de datos **bit**, **binary** o **varbinary**. *expression* se trata como un número binario para la operación bit a bit.  
  
> [!NOTE]  
>  Solo una *expression* puede ser del tipo de datos **binary** o **varbinary** en una operación bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve un **int** si los valores de entrada son **int**; un **smallint** si los valores de entrada son **smallint**, o un **tinyint** si los valores de entrada son **tinyint**.  
  
## <a name="remarks"></a>Observaciones  
 El operador | de bit a bit realiza una operación OR lógica de bit a bit entre las dos expresiones y, para ello, toma cada bit correspondiente de ambas expresiones. Los bits del resultado se establecen en 1 si alguno o ambos bits (para el bit actual que se resuelve) de las expresiones de entrada tienen el valor 1; si ninguno de los bits de la expresión de entrada es 1, el bit del resultado se establece en 0.  
  
 Si las expresiones de la izquierda y de la derecha tienen tipos de datos de entero diferentes (por ejemplo, *expression* de la izquierda es de tipo **smallint** y *expression* de la derecha es de tipo **int**), el argumento del tipo de datos más pequeño se convierte al tipo de datos mayor. En este ejemplo, **smallint**_expression_ se convierte en **int**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una tabla con tipos de datos **int** para mostrar los valores originales y se pone la tabla en una fila.  
  
```sql  
CREATE TABLE bitwise  
(   
 a_int_value int NOT NULL,  
b_int_value int NOT NULL  
);  
GO  
INSERT bitwise VALUES (170, 75);  
GO  
```  
  
 La siguiente consulta realiza la operación OR bit a bit en las columnas **a_int_value** y **b_int_value**.  
  
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
  
 La representación binaria de 170 (**a_int_value** o `A`, abajo) es `0000 0000 1010 1010`. La representación binaria de 75 (**b_int_value** o `B`, abajo) es `0000 0000 0100 1011`. Al realizar la operación OR bit a bit en estos dos valores, se produce el resultado binario `0000 0000 1110 1011`, que es 235 en decimal.  
  
```  
(A | B)  
0000 0000 1010 1010  
0000 0000 0100 1011  
-------------------  
0000 0000 1110 1011  
```  
  
## <a name="see-also"></a>Consulte también  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [&#124;= &#40;Bitwise OR Assignment&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)  (&#124;= [Asignación de OR bit a bit] [Transact-SQL])  
 [Operadores compuestos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


