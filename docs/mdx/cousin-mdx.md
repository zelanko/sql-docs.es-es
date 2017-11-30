---
title: Cousin (MDX) | Documentos de Microsoft
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
f1_keywords: COUSIN
dev_langs: kbMDX
helpviewer_keywords: Cousin function
ms.assetid: 9a416685-d35d-4d9c-a9f6-4574cbe59aea
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fee1f82f0ed706a2ce75eedcb0968f007a0037c3
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="cousin-mdx"></a>Cousin (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el miembro secundario con la misma posición relativa bajo un miembro primario que el miembro secundario especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Ancestor_Member_Expression*  
 Expresión de miembro MDX válida que devuelve un miembro antecesor.  
  
## <a name="remarks"></a>Comentarios  
 Esta función actúa sobre el orden y la posición de los miembros dentro de los niveles. Si existen dos jerarquías y la primera tiene cuatro niveles mientras que la segunda tiene cinco, el elemento Cousin del tercer nivel de la primera jerarquía es el tercer nivel de la segunda jerarquía.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente recupera el elemento Cousin del cuarto trimestre del año fiscal 2002, de acuerdo con su antecesor en el nivel de año del año fiscal 2003. El elemento Cousin recuperado es el cuarto trimestre del año fiscal 2003.  
  
```  
SELECT Cousin   
   ( [Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002],  
     [Date].[Fiscal].[FY 2003]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente recupera el elemento Cousin del mes de julio del año fiscal 2002, de acuerdo con su antecesor en el nivel de trimestre del segundo trimestre del año fiscal 2004. El elemento Cousin recuperado es el mes de octubre de 2003.  
  
```  
SELECT Cousin   
   ([Date].[Fiscal].[Month].[July 2002] ,  
    [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2004]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
