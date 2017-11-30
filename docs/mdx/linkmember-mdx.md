---
title: LinkMember (MDX) | Documentos de Microsoft
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
f1_keywords: LINKMEMBER
dev_langs: kbMDX
helpviewer_keywords: LinkMember function
ms.assetid: b9106f07-8ea2-4933-aed3-ee9c63acf7ac
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a6fafec6febad45fe226bb9b96abd8c1ad3bd6da
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="linkmember-mdx"></a>LinkMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el miembro equivalente a un miembro especificado de una jerarquía especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LinkMember(Member_Expression, Hierarchy_Expression)   
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Hierarchy_Expression*  
 Expresión MDX válida que devuelve una jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 El **LinkMember** función devuelve el miembro de la jerarquía especificada que coincide con los valores de clave en cada nivel del miembro especificado en la jerarquía relacionada. Los atributos de cada nivel deben tener la misma cardinalidad de clave y tipo de datos. En las jerarquías no naturales, si existe más de una coincidencia para el valor clave de un atributo, el resultado será un error o indeterminado.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el **LinkMember** función para devolver la medida predeterminada del cubo de Adventure Works para los antecesores del miembro 1 de julio de 2002 de la jerarquía de atributo Date.Date de la jerarquía Calendar.  
  
```  
SELECT  Hierarchize  
   (Ascendants   
      (LinkMember   
         ([Date].[Date].[July 1, 2002], [Date].[Calendar]  
         )  
       )  
    ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Hierarchize &#40; MDX &#41;](../mdx/hierarchize-mdx.md)   
 [Ascendants &#40; MDX &#41;](../mdx/ascendants-mdx.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
