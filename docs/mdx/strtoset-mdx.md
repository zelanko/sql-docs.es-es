---
title: StrToSet (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: STRTOSET
dev_langs: kbMDX
helpviewer_keywords: StrToSet function
ms.assetid: 1700a563-6527-450a-8d3b-975c65bb6e51
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 98095d2d8910a9e69d74712b99e1ccc7954826ae
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el conjunto especificado por una cadena con formato de Expresiones multidimensionales (MDX).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Specification*  
 Expresión de cadena válida que especifica, directa o indirectamente, un conjunto.  
  
## <a name="remarks"></a>Comentarios  
 El **StrToSet** función devuelve el conjunto especificado en la expresión de cadena. El **StrToSet** función normalmente se utiliza con funciones definidas por el usuario para devolver una especificación de conjunto desde una función externa a una instrucción MDX, o cuando se parametriza una consulta MDX.  
  
-   Cuando se utiliza la marca CONSTRAINED, la especificación de conjunto debe contener nombres de miembro calificados o no calificados, o un conjunto de tuplas que contenga nombres de miembro calificados o no calificados entre llaves {}. Esta marca se utiliza para reducir el riesgo de ataques por inyección de código a través de la cadena especificada. Si se proporciona una cadena que no se resuelve directamente en nombres de miembro calificados o no calificados, aparece el siguiente error: "Se infringieron las restricciones impuestas por la marca CONSTRAINED en la función STRTOSET."  
  
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
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
