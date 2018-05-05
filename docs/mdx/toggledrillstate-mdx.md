---
title: ToggleDrillState (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TOGGLEDRILLSTATE
dev_langs:
- kbMDX
helpviewer_keywords:
- ToggleDrillState function
ms.assetid: 26fa1a0d-3ed1-45dc-955d-0591d49e4db9
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 718b2039b8f2451e145ab9109f4fb9d0743c2693
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Alterna el estado de detalle de los miembros entre modos de obtención de detalles y resumen.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Recursiva*  
 (Opcional). Palabra clave que indica comparación recursiva de conjuntos. El **ToggleDrillState** función es una combinación de la **DrillupMember** y **DrilldownMember** funciones. Recursividad solo se aplica cuando el miembro está en el **DrilldownMember** estado.  
  
 *Include_calc_members*  
 (Opcional). Marca que indica si se deben incluir en el nivel de detalle los miembros calculados, si existen.  
  
## <a name="remarks"></a>Comentarios  
 El **ToggleDrillState** función alterna el estado de detalle de cada miembro del segundo conjunto que está presente en el primer conjunto. El primer conjunto puede contener tuplas con cualquier dimensionalidad, pero el segundo conjunto debe contener miembros de una sola dimensión. El **ToggleDrillState** función es una combinación de la **DrillupMember** y **DrilldownMember** funciones. Si el miembro *m*, del segundo conjunto está presente en el primer conjunto y se aumenta el detalle de ese miembro (es decir, tiene un descendiente que le sigue), a continuación, `DrillupMember(Set_Expression1, {m})` se aplica al miembro o tupla del primer conjunto. Si ese *m* miembro se reduce el detalle (es decir, no hay ningún descendiente del *m* que sigue inmediatamente a *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` se aplica al primer conjunto.  
  
 Si la parte opcional **RECURSIVA** marca se utiliza, resumir y explorar en profundidad se aplican de forma recursiva. Para obtener más información acerca de la marca recursiva, consulte el [DrillupMember](../mdx/drillupmember-mdx.md) y [DrilldownMember](../mdx/drilldownmember-mdx.md) funciones.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones obtener detalles. vea [admite propiedades XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) para obtener más información.  
  
 Vea [diario de base de datos: funciones de conjunto MDX: la función ToggleDrillState()](http://go.microsoft.com/fwlink/?LinkId=517759) para escenarios y ejemplos que utilizan esta función.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente aumenta el detalle del miembro Australia del primer conjunto y reduce el detalle del miembro United States del primer conjunto.  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
