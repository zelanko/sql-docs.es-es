---
title: OpeningPeriod (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 07f94c3ed850af10120b1de7d95941bc5c90e826
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088219"
---
# <a name="openingperiod-mdx"></a>OpeningPeriod (MDX)


  Devuelve el primer miembro del mismo nivel entre los descendientes de un nivel especificado (opcionalmente, en un miembro especificado).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OpeningPeriod( [ Level_Expression [ , Member_Expression ] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 Esta función se ha diseñado básicamente para su uso con la dimensión Time, aunque también se puede utilizar con cualquier dimensión.  
  
-   Si se especifica una expresión de nivel, el **OpeningPeriod** función usa la jerarquía que contiene el nivel especificado y devuelve el primer nodo relacionado entre los descendientes del miembro predeterminado en el nivel especificado.  
  
-   Si se especifican una expresión de nivel y una expresión de miembro, el **OpeningPeriod** función devuelve el primer nodo relacionado entre los descendientes del miembro especificado en el nivel especificado dentro de la jerarquía que contiene el texto especificado nivel.  
  
-   Si se especifica ni una expresión de nivel ni una expresión de miembro, el **OpeningPeriod** función usa el nivel predeterminado y un miembro de la dimensión con un tipo de tiempo.  
  
> [!NOTE]  
>  El [ClosingPeriod](../mdx/closingperiod-mdx.md) función es similar a la **OpeningPeriod** funcione, salvo que el **ClosingPeriod** función devuelve el último elemento relacionado en lugar del primero elemento del mismo nivel.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro FY2002 de la dimensión Date (que posee un tipo Time). Se devuelve este miembro debido a que el nivel Fiscal Year es el primer descendiente del nivel [All], la jerarquía Fiscal es la predeterminada debido a que es la primera jerarquía definida por el usuario de la colección de jerarquías, y el miembro FY 2002 es el primer miembro del mismo nivel de esta jerarquía en este nivel.  
  
```  
SELECT OpeningPeriod() ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro July 1, 2001 en el nivel Date.Date.Date de la jerarquía de atributo Date.Date. Este miembro es el primer miembro del mismo nivel del descendiente del nivel [All] de la jerarquía de atributo Date.Date.  
  
```  
SELECT OpeningPeriod([Date].[Date].[Date]) ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro January, 2003, que es el primer miembro del mismo nivel que el descendiente del miembro 2003 en el nivel de año de la jerarquía definida por el usuario Calendar.  
  
```  
SELECT OpeningPeriod([Date].[Calendar].[Month],[Date].[Calendar].[Calendar Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve el valor de la medida predeterminada para el miembro July, 2002, que es el primer miembro del mismo nivel que el descendiente del miembro 2003 en el nivel de año de la jerarquía definida por el usuario Fiscal.  
  
```  
SELECT OpeningPeriod([Date].[Fiscal].[Month],[Date].[Fiscal].[Fiscal Year].&[2003]) ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [FirstSibling &#40;MDX&#41;](../mdx/firstsibling-mdx.md)  
  
  
