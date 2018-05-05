---
title: ClosingPeriod (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CLOSINGPERIOD
dev_langs:
- kbMDX
helpviewer_keywords:
- ClosingPeriod function
ms.assetid: ae709017-219d-43e1-a98a-a85bd365b4cd
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 43094cc0934c516a871e249fd9bbdc22d0c4bf12
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="closingperiod-mdx"></a>ClosingPeriod (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el miembro que es el último del mismo nivel entre los descendientes de un miembro especificado en un nivel especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ClosingPeriod( [ Level_Expression [ ,Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Esta función está diseñada básicamente para utilizarse en una dimensión de tipo Time, pero se puede utilizar con cualquier dimensión.  
  
-   Si se especifica una expresión de nivel, la **ClosingPeriod** función utiliza la dimensión que contiene el nivel especificado y devuelve el último del mismo nivel entre los descendientes del miembro predeterminado en el nivel especificado.  
  
-   Si no se especifican una expresión de nivel y una expresión de miembro, el **ClosingPeriod** función devuelve el último del mismo nivel entre los descendientes del miembro especificado en el nivel especificado.  
  
-   Si se especifica una expresión de nivel ni una expresión de miembro, el **ClosingPeriod** función utiliza el nivel predeterminado y el miembro de la dimensión (si existe) en el cubo con un tipo de tiempo.  
  
 El **ClosingPeriod** función es equivalente a la siguiente instrucción MDX:  
  
 `Tail(Descendants(Member_Expression, Level_Expression), 1)`.  
  
> [!NOTE]  
>  El [OpeningPeriod](../mdx/openingperiod-mdx.md) función es similar a la **ClosingPeriod** funcione, salvo que la **OpeningPeriod** función devuelve el primer miembro del mismo nivel en lugar del último.  
  
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
  
## <a name="see-also"></a>Vea también  
 [OpeningPeriod &#40;MDX&#41;](../mdx/openingperiod-mdx.md)   
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)   
 [LastSibling &#40;MDX&#41;](../mdx/lastsibling-mdx.md)  
  
  
