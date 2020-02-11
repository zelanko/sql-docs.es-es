---
title: Raíz (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: be687d5cbfd4fdbb706ef5c10778a4f3e3f93197
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037043"
---
# <a name="root-mdx"></a>Root (MDX)


  Devuelve una tupla que consta de **todos** los miembros de cada jerarquía de atributo dentro del ámbito actual de un cubo, una dimensión o una tupla. Para obtener más información sobre el ámbito, vea [instrucción scope &#40;MDX&#41;](../mdx/mdx-scripting-scope.md).  
  
> [!NOTE]  
>  Si una jerarquía de atributo no tiene un miembro **All** , la tupla contiene el miembro predeterminado de esa jerarquía.  
  
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
  
## <a name="remarks"></a>Observaciones  
 Si no se especifica un nombre de dimensión ni una expresión de tupla, la función **raíz** devuelve una tupla que contiene el miembro **All** (o el miembro predeterminado si el miembro **All** no existe) de cada jerarquía de atributo del cubo. El orden de los miembros de la tupla se basa en la secuencia en la que las jerarquías de atributo se definen en el cubo.  
  
 Si se especifica un nombre de dimensión, la función **raíz** devuelve una tupla que contiene el miembro **All** (o el miembro predeterminado si el miembro **All** no existe) de cada jerarquía de atributo de la dimensión especificada basándose en el contexto del miembro actual. El orden de los miembros de la tupla se basa en la secuencia en la que las jerarquías de atributo se definen en la dimensión.  
  
> [!NOTE]  
>  Si se especifica un nombre de jerarquía, la función de **tupla** seleccionará el nombre de la dimensión en el nombre de la jerarquía especificado.  
  
 Si se especifica una expresión de tupla, la función **raíz** devuelve una tupla que contiene la intersección de la tupla especificada y **todos** los miembros de todos los demás atributos de dimensión no se incluyen explícitamente en la tupla especificada.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve la tupla que contiene el miembro **All** (o el valor predeterminado si el miembro **All** no existe) de cada jerarquía del cubo Adventure Works.  
  
```  
SELECT Root()ON 0  
FROM [Adventure Works]  
```  
  
 En el ejemplo siguiente se devuelve la tupla que contiene el miembro **All** (o el valor predeterminado si el miembro **All** no existe) de cada jerarquía de la dimensión Date del cubo Adventure Works y el valor para el miembro especificado de la dimensión Measures que forma una intersección con estos miembros predeterminados.  
  
```  
SELECT Root([Date]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
 En el ejemplo siguiente se devuelve la tupla que contiene el miembro de tupla especificado (1 de julio de 2001, junto con el miembro **All** (o el valor predeterminado si el miembro **All** no existe) de cada una de las jerarquías no especificadas en la dimensión Date, el cubo Adventure Works y el valor para el miembro especificado de la dimensión Measures que forma una intersección con estos miembros.  
  
```  
SELECT Root([Date].[July 1, 2001]) ON 0  
FROM [Adventure Works]  
WHERE [Measures].[Order Count]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
