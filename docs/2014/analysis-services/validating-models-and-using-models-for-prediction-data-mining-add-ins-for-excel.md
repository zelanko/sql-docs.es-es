---
title: Validar modelos y usar modelos para la predicción (complementos de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97268dac1fef029bc35ff702ace0d422ee296d65
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66065496"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>Validar modelos y usar modelos para la predicción (Complementos de minería de datos para Excel)
  La prueba y validación de un modelo constituye un paso importante en el proceso de minería de datos. Antes de implementar los modelos de minería de datos en un entorno de producción, debe saber cómo se comportan con datos reales.  
  
 Los Complementos de minería de datos incluyen herramientas que le ayudan a probar los modelos generados, así como a crear predicciones y recomendaciones utilizando estos.  
  
## <a name="accuracy-chart"></a>Gráfico de precisión  
 El Asistente para **gráfico de precisión** le ayuda a crear una consulta de predicción y evaluar el rendimiento de un modelo de minería de datos mediante la creación de un gráfico de elevación o de dispersión. El gráfico de elevación permite distinguir entre los modelos de una estructura que son prácticamente idénticos y determinar cuál ofrece las mejores predicciones.  
  
 [Gráfico de precisión &#40;SQL Server complementos de minería de datos&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>Matriz de clasificación  
 El Asistente para **matriz de clasificación** le ayuda a crear una consulta de predicción para evaluar el rendimiento de un modelo de clasificación. El resultado es un gráfico que resume las predicciones precisas e imprecisas realizadas por el modelo. La matriz es una herramienta valiosa porque no sólo muestra la frecuencia con que el modelo predice un valor correctamente, sino que también muestra qué valores predice el modelo incorrectamente con más frecuencia.  
  
 [Matriz de clasificación &#40;SQL Server complementos de minería de datos&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>Gráfico de beneficios  
 El Asistente para **gráfico de beneficios** le ayuda a sopesar las ventajas de usar un modelo de minería de datos y evaluar los costos de falsos positivos y falsos negativos.  
  
 Este tipo de gráfico mide la precisión de la predicción del modelo e incorpora los costos unitarios y totales que especifique.  
  
 [Gráfico de beneficios &#40;SQL Server complementos de minería de datos&#41;](profit-chart-sql-server-data-mining-add-ins.md).  
  
## <a name="cross-validation"></a>Validación cruzada  
 La validación cruzada es una técnica establecida en la comunidad de la minería de datos para evaluar la validez de un conjunto de datos y la precisión de un modelo de minería de datos en dicho conjunto de datos. Divide un conjunto de datos en subconjuntos y, a continuación, va creando, entrenando y probando modelos de forma iterativa en cada subconjunto.  
  
 El Asistente para la **validación cruzada** le permite especificar el número de plegamientos por los que dividir los datos y, a continuación, proporciona un informe de validación cruzada que describe estadísticamente las diferencias entre estas secciones transversales. Con esta información, puede determinar si el modelo funciona bien con todos los datos de entrenamiento, o si está sesgado hacia un subconjunto determinado.  
  
 [&#40;de validación cruzada SQL Server complementos de minería de datos&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>Asistente para consultas  
 El Asistente para **consultas** es una herramienta interactiva que le ayuda a generar una consulta de predicción. Las consultas son la forma de generar recomendaciones, pronósticos futuros, etc.  
  
 En el Asistente para **consultas** , elija un modelo y, a continuación, proporcione datos de entrada, como valores únicos o desde una tabla o un rango, y el asistente le ayudará a seleccionar las columnas que se van a mostrar. También puede agregar funciones a la consulta para generar puntuaciones de probabilidad y otras estadísticas útiles.  
  
 [&#40;de consultas SQL Server complementos de minería de datos&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>Editor de consultas avanzadas  
 El **Editor de consultas avanzadas** es un conjunto interactivo de cuadros de diálogo que le ayuda a crear todo tipo de instrucciones DMX, desde ejecutar consultas personalizadas hasta crear y entrenar nuevos modelos, eliminar modelos o crear nuevos conjuntos de datos.  
  
 [Editor de consultas avanzadas de minería de datos](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>Consulte también  
 [Explorar y limpiar datos](exploring-and-cleaning-data.md)   
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Implementar y escalar modelos de minería de datos &#40;complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
