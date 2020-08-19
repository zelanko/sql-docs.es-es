---
description: DrillupLevel (MDX)
title: DrillupLevel (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cfdb8e77fcb92fe208e83f45c32a5c20c5d29615
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421909"
---
# <a name="drilluplevel-mdx"></a>DrillupLevel (MDX)


  Reduce el detalle de los miembros de un conjunto por debajo de un nivel especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DrillupLevel(Set_Expression [ , Level_Expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
 *Level_Expression*  
 Expresión MDX válida que devuelve un nivel.  
  
## <a name="remarks"></a>Observaciones  
 La función **DrillupLevel** devuelve un conjunto de miembros organizados jerárquicamente basándose en los miembros incluidos en el conjunto especificado. Se mantiene el orden entre los miembros del conjunto especificado.  
  
 Si se especifica una expresión de nivel, la función **DrillupLevel** crea el conjunto mediante la recuperación de solo los miembros que están por encima del nivel especificado. Si se especifica una expresión de nivel y no hay un miembro del nivel especificado representado en el conjunto especificado, se devuelve el conjunto especificado.  
  
 Si no se especifica una expresión de nivel, la función crea el conjunto mediante la recuperación de solo aquellos miembros que se encuentran un nivel por encima del nivel más bajo de la primera dimensión a la que se hace referencia en el conjunto especificado.  
  
## <a name="example"></a>Ejemplo  
 EL ejemplo siguiente devuelve el conjunto de miembros del primer conjunto que están por encima del nivel Subcategory.  
  
```  
SELECT DrillUpLevel   
  ({[Product].[Product Categories].[All Products]  
    ,[Product].[Product Categories].[Subcategory].&[32],  
    [Product].[Product Categories].[Product].&[215]},  
  [Product].[Product Categories].[Subcategory]  
    )  
  ON 0  
  FROM [Adventure Works]  
  WHERE [Measures].[Internet Order Quantity]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
