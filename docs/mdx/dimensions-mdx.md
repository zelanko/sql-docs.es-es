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
ms.openlocfilehash: 84d5ab0caa22c6f35f3e7b790dbfb3348df8ceb1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67999967"
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
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un número de jerarquía, la función **Dimensions** devuelve una jerarquía cuya posición de base cero dentro del cubo es el número de jerarquía especificado.  
  
 Si se especifica un nombre de jerarquía, la función **Dimensions** devuelve la jerarquía especificada. Normalmente, se usa esta versión de cadena de la función **Dimensions** con funciones definidas por el usuario.  
  
> [!NOTE]  
>  La dimensión **Measures** siempre está representada por `Dimensions(0)`.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se usa la función **Dimensions** para devolver el nombre, el recuento de niveles y el recuento de miembros de una jerarquía especificada, utilizando una expresión numérica y una expresión de cadena.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
