---
title: Con ejes de consulta y segmentador en un ejemplo Simple (MDX) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fce95d7e51c17f6e8a0fedbec01eccf7bd8ec8c4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-query-and-slicer-axes---using-axes-in-a-simple-example"></a>Consulta MDX y ejes de segmentación de datos - mediante ejes en un ejemplo Simple
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  En este sencillo ejemplo se ilustran los conceptos en los que se basa la especificación y el uso de los ejes de consulta y segmentador.  
  
## <a name="the-cube"></a>Cubo  
 Un cubo, denominado TestCube, tiene dos dimensiones simples: Route y Time. Cada dimensión solo tiene una jerarquía de usuario, denominadas Route y Time respectivamente. Puesto que las medidas del cubo son parte de la dimensión Measures, este cubo tiene tres dimensiones en total.  
  
## <a name="the-query"></a>Consulta  
 La consulta va a proporcionar una matriz en la que la medida Packages se puede comparar con rutas (routes) y tiempos (times).  
  
 En la siguiente consulta MDX de ejemplo, las jerarquías Route y Time se utilizan como ejes de la consulta y la dimensión Measures como eje segmentador. La función [Members](../../../mdx/members-set-mdx.md) indica que MDX usará los miembros de la jerarquía o el nivel para generar un conjunto. El uso de la función **Members** implica que no es necesario especificar explícitamente cada miembro de una jerarquía o un nivel específicos de una consulta MDX.  
  
```  
SELECT  
   { Route.nonground.Members } ON COLUMNS,  
   { Time.[1st half].Members } ON ROWS  
FROM TestCube  
WHERE ( [Measures].[Packages] )  
```  
  
## <a name="the-results"></a>Resultado  
 El resultado es una cuadrícula que identifica el valor de la medida Packages en cada intersección de las dimensiones de eje COLUMNS y ROWS. En la tabla siguiente se muestra el aspecto que tendría la cuadrícula.  
  
||air|sea|  
|-|---------|---------|  
|1st quarter|60|50|  
|2nd quarter|45|45|  
  
## <a name="see-also"></a>Vea también  
 [Especificar el contenido de un eje de consulta & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md)   
 [Especificar el contenido de un eje segmentador & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-slicer-axis.md)  
  
  
