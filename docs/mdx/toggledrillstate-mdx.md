---
description: ToggleDrillState (MDX)
title: ToggleDrillState (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: dd716e631adc3ded77f81278c20f754b28199b49
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192325"
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
 (Opcional). Palabra clave que indica comparación recursiva de conjuntos. La función **ToggleDrillState** es una combinación de las funciones **DrillupMember** y **DrilldownMember** . La recursividad solo se aplica cuando el miembro está en el estado de **DrilldownMember** .  
  
 *Include_calc_members*  
 (Opcional). Marca que indica si se deben incluir en el nivel de detalle los miembros calculados, si existen.  
  
## <a name="remarks"></a>Comentarios  
 La función **ToggleDrillState** alterna el estado de detalle de cada miembro del segundo conjunto que se encuentra en el primer conjunto. El primer conjunto puede contener tuplas con cualquier dimensionalidad, pero el segundo conjunto debe contener miembros de una sola dimensión. La función **ToggleDrillState** es una combinación de las funciones **DrillupMember** y **DrilldownMember** . Si el miembro, *m*, del segundo conjunto está presente en el primer conjunto y ese miembro se explora en profundidad (es decir, tiene un descendiente inmediatamente después), `DrillupMember(Set_Expression1, {m})` se aplica al miembro o tupla del primer conjunto. Si se aumenta el detalle de ese miembro *m* (es decir, no hay ningún descendiente de *m* que siga inmediatamente a *m*), `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` se aplica al primer conjunto.  
  
 Si se usa la marca **recursiva** opcional, la obtención de detalles y la exploración en profundidad se aplican de forma recursiva. Para obtener más información sobre la marca recursiva, vea las funciones [DrillupMember](../mdx/drillupmember-mdx.md) y [DrilldownMember](../mdx/drilldownmember-mdx.md) .  
  
 La consulta de la propiedad XMLA MdpropMdxDrillFunctions permite comprobar el nivel de compatibilidad que el servidor proporciona para las funciones de perforación. para más información, consulte [las propiedades XMLA compatibles &#40;&#41;XMLA ](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) .  
  
 Vea [diario de base de datos: funciones de conjunto MDX: la función ToggleDrillState ()](https://go.microsoft.com/fwlink/?LinkId=517759) para escenarios y ejemplos que implican esta función.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente aumenta el detalle del miembro Australia del primer conjunto y reduce el detalle del miembro Estados Unidos del primer conjunto.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
