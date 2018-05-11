---
title: Cubo celdas (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00e22780b1313ee08345f26ad77f9eabe8ad18cb
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="cube-cells-analysis-services---multidimensional-data"></a>Celdas de cubos (Analysis Services - Datos multidimensionales)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un cubo se compone de celdas organizadas por grupos de medida y dimensiones. Una celda representa la intersección lógica única de un miembro de cada dimensión del cubo en el mismo. Por ejemplo, el cubo que se describe en el siguiente diagrama contiene un grupo de medida con dos medidas, organizadas en tres dimensiones llamadas Source, Route y Time.  
  
 ![Diagrama de cubo que se identifica una sola celda](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro5.gif "diagrama de cubo que se identifica una sola celda")  
  
 La celda sombreada única del diagrama es la intersección de los siguientes miembros:  
  
-   El miembro air de la dimensión Route.  
  
-   El miembro Africa de la dimensión Source.  
  
-   El miembro 4th quarter de la dimensión Time.  
  
-   La medida Packages.  
  
## <a name="leaf-and-nonleaf-cells"></a>Celdas hoja y no hoja  
 El valor de una celda en un cubo se puede obtener de varias formas. En el ejemplo anterior, el valor de la celda puede recuperará directamente de la tabla de hechos del cubo, ya que todos los miembros que se usa para identificar la celda son *miembros hoja*. Un miembro hoja no tiene miembros secundarios, jerárquicamente hablando, y normalmente hace referencia a un solo registro de una tabla de dimensiones. Este tipo de celda se conoce como un *celda hoja*.  
  
 Sin embargo, una celda también puede identificarse mediante el uso de *miembros no hoja*. Un miembro no hoja es un miembro que tiene uno o más miembros secundarios. En este caso, el valor de la celda se deriva normalmente de la agregación de miembros secundarios asociados al miembro no hoja. Por ejemplo, la intersección de los siguientes miembros y dimensiones hace referencia a una celda cuyo valor suministra la agregación:  
  
-   El miembro air de la dimensión Route.  
  
-   El miembro Africa de la dimensión Source.  
  
-   El miembro 2nd half de la dimensión Time.  
  
-   El miembro Packages.  
  
 El miembro 2nd half de la dimensión Time es un miembro no hoja. Por lo tanto, todos los valores asociados a él deben ser valores agregados, como se muestra en el siguiente diagrama.  
  
 ![las celdas de 3rd y 4th quarter para el miembro 2nd half](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro6.gif "las celdas de 3rd y 4th quarter para el miembro 2nd half")  
  
 Si consideramos que las agregaciones de los miembros 3rd quarter y 4th quarter son sumas, el valor de la celda especificada es 400, que es el total de todas las celdas hoja sombreadas del diagrama anterior. Dado que el valor de la celda se deriva de la agregación de otras celdas, la celda especificada se considera un *celda no hoja*.  
  
 Los valores de celdas derivados para miembros que utilizan grupos de miembros y resúmenes personalizados, además de miembros personalizados, se controlan de la misma manera. Sin embargo, los valores de celdas derivados para miembros calculados se basan totalmente en la expresión MDX (Expresiones multidimensionales) utilizada para definir el miembro calculado; en algunos casos, puede que no intervenga ningún dato de celda real. Para obtener más información, consulte [operadores de resúmenes personalizados en dimensiones de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension-attributes-custom-rollup-operators.md), [definir fórmulas de miembro personalizado](../../analysis-services/multidimensional-models/attribute-properties-define-custom-member-formulas.md), y [cálculos](../../analysis-services/multidimensional-models-olap-logical-cube-objects/calculations.md).  
  
## <a name="empty-cells"></a>Celdas vacías  
 No es necesario que todas las celdas de un cubo contengan un valor; puede haber intersecciones del cubo sin datos. Estas intersecciones, denominadas celdas vacías, se dan con frecuencia en los cubos debido a que no todas las intersecciones de un atributo de dimensión con una medida de un cubo contienen un registro correspondiente en una tabla de hechos. La proporción de celdas vacías en un cubo para el número total de celdas de un cubo se denomina a menudo la *dispersión* de un cubo.  
  
 Por ejemplo, la estructura del cubo que aparece en el siguiente diagrama es parecida a otros ejemplos de este tema. Sin embargo, en este ejemplo, no existían embarques aéreos a Africa en el tercer trimestre (3rd quarter) o a Australia en el cuarto (4th quarter). No existen datos en la tabla de hechos que admitan las intersecciones de estas dimensiones y medidas, por lo que las celdas de estas intersecciones están vacías.  
  
 ![Diagrama de cubo identifican celdas vacías](../../analysis-services/multidimensional-models-olap-logical-cube-objects/media/as-cubeintro7.gif "diagrama de cubo identifican celdas vacías")  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una celda vacía es una celda con características especiales. Como las celdas vacías pueden sesgar los resultados de combinaciones cruzadas, recuentos, etc. muchas funciones de MDX proporcionan la capacidad de omitir las celdas vacías para los cálculos. Para obtener más información, consulte [expresiones multidimensionales &#40;MDX&#41; referencia](../../mdx/multidimensional-expressions-mdx-reference.md), y [conceptos clave de MDX &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md).  
  
## <a name="security"></a>Seguridad  
 El acceso a los datos de las celdas se administra en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el nivel de rol y se puede controlar con precisión mediante el uso de expresiones MDX. Para obtener más información, consulte [conceder acceso personalizado a los datos de la dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md), y [conceder acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de cubos &#40;Analysis Services - datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)   
 [Las agregaciones y diseños de agregaciones](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)  
  
  
