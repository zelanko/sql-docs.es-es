---
title: ToggleDrillState (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 58acac77e4826855997791476b0602699452b7b8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228076"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


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
 El **ToggleDrillState** función cambia el estado de detalle de cada miembro del segundo conjunto que se encuentra en el primer conjunto. El primer conjunto puede contener tuplas con cualquier dimensionalidad, pero el segundo conjunto debe contener miembros de una sola dimensión. El **ToggleDrillState** función es una combinación de la **DrillupMember** y **DrilldownMember** funciones. Si el miembro, *m*del segundo conjunto está presente en el primer conjunto y se aumenta el detalle de ese miembro (es decir, tiene un descendiente que le sigue), a continuación, `DrillupMember(Set_Expression1, {m})` se aplica al miembro o tupla del primer conjunto. Si ese *m* se reducirá el detalle de miembros (es decir, no hay ningún descendiente del *m* que sigue inmediatamente a *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` se aplica al primer conjunto.  
  
 Si el elemento opcional **RECURSIVA** marca se utiliza, resumir y explorar en profundidad se aplican de forma recursiva. Para obtener más información acerca de la marca recursiva, vea el [DrillupMember](../mdx/drillupmember-mdx.md) y [DrilldownMember](../mdx/drilldownmember-mdx.md) funciones.  
  
 Consultar la propiedad XMLA MdpropMdxDrillFunctions le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones de obtención de detalles; consulte [propiedades XMLA compatibles &#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) para obtener más información.  
  
 Consulte [diario de la base de datos: Funciones de conjunto MDX: La función ToggleDrillState()](https://go.microsoft.com/fwlink/?LinkId=517759) para escenarios y ejemplos que utilizan esta función.  
  
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
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
