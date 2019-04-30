---
title: Cuadro de diálogo Propiedades del eje, opciones del eje (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 553d1d4e2be366cc56ed37caad6a9db20850e856
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239345"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>Cuadro de diálogo Propiedades del eje, Opciones del eje (Generador de informes y SSRS)
  Seleccione **opciones del eje** en el **Horizontal** o **propiedades del eje vertical** cuadro de diálogo para definir la apariencia del eje del gráfico especificado. En versiones anteriores de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], el gráfico mostraba todas las etiquetas en el eje X de forma predeterminada. Sin embargo, en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008, el gráfico omite las etiquetas para generar una imagen más limpia en el gráfico y evitar las colisiones entre etiquetas. Para más información, vea [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opciones  
 **Habilitar quiebres de escala**  
 Seleccione esta opción para habilitar la inclusión de quiebres de escala en el gráfico cuando sea necesario. Si está habilitada, el gráfico calculará automáticamente si existe una diferencia suficiente entre los puntos superior e inferior del conjunto de datos como para dibujar un quiebre de escala.  
  
 **Invertir dirección**  
 Seleccione esta opción para invertir la dirección del gráfico. Por ejemplo, de manera predeterminada, un gráfico de columnas muestra el eje Y a la izquierda y las categorías de izquierda a derecha. Si selecciona esta opción, el gráfico mostrará el eje Y a la derecha y las categorías de derecha a izquierda.  
  
 **Usar color de entrelazado**  
 Seleccione esta opción para agregar franjas al gráfico y, a continuación, seleccione un color o escriba una expresión. Las franjas son bandas sombreadas situadas en el área de gráfico que proporcionan un efecto de áreas claras que se alternan con áreas oscuras entre las líneas de cuadrícula. Estas franjas son útiles para resaltar patrones que se repiten en un eje.  
  
 **Incluir siempre el cero**  
 Seleccione esta opción para incluir siempre el cero en la escala del eje. Si esta opción no está habilitada, el gráfico no pondrá una etiqueta al valor cero en el eje. Los valores cero resultan útiles cuando el conjunto de datos incluye valores negativos o valores cero.  
  
 **Eje escalar**  
 Seleccione esta opción para mostrar un conjunto de valores de eje en una escala continua. Por ejemplo, si el conjunto de datos contiene datos de enero, marzo y noviembre, un eje no escalar mostraría solo esos meses, mientras que un eje escalar mostraría todos los meses del año.  
  
 **Usar escala logarítmica**  
 Seleccione esta opción para indicar que la escala del eje es logarítmica. Esta opción solo está disponible en el eje Y si el eje contiene valores numéricos positivos.  
  
 En el cuadro, escriba la base logarítmica que se usará cuando el eje se haya establecido para usar una escala logarítmica. De forma predeterminada, el gráfico usa una base de 10 para la escala logarítmica de un eje. Esta opción solo está disponible en el eje Y si el eje es numérico.  
  
 **Mínima**  
 Escriba una expresión o un valor para el valor mínimo del eje X. Si se omite, el valor mínimo se determina mediante los datos devueltos por el conjunto de datos.  
  
 **Máximo**  
 Escriba una expresión o un valor para el valor máximo del eje X. Si se omite, el valor máximo se determina mediante los datos devueltos por el conjunto de datos.  
  
 **Interval**  
 Escriba una expresión o un valor para el intervalo entre las etiquetas del eje. Por ejemplo, escriba 1 para mostrar cada etiqueta de categoría en el eje. Escriba 2 para mostrar una de cada dos etiquetas de categoría. Si se omite, las etiquetas se calculan automáticamente basándose en los valores del conjunto de datos.  
  
 **Tipo de intervalo**  
 Escriba una expresión o un valor para el tipo de intervalo del intervalo especificado. Por ejemplo, si desea que el intervalo sea de dos días, especificará **2** para el intervalo y **Días** para el tipo de intervalo.  
  
 **Márgenes laterales**  
 Escriba una expresión o seleccione un valor para agregar o quitar un margen entre los elementos del gráfico y los lados del gráfico. Si esta opción se establece en **Automático**, se agregan márgenes laterales.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [Aplicar formato a los colores de serie de un gráfico &#40;Generador de informes y SSRS&#41;](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Especificar un intervalo de eje &#40;Generador de informes y SSRS&#41;](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Aplicar formato de fecha o de moneda a las etiquetas de los ejes &#40;Generador de informes y SSRS&#41;](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Trazar datos en un eje secundario &#40;generador de informes y SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Agregar o quitar márgenes de un gráfico &#40;Generador de informes y SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  
