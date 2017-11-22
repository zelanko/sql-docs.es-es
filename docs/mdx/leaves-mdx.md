---
title: Deja (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: LEAVES
dev_langs: kbMDX
helpviewer_keywords: Leaves function
ms.assetid: 09f908aa-1b2d-4af9-8c8d-c023915241b2
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1920799f04128a692a333e80ac5024cbdbae564a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="leaves-mdx"></a>Leaves (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un conjunto compuesto de todos los atributos (opcionalmente limitado a los que pertenecen a una dimensión específica). Para cada atributo X del conjunto recuperado, si X es el atributo de granularidad o está directa o indirectamente relacionado con este atributo, la granularidad se establece en el atributo X sin influir en el segmento. El **deja** función está diseñada para su uso dentro de una instrucción SCOPE o en el lado izquierdo de una asignación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Expresión MDX válida que devuelve una dimensión.  
  
## <a name="remarks"></a>Comentarios  
 Los miembros hoja son tuplas formadas por la combinación cruzada del nivel inferior de todas las jerarquías de atributo. Se excluyen los miembros calculados.  
  
-   Si se especifica un nombre de dimensión, el **deja** función devuelve un conjunto que contiene los miembros hoja del atributo clave de la dimensión especificada.  
  
-   Si la dimensión está asociada a varios grupos de medida, se utiliza el de la medida del ámbito actual.  
  
-   Si no se especifica un nombre de dimensión, la función devuelve un conjunto que contiene los miembros hoja de todo el cubo.  
  
    > [!NOTE]  
    >  Si la expresión de dimensión se resuelve en una jerarquía y el nombre único de la jerarquía es igual al nombre único de la dimensión (propiedad de dimensión de cubo HierarchyUniqueNameStyle=ExcludeDimensionName y nombre de la jerarquía=nombre de la dimensión), se utiliza la dimensión.  
  
    > [!IMPORTANT]  
    >  Se genera un error si no todos los atributos tienen la misma granularidad en los grupos de medida del ámbito actual.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de funciones MDX &#40; MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
