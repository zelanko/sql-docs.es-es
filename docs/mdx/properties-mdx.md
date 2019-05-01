---
title: Propiedades (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c29d9b29078d6097b512acb93ff47eef018592c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63278451"
---
# <a name="properties-mdx"></a>Properties (MDX)


  Devuelve una cadena, o un valor con tipos muy marcados, que contiene un valor de propiedad de miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Expression*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Property_Name*  
 Expresión de cadena válida de un nombre de propiedad de miembro.  
  
## <a name="remarks"></a>Comentarios  
 El **propiedades** función devuelve el valor del miembro especificado para la propiedad de miembro especificado. La propiedad de miembro puede ser cualquiera de las propiedades de miembro intrínsecas, como **nombre**, **ID**, **clave**, o **título**, o puede ser un propiedad de miembro definidas por el usuario. Para obtener más información, consulte [propiedades de miembro intrínsecas &#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) y [las propiedades de miembro definidas por el usuario &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 De forma predeterminada, se fuerza al valor a ser una cadena. Si **TYPED** se especifica, el valor devuelto está fuertemente tipado.  
  
-   Si el tipo de propiedad es intrínseco, la función devuelve el tipo original del miembro.  
  
-   Si el tipo de propiedad es definido por el usuario, el tipo del valor devuelto es el mismo que el tipo de valor devuelto de la **MemberValue** función.  
  
> [!NOTE]  
>  Properties ('Key') devuelve el mismo resultado que Key0, a excepción de las claves compuestas. Properties ('Key') devolverá un valor NULL para las claves compuestas. Utilice la tecla*x* sintaxis para las claves compuestas, como se muestra en el ejemplo. Properties('Key0'), Properties('Key1'), Properties('Key2') y así sucesivamente forman en conjunto la clave compuesta.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve propiedades de miembro intrínsecas y definidas por el usuario mediante el argumento TYPED para devolver el valor con tipos muy marcados de la propiedad de miembro Day Name.  
  
```  
WITH MEMBER Measures.MemberName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Name')  
MEMBER Measures.MemberVal AS   
   [Date].[Calendar].[July 1, 2003].Properties('Member_Value')  
MEMBER Measures.MemberKey AS   
   [Date].[Calendar].[July 1, 2003].Properties('Key')  
MEMBER Measures.MemberID AS   
   [Date].[Calendar].[July 1, 2003].Properties('ID')  
MEMBER Measures.MemberCaption AS   
   [Date].[Calendar].[July 1, 2003].Properties('Caption')  
MEMBER Measures.DayName AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name', TYPED)  
MEMBER Measures.DayNameTyped AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day Name')  
MEMBER Measures.DayofWeek AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Week')  
MEMBER Measures.DayofMonth AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Month')  
MEMBER Measures.DayofYear AS   
   [Date].[Calendar].[July 1, 2003].Properties('Day of Year')  
  
SELECT {Measures.MemberName  
   , Measures.MemberVal  
   , Measures.MemberKey  
   , Measures.MemberID  
   , Measures.MemberCaption  
   , Measures.DayName  
   , Measures.DayNameTyped  
   , Measures.DayofWeek  
   , Measures.DayofMonth  
   , Measures.DayofYear  
   }  ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente muestra el uso de la clave*x* propiedad.  
  
```  
WITH   
MEMBER Measures.MemberKey AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key')  
MEMBER Measures.MemberKey0 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key0')  
MEMBER Measures.MemberKey1 AS   
   [Customer].[Customer Geography].[State-Province].&[QLD]&[AU].Properties('Key1')  
  
SELECT {Measures.MemberKey  
   , Measures.MemberKey0  
   , Measures.MemberKey1     
   }  ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar las propiedades de miembro &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
