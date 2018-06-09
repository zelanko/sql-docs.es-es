---
title: Usar expresiones de dimensiones | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a5e26d56a52c8c922c43325bd2267fa623dc0e19
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743914"
---
# <a name="using-dimension-expressions"></a>Usar expresiones de dimensiones


  Las expresiones de dimensiones y jerarquía se usan normalmente al pasar parámetros a funciones MDX (Expresiones multidimensionales) para devolver miembros, conjuntos o tuplas de una jerarquía.  
  
 Las expresiones de dimensiones solo pueden ser expresiones simples porque son identificadores de objetos. Vea [expresiones &#40;MDX&#41; ](../mdx/expressions-mdx.md) para obtener una explicación de las expresiones simples y complejas.  
  
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
  
 Un identificador de jerarquía aparece como *Dimension_Name **.** Hierarchy_Name* en la notación de BNF que se utiliza para describir las instrucciones MDX.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;MDX&#41;](../mdx/expressions-mdx.md)  
  
  
