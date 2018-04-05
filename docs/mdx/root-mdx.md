---
title: Raíz (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- Root
dev_langs:
- kbMDX
helpviewer_keywords:
- Root function
ms.assetid: f6c42e87-5a52-4e43-9dd1-ca757f2db79c
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 16e6fb8fb10816391a25d71a717cff5f4c7abe58
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="root-mdx"></a>Root (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve una tupla que consta de la **todos los** miembros de cada jerarquía de atributo dentro del ámbito actual en un cubo, dimensión o tupla. Para obtener más información acerca del ámbito, consulte [instrucción SCOPE &#40; MDX &#41; ](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Si una jerarquía de atributo no tiene un **todos los** miembros, la tupla contiene el miembro predeterminado de esa jerarquía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cube syntax  
Root ()  
Dimension syntax  
Root( Dimension_Name )  
Tuple syntax  
Root( Tuple_Expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Name*  
 Expresión de cadena válida que especifica un nombre de dimensión.  
  
 *Tuple_Expression*  
 Expresión MDX válida que devuelve una tupla.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica un nombre de la dimensión ni una expresión de tupla, la **raíz** función devuelve una tupla que contiene el **todos los** miembro (o el miembro predeterminado si el **todos los** miembro no existe) de cada jerarquía de atributo del cubo. El orden de los miembros de la tupla se basa en la secuencia en la que las jerarquías de atributo se definen en el cubo.  
  
 Si se especifica un nombre de dimensión, el **raíz** función devuelve una tupla que contiene el **todos los** miembro (o el miembro predeterminado si el **todos los** miembro no existe) de cada jerarquía de atributo en la dimensión especificada en función del contexto del miembro actual. El orden de los miembros de la tupla se basa en la secuencia en la que las jerarquías de atributo se definen en la dimensión.  
  
> [!NOTE]  
>  Si se especifica un nombre de jerarquía, el **tupla** función seleccionará el nombre de la dimensión de la jerarquía especificada.  
  
 Si se especifica una expresión de tupla, la **raíz** función devuelve una tupla que contiene la intersección de la tupla especificada y la **todos los** miembros de todos los demás atributos de dimensión no incluidos explícitamente en la tupla especificada.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve la tupla que contiene el **todos los** miembro (o el valor predeterminado si el **todos los** miembro no existe) de cada jerarquía del cubo Adventure Works.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 El ejemplo siguiente devuelve la tupla que contiene el **todos los** miembro (o el valor predeterminado si el **todos los** miembro no existe) de cada jerarquía de la dimensión Date en el cubo de Adventure Works y el valor para el miembro especificado de la dimensión de medidas que forma intersección con estos miembros predeterminados.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 El ejemplo siguiente devuelve la tupla que contiene el miembro de la tupla especificada (del 1 de julio de 2001, junto con el **todos los** miembro (o el valor predeterminado si el **todos los** miembro no existe) de cada jerarquía no especificada de la fecha de dimensión de cubo de Adventure Works y el valor para el miembro especificado de la dimensión de medidas que forma intersección con estos miembros.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
