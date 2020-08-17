---
description: Leaves (MDX)
title: Hojas (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7beab859a2953b3eba52e74d97bed5718c59ea90
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387311"
---
# <a name="leaves-mdx"></a>Leaves (MDX)


  Devuelve un conjunto compuesto de todos los atributos (opcionalmente limitado a los que pertenecen a una dimensión específica). Para cada atributo X del conjunto recuperado, si X es el atributo de granularidad o está directa o indirectamente relacionado con este atributo, la granularidad se establece en el atributo X sin influir en el segmento. La función **Leaves** está diseñada para su uso dentro de una instrucción Scope o en el lado izquierdo de una asignación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Leaves( [ Dimension_expression ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Dimension_Expression*  
 Expresión MDX válida que devuelve una dimensión.  
  
## <a name="remarks"></a>Observaciones  
 Los miembros hoja son tuplas formadas por la combinación cruzada del nivel inferior de todas las jerarquías de atributo. Se excluyen los miembros calculados.  
  
-   Si se especifica un nombre de dimensión, la función **Leaves** devuelve un conjunto que contiene los miembros hoja del atributo clave de la dimensión especificada.  
  
-   Si la dimensión está asociada a varios grupos de medida, se utiliza el de la medida del ámbito actual.  
  
-   Si no se especifica un nombre de dimensión, la función devuelve un conjunto que contiene los miembros hoja de todo el cubo.  
  
    > [!NOTE]  
    >  Si la expresión de dimensión se resuelve en una jerarquía y el nombre único de la jerarquía es igual al nombre único de la dimensión (propiedad de dimensión de cubo HierarchyUniqueNameStyle=ExcludeDimensionName y nombre de la jerarquía=nombre de la dimensión), se utiliza la dimensión.  
  
    > [!IMPORTANT]  
    >  Se genera un error si no todos los atributos tienen la misma granularidad en los grupos de medida del ámbito actual.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones MDX &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
