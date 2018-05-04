---
title: Deja (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LEAVES
dev_langs:
- kbMDX
helpviewer_keywords:
- Leaves function
ms.assetid: 09f908aa-1b2d-4af9-8c8d-c023915241b2
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: c9ac580c71d1c82876a41953d6f8b5411dc7dd55
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="leaves-mdx"></a>Leaves (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
 [Referencia de funciones MDX & #40; MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
