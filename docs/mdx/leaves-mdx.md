---
title: Deja (MDX) | Documentos de Microsoft
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b18f283dce1ed5d0d3099dbdc26e27e8aff39ffc
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741254"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  Devuelve un conjunto compuesto de todos los atributos (opcionalmente limitado a los que pertenecen a una dimensión específica). Para cada atributo X del conjunto recuperado, si X es el atributo de granularidad o está directa o indirectamente relacionado con este atributo, la granularidad se establece en el atributo X sin influir en el segmento. El **deja** función está diseñada para su uso dentro de una instrucción SCOPE o en el lado izquierdo de una asignación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Expresión MDX válida que devuelve una dimensión.  
  
## <a name="remarks"></a>Notas  
 Los miembros hoja son tuplas formadas por la combinación cruzada del nivel inferior de todas las jerarquías de atributo. Se excluyen los miembros calculados.  
  
-   Si se especifica un nombre de dimensión, el **deja** función devuelve un conjunto que contiene los miembros hoja del atributo clave de la dimensión especificada.  
  
-   Si la dimensión está asociada a varios grupos de medida, se utiliza el de la medida del ámbito actual.  
  
-   Si no se especifica un nombre de dimensión, la función devuelve un conjunto que contiene los miembros hoja de todo el cubo.  
  
    > [!NOTE]  
    >  Si la expresión de dimensión se resuelve en una jerarquía y el nombre único de la jerarquía es igual al nombre único de la dimensión (propiedad de dimensión de cubo HierarchyUniqueNameStyle=ExcludeDimensionName y nombre de la jerarquía=nombre de la dimensión), se utiliza la dimensión.  
  
    > [!IMPORTANT]  
    >  Se genera un error si no todos los atributos tienen la misma granularidad en los grupos de medida del ámbito actual.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
