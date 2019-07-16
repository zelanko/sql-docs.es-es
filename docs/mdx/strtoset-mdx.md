---
title: StrToSet (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 729dae70fce03b3dec1394900126b216d09dc497
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036791"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  Devuelve el conjunto especificado por una cadena con formato de expresiones multidimensionales MDX.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Specification*  
 Expresión de cadena válida que especifica, directa o indirectamente, un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **StrToSet** función devuelve el conjunto especificado en la expresión de cadena. El **StrToSet** función normalmente se utiliza con funciones definidas por el usuario para devolver una especificación de conjunto desde una función externa a una instrucción MDX o cuando se parametriza una consulta MDX.  
  
-   Cuando se utiliza la marca CONSTRAINED, la especificación de conjunto debe contener nombres de miembro calificados u o un conjunto de tuplas que contiene los nombres de miembro calificados o no calificados entre llaves {}. Esta marca se utiliza para reducir el riesgo de ataques por inyección de código a través de la cadena especificada. Si no se proporciona una cadena no es nombres de miembros directamente resolverse en o no calificado, aparece el siguiente error: "Las restricciones impuestas por la CONSTRAINED se han infringido la marca en la función STRTOSET."  
  
-   Cuando no se utiliza la marca CONSTRAINED, la especificación de conjunto especificada se puede resolver en una expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
-   Para entender mejor las diferencias entre los conjuntos y los miembros, vea Usar expresiones de conjuntos y Usar expresiones de miembros.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve el conjunto de miembros de la jerarquía de atributo State-Province mediante la **StrToSet** función. La especificación de conjunto proporciona una expresión de conjunto MDX válida.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve un error debido a la marca CONSTRAINED. Mientras que la especificación de conjunto proporciona una expresión de conjunto MDX válida, la marca CONSTRAINED necesita nombres de miembro calificados o no calificados en la especificación de conjunto.  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 El ejemplo siguiente devuelve la medida Reseller Sales Amount para los países Germany y Canada. La especificación de conjunto proporcionada en la cadena especificada contiene nombres de miembro calificados, tal y como exige la marca CONSTRAINED.  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
