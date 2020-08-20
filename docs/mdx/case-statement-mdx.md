---
description: Instrucción CASE  (MDX)
title: CASE (instrucción, MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a5907eb58fa102c46fa22af97116c4fad0f217a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466507"
---
# <a name="case-statement-mdx"></a>Instrucción CASE  (MDX)


  Permite obtener condicionalmente valores específicos de varias comparaciones. Hay dos tipos de instrucciones CASE:  
  
-   Una instrucción CASE simple que compara una expresión con un conjunto de expresiones simples para devolver valores específicos.  
  
-   Una instrucción CASE buscada que evalúa un conjunto de expresiones booleanas para devolver valores específicos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>Argumentos  
 *input_expression*  
 Expresión MDX (Expresiones multidimensionales) que se resuelve en un valor escalar.  
  
 *when_expression*  
 Un valor escalar especificado con el que se evalúa el *input_expression* , que cuando se evalúa como true, devuelve el valor escalar de la *else_result_expression*.  
  
 *when_true_result_expression*  
 Valor escalar devuelto cuando la cláusula WHEN se evalúa como true.  
  
 *else_result_expression*  
 Valor escalar devuelto cuando ninguna de las cláusulas WHEN se evalúa como true.  
  
 *Boolean_expression*  
 Expresión MDX que se evalúa como un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 Si no existe ninguna cláusula ELSE y todas las cláusulas WHEN son falsas, el resultado será una celda vacía.  
  
## <a name="simple-case-expression"></a>Expresión CASE sencilla  
 MDX evalúa una expresión Case simple resolviendo el *input_expression* en un valor escalar. A continuación, este valor escalar se compara con el valor escalar de la *when_expression*. Si los dos valores escalares coinciden, la instrucción CASE devuelve el valor de la *when_true_expression*. Si los dos valores escalares no coinciden, se evalúa la siguiente cláusula WHEN. Si todas las cláusulas WHEN se evalúan como false, se devuelve el valor de *else_result_expression* de la cláusula else, si existe.  
  
 En el ejemplo siguiente, la medida Reseller Order Count se evalúa con varias cláusulas WHEN y devuelve un resultado basado en el valor de la medida Reseller Order Count de cada año. En el caso de los valores de recuento de pedidos de distribuidor que no coinciden con un valor escalar especificado en una *when_expression* en una cláusula When, se devuelve el valor escalar de la *else_result_expression* .  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>Expresión CASE buscada  
 Para utilizar la expresión CASE a fin de realizar evaluaciones más complejas, utilice la expresión CASE buscada. Esta variación de la expresión de búsqueda permite evaluar si una expresión de entrada se encuentra dentro de un intervalo de valores. MDX evalúa las cláusulas WHEN en el orden en que éstas aparecen en la instrucción CASE.  
  
 En el ejemplo siguiente, la medida reseller Order Count se evalúa con la *Boolean_expression* especificada para cada una de varias cláusulas When. Se devuelve un resultado basado en el valor de la medida Reseller Order Count de cada año. Debido a que las cláusulas WHEN se evalúan en el orden en que aparecen, a todos los valores mayores que 6 se les puede asignar fácilmente el valor "VERY LARGE" sin tener que especificar cada valor explícitamente. En el caso de los valores de recuento de pedidos de distribuidor que no se especifican en una cláusula WHEN, se devuelve el valor escalar de la *else_result_expression* .  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>Consulte también  
 [Instrucciones para scripting de MDX &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
