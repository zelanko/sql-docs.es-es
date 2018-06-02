---
title: Propiedades (MDX) | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b564d11696999ec2dbd778d15a3e881cab415259
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34581137"
---
# <a name="properties-mdx"></a>Properties (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve una cadena, o un valor con tipos muy marcados, que contiene un valor de propiedad de miembro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Member_Expression.Properties(Property_Name [, TYPED])  
```  
  
## <a name="arguments"></a>Argumentos  
 *Expresión_miembro*  
 Expresión MDX válida que devuelve un miembro.  
  
 *Property_name*  
 Expresión de cadena válida de un nombre de propiedad de miembro.  
  
## <a name="remarks"></a>Notas  
 El **propiedades** función devuelve el valor del miembro especificado para la propiedad de miembro especificado. La propiedad de miembro puede ser cualquiera de las propiedades de miembro intrínsecas, como **nombre**, **identificador**, **clave**, o **título**, o puede ser una propiedad de miembro definidas por el usuario. Para obtener más información, consulte [propiedades de miembro intrínsecas &#40;MDX&#41; ](../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md) y [propiedades de miembro definidas por el usuario &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 De forma predeterminada, se fuerza al valor a ser una cadena. Si **TYPED** se especifica, el valor devuelto está fuertemente tipado.  
  
-   Si el tipo de propiedad es intrínseco, la función devuelve el tipo original del miembro.  
  
-   Si el tipo de propiedad es definido por el usuario, el tipo del valor devuelto es el mismo que el tipo del valor devuelto de la **MemberValue** función.  
  
> [!NOTE]  
>  Properties ('Key') devuelve el mismo resultado que Key0, a excepción de las claves compuestas. Properties ('Key') devolverá un valor NULL para las claves compuestas. Utilice la tecla*x* sintaxis para las claves compuestas, como se ilustra en el ejemplo. Properties('Key0'), Properties('Key1'), Properties('Key2') y así sucesivamente forman en conjunto la clave compuesta.  
  
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
  
 En el ejemplo siguiente se muestra el uso de la clave*x* propiedad.  
  
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
 [Mediante las propiedades de miembro &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
