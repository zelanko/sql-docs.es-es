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
ms.openlocfilehash: 5dfdec16d20173639cc92a80b1ca546f44b70334
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049192"
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
  
## <a name="remarks"></a>Observaciones  
 La función **DrillupMember** devuelve un conjunto de miembros en función de los miembros especificados en el primer conjunto que son descendientes de miembros del segundo conjunto. El primer conjunto puede tener varias dimensiones, pero el segundo conjunto debe contener un conjunto de una dimensión. Se mantiene el orden entre los miembros originales del primer conjunto. La función crea el conjunto mediante la inclusión únicamente de los miembros del primer conjunto que son descendientes inmediatos de miembros del segundo conjunto. Si el antecesor inmediato de un miembro del primer conjunto no se encuentra en el segundo conjunto, el miembro del primer conjunto se incluye en el conjunto devuelto por esta función. También se incluyen los descendientes del primer conjunto que preceden a un miembro antecesor del segundo conjunto.  
  
 El primer conjunto puede contener tuplas en vez de miembros. La obtención de detalles de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en lugar de miembros.  
  
> [!IMPORTANT]  
>  Se reducirá el detalle de un miembro solo si va inmediatamente seguido por un elemento secundario o un descendiente. El orden de los miembros en el conjunto es importante para las\* familias de\* las funciones de obtención de detalles y drillup. Considere la posibilidad de usar la función **Hierarchy** para ordenar correctamente los miembros del primer conjunto.  
  
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
  
 El segundo ejemplo muestra la importancia del orden de los miembros. Dado que **DrillupMember** solo profundiza en los miembros que van seguidos inmediatamente de los descendientes del primer conjunto, no profundiza en el miembro de Canadá. Canadá está separada de sus descendientes por Estados Unidos y Colorado. Si vuelve a ordenar los miembros para que Canadá quede directamente encima de Alberta, Alberta y Brunswick se excluirán del conjunto de filas.  
  
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
  
 En el ejemplo 3 se muestra cómo el uso de la **jerarquía** puede mitigar los efectos del orden de los miembros y profundizar en el miembro de Canadá.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
