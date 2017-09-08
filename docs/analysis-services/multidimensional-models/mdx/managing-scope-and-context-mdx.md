---
title: "Administrar el ámbito y contexto (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [MDX], context
- scope [MDX]
- CALCULATE statement
- This function [MDX]
- SCOPE statement
- scripts [MDX], scope
ms.assetid: 631e7c20-8be9-4c35-8609-76516aef19d1
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0a7878c4c2420a4f49d14e1a3f2121009fc1d5b3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="managing-scope-and-context-mdx"></a>Administrar el ámbito y el contexto (MDX)
  En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], un script de expresiones multidimensionales (MDX) se puede aplicar a todo el cubo, o a fragmentos determinados del mismo, en puntos específicos de la ejecución del script. El script MDX puede adoptar un enfoque en capas de los cálculos del cubo mediante el uso de pasos de cálculo.  
  
> [!NOTE]  
>  Para obtener más información sobre el impacto que tienen los pasos de cálculo, vea [Descripción de orden de paso y orden de resolución &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md).  
  
 Para controlar el paso de cálculo, el ámbito y el contexto de un script MDX, se pueden usar específicamente la instrucción CACULATE, la función **This** y la instrucción SCOPE.  
  
## <a name="using-the-calculate-statement"></a>Usar la instrucción CALCULATE  
 La instrucción CALCULATE rellena cada celda del cubo con datos agregados. Por ejemplo, el script MDX predeterminado tiene una única instrucción CALCULATE al principio del script.  
  
 Para obtener más información sobre la sintaxis de la instrucción CALCULATE, vea [CALCULATE &#40;instrucciónMDX&#41;](../../../mdx/mdx-scripting-calculate.md).  
  
> [!NOTE]  
>  Si el script contiene una instrucción SCOPE que incluya una instrucción CALCULATE, MDX evalúa la instrucción CALCULATE en el contexto del subcubo definido por la instrucción SCOPE, no en relación a todo el cubo.  
  
## <a name="using-the-this-function"></a>Usar la función This  
 La función **This** permite recuperar el subcubo actual en un script MDX. La función **This** también se puede usar para establecer con rapidez los valores de las celdas del subcubo actual en una expresión MDX. Por lo general, la función **This** se usa en combinación con la instrucción SCOPE para cambiar el contenido de un subcubo específico durante un paso de cálculo determinado.  
  
> [!NOTE]  
>  Si el script contiene una instrucción SCOPE que incluya una función **This** , MDX evalúa la función **This** en el contexto del subcubo definido por la instrucción SCOPE, no en relación a todo el cubo.  
  
### <a name="this-function-example"></a>Ejemplo de la función This  
 En el siguiente ejemplo de un comando de script MDX, se usa la función **This** para aumentar el valor de la medida Amount (en el grupo de medida Finance del cubo de ejemplo de [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)]) en un 10 % para los elementos secundarios del miembro Redmond de la dimensión Customer:  
  
```  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 Para obtener más información sobre la sintaxis de la función **This**, vea [This &#40;MDX&#41;](../../../mdx/this-mdx.md).  
  
## <a name="using-the-scope-statement"></a>Usar la instrucción SCOPE  
 La instrucción SCOPE define el subcubo actual que contiene otras expresiones e instrucciones MDX en el script MDX y especifica su ámbito. MDX evalúa estas otras expresiones e instrucciones MDX, incluida la función **This** y la instrucción CALCULATE, en el contexto del subcubo.  
  
 Las instrucciones SCOPE son dinámicas, pero no iterativas por naturaleza. Las instrucciones incluidas en una instrucción SCOPE se ejecutan una sola vez, pero el subcubo en sí puede determinarse dinámicamente. Por ejemplo, suponga que tiene un cubo denominado SampleCube. A continuación aplica la siguiente instrucción SCOPE al cubo SampleCube para definir un subcubo que defina a su vez el contexto como ALLMEMBERS en la dimensión Measures:  
  
 `SCOPE([Measures].ALLMEMBERS);`  
  
 `THIS = [Measures].ALLMEMBERS.COUNT;`  
  
 `END SCOPE;`  
  
 Las instrucciones y expresiones de esta instrucción SCOPE se ejecutan una vez.  
  
 A continuación, un usuario del negocio ejecuta la siguiente consulta MDX que incluye una medida, denominada ExistingMeasure, en el cubo SampleCube:  
  
 `WITH MEMBER [Measures].[NewMeasure] AS '1'`  
  
 `SELECT`  
  
 `[Measures].ALLMEMBERS ON COLUMNS,`  
  
 `[Customer].DEFAULTMEMBER ON ROWS`  
  
 `FROM`  
  
 `[SampleCube]`  
  
 El conjunto de celdas que devuelve la consulta se parece al resultado que se muestra en la siguiente tabla.  
  
||[ExistingMeasure]|[NewMeasure]|  
|-|-------------------------|--------------------|  
|[Customer].[All]|2|2|  
  
 Si examinamos el conjunto de celdas devuelto, veremos que el valor ExistingMeasure, incluido en la instrucción SCOPE del script MDX, se actualiza dinámicamente después de definir la medida NewMeasure.  
  
 Las instrucciones SCOPE pueden anidarse en otras instrucciones SCOPE. Sin embargo, dado que las instrucciones SCOPE no son iterativas, el objetivo principal de anidar este tipo de instrucciones radica en la posibilidad de subdividir todavía más un subcubo para tratamientos especiales.  
  
### <a name="scope-statement-example"></a>Ejemplo de la instrucción SCOPE  
 En el siguiente ejemplo de script MDX se utiliza la instrucción SCOPE para aumentar el valor de la medida Amount (en el grupo de medida Finance del cubo de ejemplo de [!INCLUDE[ssAWDWsp](../../../includes/ssawdwsp-md.md)] ) en un 10% para los elementos secundarios del miembro Redmond de la dimensión Customer. No obstante, otra instrucción SCOPE cambia el subcubo de forma que incluya la medida Amount para los elementos secundarios del año 2002. Por último, la medida Amount se agrega solo a dicho subcubo, sin modificar los valores agregados de la medida Amount correspondientes a otros años.  
  
```  
/* Calculate the entire cube first. */  
CALCULATE;  
/* This SCOPE statement defines the current subcube */  
SCOPE([Customer].&[Redmond].MEMBERS,   
    [Measures].[Amount], *);  
        /* This expression sets the value of the Amount measure */  
        THIS = [Measures].[Amount] * 1.1;  
END SCOPE;  
```  
  
 Para obtener más información sobre la sintaxis de la instrucción SCOPE, vea [SCOPE &#40;Instrucción,MDX&#41;](../../../mdx/mdx-scripting-scope.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [El Script MDX básico &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
