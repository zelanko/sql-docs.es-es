---
title: StrToMember (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c76d6e1e7ffe9bc40d785952b5c456ab1fc6fa
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743054"
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)


  Devuelve el miembro especificado por una cadena con formato de Expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Member_Name*  
 Expresión de cadena válida que especifica, directa o indirectamente, un miembro.  
  
## <a name="remarks"></a>Notas  
 El **StrToMember** función devuelve el miembro especificado en la expresión de cadena. El **StrToMember** función normalmente se utiliza con funciones definidas por el usuario para devolver una especificación de miembro de una función externa a una instrucción MDX, o cuando se parametriza una consulta MDX.  
  
-   Cuando se utiliza la marca CONSTRAINED, el nombre del miembro debe resolverse directamente en un nombre de miembro calificado o no calificado. Esta marca se utiliza para reducir el riesgo de ataques por inyección de código a través de la cadena especificada. Si se proporciona una cadena que no se resuelve directamente en un nombre de miembro calificado o no calificado, aparece el siguiente error: "Se han infringido las restricciones impuestas por la marca CONSTRAINED en la función STRTOMEMBER."  
  
-   Cuando no se utiliza la marca CONSTRAINED, el miembro especificado puede resolverse directamente en un nombre de miembro o en una expresión MDX que se resuelve en un nombre.  
  
-   Para entender mejor las diferencias entre los conjuntos y los miembros, vea Usar expresiones de conjuntos y Usar expresiones de miembros.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve la medida Reseller Sales Amount del miembro Bayern de la jerarquía de atributo State-Province mediante la **StrToMember** función. La cadena especificada proporcionó el nombre de miembro calificado.  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 En el ejemplo siguiente se devuelve la medida Reseller Sales Amount del miembro Bayern mediante la **StrToMember** función. Dado que la cadena de nombre de miembro proporcionó únicamente un nombre de miembro no calificado, la consulta devuelve la primera instancia del miembro especificado, que se encuentra en la jerarquía Customer Geography de la dimensión Customer, que no forma intersección con Reseller Sales. Las prácticas recomendadas indican que para garantizar los resultados esperados, se debe especificar el nombre calificado.  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 En el ejemplo siguiente se devuelve la medida Reseller Sales Amount del miembro Bayern de la jerarquía de atributo State-Province mediante la **StrToMember** función. La cadena de nombre de miembro proporcionada se resuelve en un nombre de miembro calificado.  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve un error debido a la marca CONSTRAINED. Mientras que la cadena de nombre de miembro proporcionada contiene una expresión de miembro MDX válida que se resuelve en un nombre de miembro calificado, la marca CONSTRAINED requiere nombres de miembro calificados o no calificados en la cadena de nombre de miembro.  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
