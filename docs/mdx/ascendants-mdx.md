---
title: Ascendants (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 16c6f812d1d7cae5a81a8e64fb425f4d33f4cb5c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017062"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  Devuelve el conjunto de antecesores de un miembro especificado, incluyendo el propio miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **antecesores** función devuelve todos los antecesores de un miembro desde el propio miembro hasta la parte superior de la jerarquía del miembro; más específicamente, realiza un recorrido transversal posterior a la de la jerarquía del miembro especificado y, a continuación, Devuelve todos los miembros ascendentes relacionados con el miembro, incluido él mismo, en un conjunto. Esto es por el contrario el [antecesor](../mdx/ancestor-mdx.md) función, que devuelve un miembro antecesor específico, o antecesor, en un nivel específico.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el número de pedidos de distribuidores para el `[Sales Territory].[Northwest]` miembro y todos los antecesores de ese miembro desde el **Adventure Works** cubo. El **antecesores** función crea el conjunto que incluye el `[Sales Territory].[Northwest]` miembro y sus antecesores para el eje de filas.  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
