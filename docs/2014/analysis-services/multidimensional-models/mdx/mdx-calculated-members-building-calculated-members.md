---
title: Creación de miembros calculados en MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0275a071c5548de7086844e48cec7eff3bb72d31
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074538"
---
# <a name="building-calculated-members-in-mdx-mdx"></a>Generar miembros calculados en MDX (MDX)
  En las Expresiones multidimensionales (MDX), un miembro calculado es un miembro que se resuelve calculando una expresión MDX para devolver un valor. Esta definición tan genérica tiene un alcance notable. La capacidad de construir y utilizar miembros calculados en una consulta MDX proporciona una gran solución para manipular datos multidimensionales.  
  
 Puede crear miembros calculados en cualquier punto de una jerarquía. También puede crear miembros calculados que no dependan únicamente de los miembros existentes en un cubo, sino también de otros miembros calculados definidos en la misma expresión MDX.  
  
 Puede definir un miembro calculado para que tenga uno de los contextos siguientes:  
  
-   **Ámbito de consulta** Para crear un miembro calculado definido como parte de una consulta MDX, y en consecuencia con un ámbito limitado a la consulta, debe usar la palabra clave WITH. Posteriormente puede utilizar el miembro calculado en una instrucción MDX SELECT. De esta manera, el miembro calculado creado con la palabra clave WITH se puede cambiar sin tener que tocar la instrucción SELECT.  
  
     Para obtener más información sobre el uso de la palabra clave WITH para crear miembros calculados, vea [Crear miembros calculados en el ámbito de consulta &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md).  
  
-   **Ámbito de sesión** Para crear un miembro calculado cuyo ámbito sea más amplio que el contexto de la consulta, es decir, un ámbito que sea la duración de la sesión MDX, debe usar la instrucción CREATE MEMBER. Un miembro calculado definido por la utilización de la instrucción CREATE SET está disponible para todas las consultas de MDX de esa sesión. La instrucción CREATE MEMBER tiene sentido, por ejemplo, en una aplicación cliente que reutilice el mismo conjunto de un modo coherente en varias consultas diferentes.  
  
     Para obtener más información sobre el uso de la instrucción CREATE MEMBER para crear miembros calculados en una sesión, vea [Crear miembros calculados de ámbito de sesión &#40;MDX&#41;](mdx-calculated-members-session-scoped-calculated-members.md).  
  
## <a name="see-also"></a>Vea también  
 [CREATE MEMBER &#40;instrucción MDX&#41;](/sql/mdx/mdx-data-definition-create-member)   
 [Referencia de funciones MDX &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)   
 [SELECT &#40;Instrucción, MDX&#41;](/sql/mdx/mdx-data-manipulation-select)  
  
  
