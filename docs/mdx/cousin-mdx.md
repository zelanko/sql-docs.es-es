---
title: Cousin (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad604900ac31cbcfb7e9a68fba4241c5f539b491
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63284977"
---
# <a name="cousin-mdx"></a>Cousin (MDX)


  Devuelve el miembro secundario con la misma posición relativa bajo un miembro primario que el miembro secundario especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cousin( Member_Expression , Ancestor_Member_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
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
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
