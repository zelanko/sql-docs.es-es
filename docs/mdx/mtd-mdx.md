---
title: MTd (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e38d8d3485e50054ee4d1106b1ef7bdfc8ce96ea
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580767"
---
# <a name="mtd-mdx"></a>Mtd (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de año en la dimensión de tiempo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 Si no se especifica una expresión de miembro, el valor predeterminado es el miembro actual de la primera jerarquía con un nivel de tipo *meses* en la primera dimensión de tipo *tiempo* en el grupo de medida.  
  
 El **Mtd** función es una función abreviada para la [PeriodsToDate](../mdx/periodstodate-mdx.md) funcionar cuando se establece la propiedad Type de la jerarquía de atributo en el que se basa un nivel en *meses*. Es decir, `Mtd(Member_Expression)` es equivalente a `PeriodsToDate(Month_Level_Expression,Member_Expression)`.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve la suma de los costos de flete de las ventas por Internet del mes de julio de 2002 hasta el día 20 de julio.  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Suma &#40;MDX&#41;](../mdx/sum-mdx.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
