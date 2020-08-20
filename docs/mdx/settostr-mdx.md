---
description: SetToStr (MDX)
title: SetToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0317de06f3d68388fac5be752d26e27f0d373a89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500448"
---
# <a name="settostr-mdx"></a>SetToStr (MDX)


  Devuelve una cadena con formato de Expresiones multidimensionales (MDX) que corresponde a un conjunto especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SetToStr(Set_Expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Expresión MDX (Expresiones multidimensionales) válida que devuelve un conjunto.  
  
## <a name="remarks"></a>Observaciones  
 Esta función se utiliza para transferir una representación de cadena de un conjunto a una función externa para su análisis. La cadena que se devuelve se incluye entre llaves {} , y cada elemento del conjunto está separado por una coma.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve una cadena que contiene todos los miembros de la jerarquía de atributo Geography.Country.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
