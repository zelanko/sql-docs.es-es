---
title: "Creación de miembros calculados en MDX (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: cbfe97ab13483ccaf31134bfa45ab5b583f797d7
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-calculated-members---building-calculated-members"></a>MDX calcula miembros - creación de miembros calculados
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
En las Expresiones multidimensionales (MDX), un miembro calculado es un miembro que se resuelve calculando una expresión MDX para devolver un valor. Esta definición tan genérica tiene un alcance notable. La capacidad de construir y utilizar miembros calculados en una consulta MDX proporciona una gran solución para manipular datos multidimensionales.  
  
 Puede crear miembros calculados en cualquier punto de una jerarquía. También puede crear miembros calculados que no dependan únicamente de los miembros existentes en un cubo, sino también de otros miembros calculados definidos en la misma expresión MDX.  
  
 Puede definir un miembro calculado para que tenga uno de los contextos siguientes:  
  
-   **Ámbito de consulta** Para crear un miembro calculado definido como parte de una consulta MDX, y en consecuencia con un ámbito limitado a la consulta, debe usar la palabra clave WITH. Posteriormente puede utilizar el miembro calculado en una instrucción MDX SELECT. De esta manera, el miembro calculado creado con la palabra clave WITH se puede cambiar sin tener que tocar la instrucción SELECT.  
  
     Para obtener más información sobre el uso de la palabra clave WITH para crear miembros calculados, vea [Crear miembros calculados en el ámbito de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Ámbito de sesión** Para crear un miembro calculado cuyo ámbito sea más amplio que el contexto de la consulta, es decir, un ámbito que sea la duración de la sesión MDX, debe usar la instrucción CREATE MEMBER. Un miembro calculado definido por la utilización de la instrucción CREATE SET está disponible para todas las consultas de MDX de esa sesión. La instrucción CREATE MEMBER tiene sentido, por ejemplo, en una aplicación cliente que reutilice el mismo conjunto de un modo coherente en varias consultas diferentes.  
  
     Para obtener más información sobre el uso de la instrucción CREATE MEMBER para crear miembros calculados en una sesión, vea [Crear miembros calculados de ámbito de sesión &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE MEMBER, instrucción &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-member.md)   
 [Referencia de funciones MDX &#40; MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)   
 [Instrucción SELECT &#40; MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
