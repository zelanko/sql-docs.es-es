---
title: SetToStr (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57e74eb1c7db4aebdd01fde8fc48a425d7affa55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149282"
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
  
## <a name="remarks"></a>Comentarios  
 Esta función se utiliza para transferir una representación de cadena de un conjunto a una función externa para su análisis. La cadena devuelta aparece encerrado entre llaves {}, con cada elemento en el conjunto de separados por comas.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente devuelve una cadena que contiene todos los miembros de la jerarquía de atributo Geography.Country.  
  
```  
WITH MEMBER Measures.x AS SetToStr (Geography.Geography.Children)  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
