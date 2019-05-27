---
title: ^ (OR exclusivo bit a bit) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: db54a0b9855a659d2c9751bd1a46bd18ed9bf923
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983135"
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
 Es cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) válida de uno de los tipos de datos de la categoría del tipo de datos entero, o los tipos de datos **bit**, **binary** o **varbinary**. *expression* se trata como un número binario para la operación bit a bit.  
  
> [!NOTE]  
>  Solo una *expression* puede ser del tipo de datos **binary** o **varbinary** en una operación bit a bit.  
  
## <a name="result-types"></a>Tipos de resultado  
 **int** si los valores de entrada son **int**.  
  
 **smallint** si los valores de entrada son **smallint**.  
  
 **tinyint** si los valores de entrada son **tinyint**.  
  
## <a name="remarks"></a>Notas  
 El operador **^** bit a bit realiza una operación OR lógica exclusiva bit a bit entre dos expresiones y, para ello, toma cada bit correspondiente de ambas expresiones. Los bits del resultado se establecen en 1 si alguno (pero no ambos) de los bits (en el caso del bit actual que se resuelve) de las expresiones de entrada tiene el valor 1. Si ambos bits son 0 ó 1, el bit del resultado se establece en el valor 0.  
  
 Si las expresiones de la izquierda y de la derecha tienen tipos de datos de entero diferentes (por ejemplo, *expression* de la izquierda es de tipo **smallint** y *expression* de la derecha es de tipo **int**), el argumento del tipo de datos más pequeño se convierte al tipo de datos mayor. En este caso, **smallint**_expression_ se convierte en **int**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea una tabla con el tipo de datos **int** que almacena los valores originales e inserta dos valores en una fila.  
  
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
  

  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores bit a bit &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)   
 [^= &#40;Asignación de OR exclusivo bit a bit&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)   
 [Operadores compuestos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


