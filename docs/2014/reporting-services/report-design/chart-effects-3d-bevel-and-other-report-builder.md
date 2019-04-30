---
title: Aplicar 3D, bisel y otros efectos a un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10156"
ms.assetid: 18ef2119-2931-43ae-9078-f39b460462dd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 26fbda6dacd20b3ec02061b41a7e1de2f3b2d1ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185723"
---
# <a name="3d-bevel-and-other-effects-in-a-chart-report-builder-and-ssrs"></a>Aplicar 3D, bisel y otros efectos a un gráfico (Generador de informes y SSRS)
  Se pueden usar efectos tridimensionales (3D) para dar profundidad y agregar impacto visual a un gráfico. Por ejemplo, si desea resaltar un sector específico de un gráfico circular seccionado, puede girar y cambiar la perspectiva del gráfico para que los usuarios se fijen primero en dicho sector. Cuando se aplican efectos 3D al gráfico, se deshabilitan todos los colores de degradado y los estilos de sombreado.  
  
 Los efectos tridimensionales se pueden aplicar a gráficos individuales; además, en el mismo informe se pueden mostrar gráficos bidimensionales y tridimensionales.  
  
 Si quiere agregar efectos tridimensionales a un área de gráfico de cualquier tipo de gráfico, solo tiene que seleccionar **Habilitar 3D** en el cuadro de diálogo **Propiedades del área de gráfico**. Para obtener más información, vea [Agregar efectos 3D a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-add-3d-effects-report-builder.md).  
  
 Otra manera de agregar impacto visual a los gráficos es mediante la incorporación de estilos de bisel, relieve y textura a los gráficos de barras, de columnas, circulares y de anillos. Para más información, vea [Agregar estilos con bisel, relieve y textura a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="coordinate-based-three-dimensional-charts"></a>Gráficos tridimensionales basados en coordenadas  
 Cuando se trabaja con tipos de gráficos basados en coordenadas (de columnas, de barras, de áreas, de puntos, de líneas y de intervalos), los efectos tridimensionales muestran el gráfico con un tercer eje, conocido como el "eje Z". La introducción de este tercer eje permite aplicar una serie de mejoras visuales al gráfico.  
  
### <a name="changing-the-white-space-in-a-3d-chart"></a>Cambiar el espacio en blanco en un gráfico 3D  
 Cuando se muestra un gráfico de áreas en modo tridimensional, cada serie aparece en una fila independiente a lo largo del eje Z del gráfico. Para cambiar la separación que hay entre una serie y otra, modifique la profundidad de rango de punto; para ello, cambie la propiedad **Profundidad de rango de punto** en el cuadro de diálogo Efectos 3D.  
  
### <a name="changing-the-projection-of-a-3d-chart"></a>Cambiar la proyección de un gráfico 3D  
 Hay dos tipos de proyecciones 3D: oblicua y en perspectiva. Una proyección oblicua agrega una dimensión de profundidad a un gráfico bidimensional. El eje Z se dibuja formando ángulos iguales con los ejes horizontal y vertical, que siguen siendo perpendiculares entre sí como en un gráfico bidimensional.  
  
 En la proyección en perspectiva, se calcula un plano de vista y se vuelve a dibujar el gráfico como si se estuviera observando desde ese punto. El valor de **Giro** desplaza la vista verticalmente desde el "nivel del suelo", situado en la posición 0, hasta el punto de máxima elevación, en la posición 90. El valor de **Inclinación** desplaza el ángulo de visión hacia la izquierda o hacia la derecha. Un valor de 0 es equivalente a una vista bidimensional del gráfico. El valor de **Perspectiva** define el porcentaje de distorsión que se usará al mostrar la proyección. Este tipo de proyección mantiene las proporciones del gráfico, pero le da un aspecto deformado, por lo que resulta más eficaz usar un grado más bajo de perspectiva.  
  
> [!NOTE]  
>  Las proyecciones en perspectiva y oblicua son tipos de proyecciones independientes, de modo que no se puedan usar juntas en el mismo gráfico.  
  
### <a name="clustering-data"></a>Agrupar los datos en clústeres  
 En los gráficos 2D, las series de datos aparecen unas junto a las otras. Con el método de agrupación en clústeres, las series individuales se muestran en filas independientes en un gráfico 3D. Por ejemplo, si tiene un gráfico que contiene tres series de puntos de datos, con la agrupación en clústeres se mostrará cada una de las tres series en una fila independiente a lo largo del eje Z. De forma predeterminada, todos los tipos de gráficos mostrados en 3D se agrupan en clústeres.  
  
 La agrupación en clústeres se puede deshabilitar para los gráficos de barras y de columnas. Si se deshabilita la agrupación en clústeres y hay varias series de barras y de columnas, estas se muestran unas junto a las otras en una fila.  
  
## <a name="shape-based-three-dimensional-charts"></a>Gráficos tridimensionales basados en formas  
 Los tipos de gráficos basados en formas (circular, de anillos, de embudo y piramidal) disponen de menos efectos tridimensionales. Si trabaja con tipos de gráficos basados en formas, solo puede cambiar los valores de giro e inclinación.  
  
## <a name="rotations"></a>Giros  
 Los gráficos se pueden girar horizontal y verticalmente de -90 a 90 grados. Un ángulo horizontal positivo girará el gráfico en sentido contrario a las agujas del reloj alrededor del eje X, mientras que un ángulo vertical positivo girará el gráfico en el sentido de las agujas del reloj alrededor del eje Y.  
  
## <a name="highlighting-3d-effects"></a>Efectos 3D de resaltado  
 Puede agregar estilos de resaltado a un gráfico 3D mediante la propiedad **Shading** , que aparece debajo de Area3DStyle en el panel Propiedades cuando se selecciona el área del gráfico. Un estilo de iluminación simple aplica el mismo matiz a los elementos del área del gráfico. Un estilo realista cambia los matices de los elementos del área del gráfico que dependen de un ángulo de iluminación especificado.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Agregar efectos 3D a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-add-3d-effects-report-builder.md)  
  
  
