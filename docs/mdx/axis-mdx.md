---
title: Eje (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- AXIS
dev_langs:
- kbMDX
helpviewer_keywords:
- Axis function
ms.assetid: a3a60a1e-e266-4fa1-ae13-bae73544de33
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2503dcaa13db79acd5cff94c78ad365ee41b0b9b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="axis-mdx"></a>Axis (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el conjunto de tuplas en un eje especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Axis(Axis_Number)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Axis_Number*  
 Expresión numérica válida que especifica el número de eje.  
  
## <a name="remarks"></a>Comentarios  
 El **eje** función utiliza la posición de base cero de un eje para devolver el conjunto de tuplas en un eje. Por ejemplo, `Axis(0)` devuelve el eje COLUMNS,  `Axis(1)` devuelve el eje ROWS, y así sucesivamente. El **eje** no se puede usar la función en el eje del filtro. Esta función puede utilizarse para hacer que los miembros calculados dependan del contexto de la consulta que se está ejecutando. Por ejemplo, podría necesitar un miembro calculado que proporcione la suma solamente de los miembros seleccionados en el eje de filas. También puede utilizarse para hacer que la definición de un eje dependa de la definición de otro. Por ejemplo, ordenando el contenido del eje de filas según el valor del primer elemento del eje de columnas.  
  
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
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
