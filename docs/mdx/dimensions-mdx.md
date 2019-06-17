---
title: Dimensiones (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2703122b67debf0749abcd2ea01114fb6ecaa06
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63248145"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  Devuelve una jerarquía especificada mediante una expresión numérica o de cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>Argumentos  
 *Hierarchy_Number*  
 Expresión numérica válida que especifica un número de jerarquía.  
  
 *Hierarchy_Name*  
 Expresión de cadena válida que especifica un nombre de jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica un número de jerarquía, el **dimensiones** función devuelve una jerarquía cuya posición de base cero dentro del cubo es especifica el número de jerarquía.  
  
 Si se especifica un nombre de jerarquía, el **dimensiones** función devuelve la jerarquía especificada. Normalmente, se utiliza esta versión de cadena de la **dimensiones** función con funciones definidas por el usuario.  
  
> [!NOTE]  
>  El **medidas** dimensión se representa siempre por `Dimensions(0)`.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes usan la **dimensiones** función para devolver el nombre, el número de niveles y el recuento de miembros de una jerarquía especificada, mediante una expresión numérica y una expresión de cadena.  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
