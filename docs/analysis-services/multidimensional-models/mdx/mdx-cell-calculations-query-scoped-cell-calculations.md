---
title: "Creación de cálculos de celdas del ámbito de consulta (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
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
- WITH keyword
- query-scoped cell calculations [MDX]
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34ef680e855c0a6b29363923ba6984189a4e9119
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="mdx-cell-calculations---query-scoped-cell-calculations"></a>Cálculos de celdas MDX - cálculos de celdas del ámbito de consulta
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
La palabra clave **WITH** en las expresiones multidimensionales (MDX) se usa para describir las celdas calculadas en el contexto de una consulta. La palabra clave **WITH** tiene la siguiente sintaxis:  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 El valor `CellCalc_Identifier` es el nombre de las celdas calculadas. El valor `String_Expression` contiene una lista de expresiones de conjunto MDX ortogonales de una sola dimensión. Cada una de estas expresiones de conjunto debe dar como resultado una de las categorías que figuran en la siguiente tabla:  
  
|Categoría|Description|  
|--------------|-----------------|  
|Conjunto vacío|Una expresión de conjunto MDX que se resuelve en un conjunto vacío. En este caso, el ámbito de la celda calculada es todo el cubo.|  
|Conjunto de un solo miembro|Una expresión de conjunto MDX que se resuelve en un solo miembro.|  
|Conjunto de miembros de nivel|Una expresión de conjunto MDX que se resuelve en miembros de un solo nivel. Un ejemplo de este tipo de expresión de conjunto es la función MDX *Level_Expression*.**Members** . Para incluir los miembros calculados, use la función MDX *Level_Expression*.**AllMembers**. Para más información, vea [AllMembers &#40;MDX&#41;](../../../mdx/allmembers-mdx.md).|  
|Conjunto de descendientes|Una expresión de conjunto MDX que se resuelve en los descendientes de un miembro determinado. Un ejemplo de expresión de conjunto es la función MDX **Descendants**(*Member_Expression*, *Level_Expresion*, *Desc_Flag*). Para obtener más información, vea [Descendants &#40;MDX&#41;](../../../mdx/descendants-mdx.md).|  
  
 Si el argumento `String_Expression` no describe ninguna dimensión, MDX considera que se han incluido todos los miembros para generar el subcubo de cálculo. Por lo tanto, si el argumento `String_Expression` tiene el valor NULL, la definición de las celdas calculadas se aplica a todo el cubo.  
  
 El argumento `MDX_Expression` contiene una expresión MDX que se evalúa como un valor de celda para todas las celdas definidas en el argumento `String_Expression` .  
  
## <a name="additional-considerations"></a>Consideraciones adicionales  
 MDX procesa la condición de cálculo, especificada por la propiedad **CONDITION** solamente una vez. Este único procesamiento proporciona mayor rendimiento para la evaluación de varias definiciones de celdas calculadas, sobre todo con celdas calculadas superpuestas a través de pasos de cubo.  
  
 Este único procesamiento se lleva a cabo dependiendo del ámbito de creación establecido en la definición de las celdas calculadas:  
  
-   Si se crea en un ámbito global, como parte de un cubo, MDX procesa la condición de cálculo al mismo tiempo que el cubo. Si se modifican de alguna manera las celdas del cubo y se incluyen en el subcubo de cálculo de una definición de celdas calculadas, la condición de cálculo puede no ser precisa hasta que el cubo vuelva a procesarse. La modificación de las celdas puede producirse a partir de reescrituras, por ejemplo. La condición de cálculo se vuelve a procesar en el mismo momento que el cubo.  
  
-   Si se creó en un ámbito de sesión, MDX procesa la condición de cálculo cuando la instrucción se emite durante la sesión. Como en definiciones de celdas calculadas creadas globalmente, si se modifican las celdas, la condición de cálculo puede no ser precisa para la definición de celdas calculadas.  
  
-   Si se creó en un ámbito de consulta, MDX procesa la condición de cálculo cuando se ejecuta la consulta. Aquí también se aplica el tema de modificación de las celdas, aunque las cuestiones de latencia de datos son mínimas debido al bajo tiempo de proceso de la ejecución de la consulta MDX.  
  
 Por otro lado, MDX procesa la fórmula de cálculo siempre que se emite una consulta MDX en el cubo y ésta implica celdas incluidas en la definición de celdas calculadas. Este procesamiento se lleva a cabo independientemente del ámbito de creación.  
  
## <a name="see-also"></a>Vea también  
 [CREATE CELL CALCULATION instrucción &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-cell-calculation.md)  
  
  
