---
title: Ascendants (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ef9cccb488cebb08c1b9721c40cb8037ea8687a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739624"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  Devuelve el conjunto de antecesores de un miembro especificado, incluyendo el propio miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
## <a name="remarks"></a>Notas  
 El **antecesores** función devuelve todos los antecesores de un miembro desde el propio miembro hasta la parte superior de la jerarquía del miembro; más específicamente, realiza un recorrido transversal posterior a la de la jerarquía para el miembro especificado y, a continuación, devuelve todos los miembros antecesores relacionados con el miembro, incluido él mismo, en un conjunto. Se trata de diferencia el [antecesor](../mdx/ancestor-mdx.md) función, que devuelve un miembro antecesor específico, o antecesor, en un nivel específico.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el número de pedidos de distribuidores el `[Sales Territory].[Northwest]` miembro y todos los antecesores de ese miembro de la **Adventure Works** cubo. El **antecesores** función crea el conjunto que incluye el `[Sales Territory].[Northwest]` miembro y sus antecesores para el eje de filas.  
  
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
  
  
