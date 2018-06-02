---
title: DrilldownMember (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f50d68c383f758bfa75d8fd50964eaaf8c89fa4
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578067"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Aumenta el detalle de los miembros de un conjunto especificado presentes en un segundo conjunto especificado.  
  
 Alternativamente, la función detalla en un conjunto de tuplas usando la primera jerarquía de la tupla o la jerarquía especificada opcionalmente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression1*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Set_Expression2*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Target_Hierarchy*  
 Expresión MDX válida que devuelve una jerarquía.  
  
 *Recursiva*  
 Palabra clave que indica comparación recursiva de conjuntos.  
  
 *Include_Calc_Members*  
 Palabra clave para que los miembros calculados puedan estar incluidos en la obtención de detalles.  
  
## <a name="remarks"></a>Notas  
 Esta función devuelve un conjunto de miembros secundarios que están ordenados por jerarquía, e incluye los miembros especificados en el primer conjunto que también están presentes en el segundo conjunto. No se explorará en profundidad los miembros primarios si el primer conjunto contiene el miembro primario y uno o más miembros secundarios. El primer conjunto puede tener varias dimensiones, pero el segundo conjunto debe contener un conjunto de una dimensión. El orden se mantiene entre los miembros originales del primer conjunto, aunque todos los miembros secundarios incluidos en el conjunto de resultados de la función se incluyen inmediatamente bajo su miembro primario. La función crea el conjunto de resultados mediante la recuperación de los elementos secundarios de cada miembro del primer conjunto que también se encuentren en el segundo conjunto. Si **RECURSIVA** se especifica, la función continúa recursivamente compare establecen los miembros del conjunto con el segundo conjunto, recuperar los elementos secundarios de cada miembro en el resultado de resultados que esté también presente en el segundo conjunto hasta que no queden miembros del conjunto de resultados pueden encontrarse en el segundo conjunto.  
  
 Consultar la propiedad XMLA **MdpropMdxDrillFunctions** le permite comprobar el nivel de compatibilidad que proporciona el servidor para las funciones obtener detalles, consulte [admite propiedades XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)para obtener más información.  
  
 El primer conjunto puede contener tuplas en vez de miembros. El aumento del nivel de detalle de tupla es una extensión de OLE DB y devuelve un conjunto de tuplas en vez de miembros.  
  
> [!IMPORTANT]  
>  Se aumentará el detalle de un miembro solamente si va inmediatamente seguido de uno de sus elementos secundarios. Es importante el orden de los miembros del conjunto de obtención de detalles * y Drillup\* familias de funciones.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente aumenta el detalle de Australia, que es el miembro del primer conjunto que también está presente en el segundo conjunto.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 El ejemplo siguiente aumenta el detalle de Australia, que es el miembro del primer conjunto que también está presente en el segundo conjunto. No obstante, dado que el argumento RECURSIVE está presente, la función continúa comparando de forma recursiva los miembros del conjunto de resultados (miembros del nivel State-Province) con el segundo conjunto mediante la recuperación de los elementos secundarios de cada miembro del conjunto de resultados (miembros del nivel City) que estén también presentes en el segundo conjunto hasta que no queden miembros del conjunto de resultados en el segundo conjunto.  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
