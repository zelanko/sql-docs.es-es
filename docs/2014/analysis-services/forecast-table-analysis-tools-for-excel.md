---
title: Pronóstico (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 623f3a4724de84dbb1e355ffbd64a6868ea0f12a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731876"
---
# <a name="forecast-table-analysis-tools-for-excel"></a>Pronóstico (Herramientas de análisis de tabla para Excel)
  ![Cinta de opciones de herramientas de botón de previsión de análisis de tabla](media/tat-forecast.gif "botón pronóstico en la cinta de opciones de herramientas de análisis de tabla")  
  
 El **previsión** herramienta le ayuda a realizar predicciones basadas en datos de una tabla de datos de Excel u otro origen de datos y, opcionalmente, ver las probabilidades asociadas a cada valor de predicción. Por ejemplo, si los datos contienen una columna de fecha y otra que muestra las ventas totales de cada día del mes, se podrían predecir las ventas de los días siguientes. También puede especificar el número de predicciones que hay que realizar. Por ejemplo, puede predecir las ventas de cinco días o de treinta.  
  
 Una vez que se completa la herramienta, anexa las nuevas predicciones al final de la tabla de datos de origen y resalta los valores nuevos. Los nuevos valores de serie temporal no se anexan; esto permite revisar las predicciones en primer lugar.  
  
 La herramienta también crea una nueva hoja de cálculo denominada **informe de pronóstico**. En ella se informa sobre si el asistente ha creado una predicción correctamente. También incluye un gráfico de líneas que muestra las tendencias históricas.  
  
 Cuando se amplía la serie temporal para incluir las nuevas predicciones, los valores de predicción se agregan al gráfico de líneas. Los valores históricos aparecen como una línea continua, mientras que las predicciones están representadas por una línea de puntos.  
  
## <a name="using-the-forecast-tool"></a>Usar la herramienta Pronóstico  
  
1.  Abra una tabla de Excel que contenga datos numéricos predecibles.  
  
2.  Haga clic en **previsión** en el **analizar** ficha.  
  
3.  Especifique las columnas que desea pronosticar. La herramienta selecciona automáticamente las columnas de los datos que tienen un tipo de datos predecible: es decir, datos numéricos continuos. Es posible que la herramienta no seleccione algunas columnas que tienen datos numéricos continuos si esas columnas contienen muchos valores NULL o valores cero, ya que los datos ausentes pueden afectar a los resultados. Si esto ocurre, puede corregir los datos usando el [cambiar etiquetas &#40;complementos de minería de datos de SQL Server&#41; ](relabel-sql-server-data-mining-add-ins.md) herramienta.  
  
4.  Especifique la columna que contiene la fecha, hora u otro identificador de serie. Si selecciona la opción  **\<sin marca de tiempo >** la herramienta creará una serie basada en la secuencia de filas en el origen de datos.  
  
5.  Especifique el número de predicciones que se deben realizar.  
  
6.  Opcionalmente, proporcione una sugerencia al algoritmo sobre si espera que los datos se repitan de forma semanal, mensual o en otros períodos. Si los datos no se ajusta a cualquiera de los patrones especificados, o si es consciente de los patrones, seleccione  **\<detectar automáticamente >** para que la herramienta busque los períodos de tiempo de repetición.  
  
7.  El asistente agrega las predicciones a la tabla de origen y crea un informe de pronóstico en una nueva hoja de cálculo.  
  
8.  Para agregar los nuevos valores al gráfico de predicción, amplíe la serie temporal para que incluya los valores pronosticados.  
  
### <a name="requirements"></a>Requisitos  
 Las columnas que se predicen deben contener datos numéricos continuos, como valores de moneda u otros números.  
  
 Si es posible, los datos también deben incluir una columna que contenga una serie de fechas o de horas. Puede usar una serie numérica (1,2,3...) en lugar de los datos de fecha y hora. No obstante, los valores de la columna de serie deben ser únicos. Se produce un error si el **previsión** herramienta descubre valores duplicados en la columna de serie.  
  
 No se puede predecir una fecha mediante el uso de la **previsión** herramienta. Aunque es posible que no se produzca ningún error, este algoritmo no está diseñado para usar fechas como valores de predicción.  
  
### <a name="understanding-time-stamps"></a>Descripción de las marcas de tiempo  
 Debe identificar una columna que se usará como un *marca de tiempo*. La marca de tiempo cumple dos objetivos. En primer lugar, identifica de forma única un valor en una serie temporal. Por ejemplo, si está realizando un seguimiento de las ventas diarias, debería tener solo un valor de ventas para cada día. La fecha de calendario se puede usar como marca de tiempo. En segundo lugar, la columna de marca de tiempo indica la unidad para las predicciones. Si está realizando el seguimiento de las ventas diarias, las predicciones también estarán en unidades de días.  
  
 Si los datos no incluyen ninguna columna de fecha u hora, la herramienta creará automáticamente una clave de serie temporal denominada _RowIndex. La clave se basará en el orden de las filas del conjunto de datos.  
  
 Cuando especifique el número de predicciones, escriba un número entero que indique el número de pasos. Las unidades de estos pasos dependen de las unidades usadas en las series de hora y fecha de los datos. Si los datos presentan resultados de ventas por meses, se predecirá una serie de meses. No puede cambiar las unidades de tiempo a menos que cambie los datos de origen.  
  
### <a name="understanding-periodicity"></a>Descripción de la periodicidad  
 Un pronóstico se basa en la repetición de patrones durante un período de tiempo. Por consiguiente, el algoritmo de serie temporal de Microsoft realiza cálculos para determinar los períodos de tiempo que tienen los patrones más determinantes. *Periodicidad* hace referencia a estos períodos de tiempo.  
  
 Una serie temporal puede contener muchos patrones potenciales. Si está seguro de que los datos contienen un cierto patrón, quizá pueda mejorar la calidad de la predicción proporcionando una sugerencia al algoritmo.  
  
 Por ejemplo, si espera que los datos se repitan semanalmente, puede seleccionar Semanal para indicar que el algoritmo debe buscar patrones semanales. Sin embargo, si no se encuentra ningún patrón semanal determinante, el algoritmo omitirá la sugerencia.  
  
## <a name="understanding-the-forecasting-report"></a>Descripción del informe de pronóstico  
 En este gráfico, los valores históricos de la tabla de datos aparecen como una línea oscura. Los valores de predicción aparecen como líneas de puntos. Puede hacer clic en un punto de la línea para ver el valor pronosticado.  
  
> [!NOTE]  
>  Si no ve las etiquetas en el eje de tiempo para los valores previstos en el gráfico, abra la hoja de cálculo que contiene los valores de predicción y utilice el **rellenar, Series** función de Excel para extender la columna de marca de tiempo para incluir la predicción valores.  
  
 En algunos casos, es posible que el pronóstico no tenga tantos intervalos de tiempo como se había solicitado. Eso suele significar que los datos eran insuficientes para permitir que el algoritmo pronosticara un futuro tan lejano. El **previsión** herramienta sólo realizará predicciones que cumplen un umbral de probabilidad mínima.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 El Cliente de minería de datos para Excel, que es un complemento independiente que proporciona funciones más avanzadas de minería de datos, también incluye un asistente para pronóstico.  
  
 Tanto el **previsión** herramienta (en las herramientas de análisis de tabla para Excel) y el **previsión** uso del asistente (en el cliente de minería de datos para Excel) el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de serie temporal.  
  
-   El **previsión** herramienta es más fácil de usar porque se configura automáticamente el algoritmo para usar la configuración más adecuada para sus datos.  
  
-   El **previsión** asistente en el cliente de minería de datos para Excel le da la capacidad para personalizar los parámetros.  
  
 Para obtener más información sobre la **previsión** asistente, consulte [Asistente para pronóstico &#40;complementos minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md). Para obtener más información acerca del algoritmo usado para el pronóstico, vea el tema "Algoritmo de serie temporal de Microsoft" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tablas para Excel](table-analysis-tools-for-excel.md)  
  
  
