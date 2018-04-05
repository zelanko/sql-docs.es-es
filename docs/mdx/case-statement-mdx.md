---
title: CASE (instrucción) (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CASE
ms.assetid: 0aee3b4a-d5f7-4c9a-87b8-e5efc2da6b6d
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a4dbcc7ab42a0e044be0c7561adff4049fd8d1b9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="case-statement-mdx"></a>Instrucción CASE  (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 Un valor escalar especificado con que el *input_expression* se evalúa, que cuando evalúa como true, devuelve el valor escalar de la *else_result_expression*.  
  
 *when_true_result_expression*  
 Valor escalar devuelto cuando la cláusula WHEN se evalúa como true.  
  
 *else_result_expression*  
 Valor escalar devuelto cuando ninguna de las cláusulas WHEN se evalúa como true.  
  
 *Boolean_expression*  
 Expresión MDX que se evalúa como un valor escalar.  
  
## <a name="remarks"></a>Comentarios  
 Si no existe ninguna cláusula ELSE y todas las cláusulas WHEN son falsas, el resultado será una celda vacía.  
  
## <a name="simple-case-expression"></a>Expresión CASE sencilla  
 MDX evalúa una expresión case sencilla mediante la resolución de la *input_expression* en un valor escalar. Este valor escalar, a continuación, se compara con el valor escalar de la *when_expression*. Si los dos valores escalares coinciden, la instrucción CASE devuelve el valor de la *when_true_expression*. Si los dos valores escalares no coinciden, se evalúa la siguiente cláusula WHEN. Si todas las cláusulas WHEN se evalúan como false, el valor de *else_result_expression* de la cláusula ELSE, si existe, se devuelve.  
  
 En el ejemplo siguiente, la medida Reseller Order Count se evalúa con varias cláusulas WHEN y devuelve un resultado basado en el valor de la medida Reseller Order Count de cada año. Para los valores Reseller Order Count que no coincide con un valor escalar especificado en un *when_expression* en una cláusula WHEN, el valor escalar de la *else_result_expression* se devuelve.  
  
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
  
 En el ejemplo siguiente, se evalúa la medida Reseller Order Count con especificado *Boolean_expression* para cada una de las diferentes cláusulas WHEN. Se devuelve un resultado basado en el valor de la medida Reseller Order Count de cada año. Debido a que las cláusulas WHEN se evalúan en el orden en que aparecen, a todos los valores mayores que 6 se les puede asignar fácilmente el valor "VERY LARGE" sin tener que especificar cada valor explícitamente. Para los valores Reseller Order Count que no se especifican en una cláusula WHEN, el valor escalar de la *else_result_expression* se devuelve.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de Scripting de MDX &#40; MDX &#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
