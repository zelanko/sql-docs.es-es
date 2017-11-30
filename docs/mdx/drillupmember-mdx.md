---
title: DrillupMember (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: DRILLUPMEMBER
dev_langs: kbMDX
helpviewer_keywords: DrillupMember function
ms.assetid: debcd966-ea4e-4ecf-8600-0a4d346d03f8
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 9238f765f2dac6f892baffee15f473674fe5e8a7
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="drillupmember-mdx"></a>DrillupMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 El **DrillupMember** función devuelve un conjunto de miembros basado en los miembros especificados en el primer conjunto que son descendientes de miembros en el segundo conjunto. El primer conjunto puede tener varias dimensiones, pero el segundo conjunto debe contener un conjunto de una dimensión. Se mantiene el orden entre los miembros originales del primer conjunto. La función crea el conjunto mediante la inclusión únicamente de los miembros del primer conjunto que son descendientes inmediatos de miembros del segundo conjunto. Si el antecesor inmediato de un miembro del primer conjunto no se encuentra en el segundo conjunto, el miembro del primer conjunto se incluye en el conjunto devuelto por esta función. También se incluyen los descendientes del primer conjunto que preceden a un miembro antecesor del segundo conjunto.  
  
 El primer conjunto puede contener tuplas en vez de miembros. Obtención de detalles de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en vez de miembros.  
  
> [!IMPORTANT]  
>  Se reducirá el detalle de un miembro solo si va inmediatamente seguido por un elemento secundario o un descendiente. Es importante el orden de los miembros del conjunto para la obtención de detalles\* y Drillup\* familias de funciones. Considere el uso de la **Hierarchize** función para ordenar adecuadamente los miembros del primer conjunto.  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
