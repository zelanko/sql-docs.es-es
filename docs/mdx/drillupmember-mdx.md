---
title: DrillupMember (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31981669d5d08e63a853b8daa530b886f9b7dfbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690764"
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)


  Devuelve los miembros de un conjunto especificado que no son descendientes de miembros de un segundo conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **DrillupMember** función devuelve un conjunto de miembros en función de los miembros especificados en el primer conjunto que son descendientes de miembros en el segundo conjunto. El primer conjunto puede tener varias dimensiones, pero el segundo conjunto debe contener un conjunto de una dimensión. Se mantiene el orden entre los miembros originales del primer conjunto. La función crea el conjunto mediante la inclusión únicamente de los miembros del primer conjunto que son descendientes inmediatos de miembros del segundo conjunto. Si el antecesor inmediato de un miembro del primer conjunto no se encuentra en el segundo conjunto, el miembro del primer conjunto se incluye en el conjunto devuelto por esta función. También se incluyen los descendientes del primer conjunto que preceden a un miembro antecesor del segundo conjunto.  
  
 El primer conjunto puede contener tuplas en vez de miembros. Obtención de detalles de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en vez de miembros.  
  
> [!IMPORTANT]  
>  Se reducirá el detalle de un miembro solo si va inmediatamente seguido por un elemento secundario o un descendiente. Es importante el orden de los miembros del conjunto para ambos la obtención de detalles\* y Drillup\* familias de funciones. Considere el uso de la **Hierarchize** función para ordenar adecuadamente los miembros del primer conjunto.  
  
## <a name="example"></a>Ejemplo  
 Los tres ejemplos siguientes son idénticos salvo por el segundo conjunto. En el primer ejemplo, el segundo conjunto es Estados Unidos. Como resultado, Colorado se excluye del conjunto de resultados. Es un descendiente de Estados Unidos.  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 El segundo ejemplo muestra la importancia del orden de los miembros. Puesto que **DrillupMember** solo explora en profundidad aquellos miembros seguidos inmediatamente por descendientes del primer conjunto, se muestran los detalles del miembro Canada. Canadá está separada de sus descendientes por Estados Unidos y Colorado. Si vuelve a ordenar los miembros para que Canadá quede directamente encima de Alberta, Alberta y Brunswick se excluirán del conjunto de filas.  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 Tercer ejemplo se muestra cómo el uso de **Hierarchize** puede mitigar los efectos del orden de los miembros y obtener los detalles del miembro Canada.  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
