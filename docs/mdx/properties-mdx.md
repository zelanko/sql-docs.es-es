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
ms.openlocfilehash: 9a9aa2ab3fbfdbe10246e0dcf8758cfcf7732375
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68893674"
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
  
## <a name="remarks"></a>Observaciones  
 La función **Properties** devuelve el valor del miembro especificado para la propiedad de miembro especificada. La propiedad de miembro puede ser cualquiera de las propiedades de miembro intrínsecas, como nombre, **identificador**, **clave**o **título**, o puede ser una propiedad de miembro definida por **el**usuario. Para obtener más información, vea [propiedades de miembro intrínsecas &#40;&#41;MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) y [propiedades de miembro definidas por el usuario &#40;MDX&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties).  
  
 De forma predeterminada, se fuerza al valor a ser una cadena. Si se especifica **Typed** , el valor devuelto es fuertemente tipado.  
  
-   Si el tipo de propiedad es intrínseco, la función devuelve el tipo original del miembro.  
  
-   Si el tipo de propiedad es definido por el usuario, el tipo del valor devuelto es el mismo que el tipo del valor devuelto de la función **MemberValue** .  
  
> [!NOTE]  
>  Properties ('Key') devuelve el mismo resultado que Key0, a excepción de las claves compuestas. Properties ('Key') devolverá un valor NULL para las claves compuestas. Use la sintaxis Key*x* para las claves compuestas, como se muestra en el ejemplo. Properties('Key0'), Properties('Key1'), Properties('Key2') y así sucesivamente forman en conjunto la clave compuesta.  
  
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
  
 En el ejemplo siguiente se muestra el uso de la propiedad KEY*x* .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Usar las propiedades de miembro &#40;&#41;MDX](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-member-properties)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
