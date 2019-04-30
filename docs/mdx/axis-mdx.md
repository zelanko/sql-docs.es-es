---
title: Eje (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2802422f7d50c0a504a0c42eec940d81e89e66b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181648"
---
# <a name="axis-mdx"></a>Axis (MDX)


  Devuelve el conjunto de tuplas en un eje especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Axis_Number*  
 Expresión numérica válida que especifica el número de eje.  
  
## <a name="remarks"></a>Comentarios  
 El **eje** función utiliza la posición de base cero de un eje para devolver el conjunto de tuplas en un eje. Por ejemplo, `Axis(0)` devuelve el eje COLUMNS,  `Axis(1)` devuelve el eje ROWS, y así sucesivamente. El **eje** función no se puede usar en el eje del filtro. Esta función puede utilizarse para hacer que los miembros calculados dependan del contexto de la consulta que se está ejecutando. Por ejemplo, podría necesitar un miembro calculado que proporcione la suma solamente de los miembros seleccionados en el eje de filas. También puede utilizarse para hacer que la definición de un eje dependa de la definición de otro. Por ejemplo, ordenando el contenido del eje de filas según el valor del primer elemento del eje de columnas.  
  
> [!NOTE]  
>  Un eje solamente puede hacer referencia a un eje anterior. Por ejemplo, `Axis(0)` debe aparecer después de que se haya evaluado el eje COLUMNS, como en los ejes ROW o PAGE.  
  
## <a name="examples"></a>Ejemplos  
 La consulta de ejemplo siguiente muestra el modo de usar la función Axis:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SETTOSTR(AXIS(1))`  
  
 `SELECT MEASURES.AXISDEMO ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 En el ejemplo siguiente se muestra el uso de la función Axis dentro de un miembro calculado:  
  
 `WITH MEMBER MEASURES.AXISDEMO AS`  
  
 `SUM(AXIS(1), [Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.AXISDEMO} ON 0,`  
  
 `{[Date].[Calendar Year].&[2003], [Date].[Calendar Year].&[2004]} ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
