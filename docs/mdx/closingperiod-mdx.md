---
title: ClosingPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 102485ede0e52389d43bdb64742a2564aaa71419
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68016793"
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)


  Devuelve el miembro que es el último del mismo nivel entre los descendientes de un miembro especificado en un nivel especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Observaciones  
 Esta función está diseñada básicamente para utilizarse en una dimensión de tipo Time, pero se puede utilizar con cualquier dimensión.  
  
-   Si se especifica una expresión de nivel, la función **ClosingPeriod** usa la dimensión que contiene el nivel especificado y devuelve el último elemento del mismo nivel entre los descendientes del miembro predeterminado en el nivel especificado.  
  
-   Si se especifican una expresión de nivel y una expresión de miembro, la función **ClosingPeriod** devuelve el último elemento del mismo nivel entre los descendientes del miembro especificado en el nivel especificado.  
  
-   Si no se especifica una expresión de nivel ni una expresión de miembro, la función **ClosingPeriod** utiliza el nivel predeterminado y el miembro de la dimensión (si existe) en el cubo con un tipo de tiempo.  
  
 La función **ClosingPeriod** es equivalente a la siguiente instrucción MDX:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  La función [OpeningPeriod](../mdx/openingperiod-mdx.md) es similar a la función **ClosingPeriod** , salvo que la función **OpeningPeriod** devuelve el primer elemento del mismo nivel en lugar del último elemento del mismo nivel.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro FY2005 de la dimensión Date (que posee un tipo semántico Time). Se devuelve este miembro debido a que el nivel Fiscal Year es el primer descendiente del nivel [All], la jerarquía Fiscal es la predeterminada debido a que es la primera jerarquía definida por el usuario de la colección de jerarquías, y el miembro FY 2007 es el último miembro del mismo nivel de esta jerarquía en este nivel.  
  
```  
SELECT ClosingPeriod() ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro November 30, 2006 en el nivel Date.Date.Date de la jerarquía de atributo Date.Date. Este miembro es el último miembro del mismo nivel que el descendiente del nivel [All] de la jerarquía de atributo Date.Date.  
  
```  
SELECT ClosingPeriod ([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro December, 2003, que es el último miembro del mismo nivel que el descendiente del miembro 2003 en el nivel de año de la jerarquía definida por el usuario Calendar.  
  
```  
SELECT ClosingPeriod ([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro June, 2003, que es el último miembro del mismo nivel que el descendiente del miembro 2003 en el nivel de año de la jerarquía definida por el usuario Fiscal.  
  
```  
SELECT ClosingPeriod ([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [&#41;OpeningPeriod &#40;MDX](../mdx/openingperiod-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [&#41;LastSibling &#40;MDX](../mdx/lastsibling-mdx.md)  
  
  
