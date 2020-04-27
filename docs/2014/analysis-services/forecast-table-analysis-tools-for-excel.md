---
title: Previsión (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- forecasting
- mining model, time series
- time series [data mining]
ms.assetid: 22bb0b5e-78f5-484e-883d-2b5985a12749
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc620811209d854af5a9c874956847236819f462
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081047"
---
# <a name="forecast-table-analysis-tools-for-excel"></a>Pronóstico (Herramientas de análisis de tabla para Excel)
  ![Botón Pronóstico, cinta de opciones Herramientas de análisis de tabla](media/tat-forecast.gif "Botón Pronóstico, cinta de opciones Herramientas de análisis de tabla")  
  
 La herramienta **previsión** le ayuda a realizar predicciones basadas en los datos de una tabla de datos de Excel u otro origen de datos y, opcionalmente, puede ver las probabilidades asociadas a cada valor de predicción. Por ejemplo, si los datos contienen una columna de fecha y otra que muestra las ventas totales de cada día del mes, se podrían predecir las ventas de los días siguientes. También puede especificar el número de predicciones que hay que realizar. Por ejemplo, puede predecir las ventas de cinco días o de treinta.  
  
 Una vez que se completa la herramienta, anexa las nuevas predicciones al final de la tabla de datos de origen y resalta los valores nuevos. Los nuevos valores de serie temporal no se anexan; esto permite revisar las predicciones en primer lugar.  
  
 La herramienta también crea una nueva hoja de cálculo denominada **Informe de previsión**. En ella se informa sobre si el asistente ha creado una predicción correctamente. También incluye un gráfico de líneas que muestra las tendencias históricas.  
  
 Cuando se amplía la serie temporal para incluir las nuevas predicciones, los valores de predicción se agregan al gráfico de líneas. Los valores históricos aparecen como una línea continua, mientras que las predicciones están representadas por una línea de puntos.  
  
## <a name="using-the-forecast-tool"></a>Usar la herramienta Pronóstico  
  
1.  Abra una tabla de Excel que contenga datos numéricos predecibles.  
  
2.  Haga clic en **previsión** en la pestaña **analizar** .  
  
3.  Especifique las columnas que desea pronosticar. La herramienta selecciona automáticamente las columnas de los datos que tienen un tipo de datos predecible, es decir, datos numéricos continuos. Es posible que la herramienta no seleccione algunas columnas que tienen datos numéricos continuos si esas columnas contienen muchos valores NULL o valores cero, ya que los datos ausentes pueden afectar a los resultados. Si esto ocurre, puede corregir los datos mediante la herramienta cambiar [etiquetas &#40;SQL Server complementos de minería de datos&#41;](relabel-sql-server-data-mining-add-ins.md) .  
  
4.  Especifique la columna que contiene la fecha, hora u otro identificador de serie. Si selecciona la opción ** \<sin marca de tiempo>** la herramienta creará una serie basada en la secuencia de filas en los datos de origen.  
  
5.  Especifique el número de predicciones que se deben realizar.  
  
6.  Opcionalmente, proporcione una sugerencia al algoritmo sobre si espera que los datos se repitan de forma semanal, mensual o en otros períodos. Si los datos no se ajustan a ninguno de los patrones especificados, o si no está al tanto de los patrones, seleccione ** \<detectar automáticamente>** para que la herramienta busque los períodos de tiempo de repetición.  
  
7.  El asistente agrega las predicciones a la tabla de origen y crea un informe de pronóstico en una nueva hoja de cálculo.  
  
8.  Para agregar los nuevos valores al gráfico de predicción, amplíe la serie temporal para que incluya los valores pronosticados.  
  
### <a name="requirements"></a>Requisitos  
 Las columnas que se predicen deben contener datos numéricos continuos, como valores de moneda u otros números.  
  
 Si es posible, los datos también deben incluir una columna que contenga una serie de fechas o de horas. Puede usar una serie numérica (1, 2, 3...) en lugar de datos de fecha y hora. No obstante, los valores de la columna de serie deben ser únicos. Se produce un error si la herramienta de **previsión** encuentra valores duplicados en la columna de la serie.  
  
 No se puede predecir una fecha mediante la herramienta de **previsión** . Aunque es posible que no se produzca ningún error, este algoritmo no está diseñado para usar fechas como valores de predicción.  
  
### <a name="understanding-time-stamps"></a>Descripción de las marcas de tiempo  
 Debe identificar la columna que se va a usar como *marca de tiempo*. La marca de tiempo cumple dos objetivos. En primer lugar, identifica de forma única un valor en una serie temporal. Por ejemplo, si está realizando un seguimiento de las ventas diarias, debería tener solo un valor de ventas para cada día. La fecha de calendario se puede usar como marca de tiempo. En segundo lugar, la columna de marca de tiempo indica la unidad para las predicciones. Si está realizando el seguimiento de las ventas diarias, las predicciones también estarán en unidades de días.  
  
 Si los datos no incluyen ninguna columna de fecha u hora, la herramienta creará automáticamente una clave de serie temporal denominada _RowIndex. La clave se basará en el orden de las filas del conjunto de datos.  
  
 Cuando especifique el número de predicciones, escriba un número entero que indique el número de pasos. Las unidades de estos pasos dependen de las unidades usadas en las series de hora y fecha de los datos. Si los datos presentan resultados de ventas por meses, se predecirá una serie de meses. No puede cambiar las unidades de tiempo a menos que cambie los datos de origen.  
  
### <a name="understanding-periodicity"></a>Descripción de la periodicidad  
 Un pronóstico se basa en la repetición de patrones durante un período de tiempo. Por consiguiente, el algoritmo de serie temporal de Microsoft realiza cálculos para determinar los períodos de tiempo que tienen los patrones más determinantes. La *periodicidad* hace referencia a estos períodos de tiempo.  
  
 Una serie temporal puede contener muchos patrones potenciales. Si está seguro de que los datos contienen un cierto patrón, quizá pueda mejorar la calidad de la predicción proporcionando una sugerencia al algoritmo.  
  
 Por ejemplo, si espera que los datos se repitan semanalmente, puede seleccionar Semanal para indicar que el algoritmo debe buscar patrones semanales. Sin embargo, si no se encuentra ningún patrón semanal determinante, el algoritmo omitirá la sugerencia.  
  
## <a name="understanding-the-forecasting-report"></a>Descripción del informe de pronóstico  
 En este gráfico, los valores históricos de la tabla de datos aparecen como una línea oscura. Los valores de predicción aparecen como líneas de puntos. Puede hacer clic en un punto de la línea para ver el valor pronosticado.  
  
> [!NOTE]  
>  Si no ve las etiquetas en el eje de tiempo para los valores de predicción en el gráfico, abra la hoja de cálculo que contiene los valores de predicción y use la función **Fill, series** de Excel para extender la columna de marca de tiempo para incluir los valores de predicción.  
  
 En algunos casos, es posible que el pronóstico no tenga tantos intervalos de tiempo como se había solicitado. Eso suele significar que los datos eran insuficientes para permitir que el algoritmo pronosticara un futuro tan lejano. La herramienta **previsión** solo realizará predicciones que cumplan un umbral de probabilidad mínimo.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 El Cliente de minería de datos para Excel, que es un complemento independiente que proporciona funciones más avanzadas de minería de datos, también incluye un asistente para pronóstico.  
  
 Tanto la herramienta **previsión** (en las herramientas de análisis de tabla para Excel) como el Asistente para **previsión** (en el cliente de minería de datos [!INCLUDE[msCoName](../includes/msconame-md.md)] para Excel) utilizan el algoritmo de serie temporal.  
  
-   La herramienta de **previsión** es más fácil de usar porque configura automáticamente el algoritmo para usar la configuración más adecuada para los datos.  
  
-   El Asistente para **pronóstico** del cliente de minería de datos para Excel le proporciona la capacidad de personalizar los parámetros.  
  
 Para obtener más información acerca del Asistente para **previsión** , vea [asistente para previsión &#40;complementos de minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md). Para obtener más información acerca del algoritmo usado para el pronóstico, vea el tema "Algoritmo de serie temporal de Microsoft" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)  
  
  
