---
title: Usar expresiones de dimensiones | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- expressions [MDX], dimensions
- dimensions [Analysis Services], MDX
ms.assetid: 1d40cffb-e88f-4284-93cf-d62ab4f08395
caps.latest.revision: "28"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1417fd747df92c84fe66e2c69996f57ab51875e1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="using-dimension-expressions"></a>Usar expresiones de dimensiones
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Las expresiones de dimensiones y jerarquía se usan normalmente al pasar parámetros a funciones MDX (Expresiones multidimensionales) para devolver miembros, conjuntos o tuplas de una jerarquía.  
  
 Las expresiones de dimensiones solo pueden ser expresiones simples porque son identificadores de objetos. Vea [expresiones &#40; MDX &#41; ](../mdx/expressions-mdx.md) para obtener una explicación de las expresiones simples y complejas.  
  
## <a name="dimension-expressions"></a>Expresiones de dimensiones  
 Una expresión de dimensión contiene un identificador de dimensión o una función de dimensión.  
  
 Las expresiones de dimensiones raramente se utilizan solas. Lo normal es que, en lugar de ello, desee especificar una jerarquía en una dimensión. La única excepción es cuando se trabaja con la dimensión Measures, que no tiene ninguna jerarquía.  
  
 En el ejemplo siguiente se muestra un miembro calculado que utiliza la expresión [Measures] junto con las funciones .Members y Count() para devolver el número de miembros de la dimensión Measures:  
  
 `WITH MEMBER [Measures].[MeasureCount] AS`  
  
 `COUNT([Measures].MEMBERS)`  
  
 `SELECT [Measures].[MeasureCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 Un identificador de dimensión aparece como *Dimension_Name* en la notación de BNF que se utiliza para describir las instrucciones MDX.  
  
## <a name="hierarchy-expressions"></a>Expresiones de jerarquías  
 Del mismo modo, las expresiones de jerarquía contienen un identificador de jerarquía o una función de jerarquía. En el ejemplo siguiente se muestra el uso de la expresión de jerarquía [Date].[Calendar], junto con las funciones .Levels y .Count, para devolver el número de niveles de la jerarquía Calendar de la dimensión Date:  
  
 `WITH MEMBER [Measures].[CalendarLevelCount] AS`  
  
 `[Date].[Calendar].Levels.Count`  
  
 `SELECT [Measures].[CalendarLevelCount] ON 0`  
  
 `FROM [Adventure Works]`  
  
 El escenario más común de uso de expresiones de jerarquía es junto con la función .Members, para devolver todos los miembros de una jerarquía. El ejemplo siguiente devuelve todos los miembros de [Date].[Calendar] en el eje de filas:  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `[Date].[Calendar].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Un identificador de jerarquía aparece como *Dimension_Name**.* *Hierarchy_Name* en la notación de BNF que se utiliza para describir las instrucciones MDX.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; MDX &#41;](../mdx/expressions-mdx.md)  
  
  
