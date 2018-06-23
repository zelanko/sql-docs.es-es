---
title: Validar modelos y usar modelos de predicción (minería de datos a los complementos para Excel) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mining models, validating
- mining models, charting
- validation [data mining]
- mining models, testing
ms.assetid: e245ac1f-1230-48e9-9091-e70b131aa2a8
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c399f7db81923e51676066fa54e0ac79614a7ba2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104776"
---
# <a name="validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel"></a>Validar modelos y usar modelos para la predicción (Complementos de minería de datos para Excel)
  La prueba y validación de un modelo constituye un paso importante en el proceso de minería de datos. Antes de implementar los modelos de minería de datos en un entorno de producción, debe saber cómo se comportan con datos reales.  
  
 Los Complementos de minería de datos incluyen herramientas que le ayudan a probar los modelos generados, así como a crear predicciones y recomendaciones utilizando estos.  
  
## <a name="accuracy-chart"></a>Gráfico de precisión  
 El **gráfico de precisión de** asistente le ayudará a crear una consulta de predicción y evaluar el rendimiento de un modelo de minería de datos mediante la creación de un gráfico de elevación o un gráfico de dispersión. El gráfico de elevación permite distinguir entre los modelos de una estructura que son prácticamente idénticos y determinar cuál ofrece las mejores predicciones.  
  
 [Gráfico de precisión &#40;complementos de minería de datos de SQL Server&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
## <a name="classification-matrix"></a>Matriz de clasificación  
 El **matriz de clasificación** asistente le ayuda a crear una consulta de predicción para evaluar el rendimiento de un modelo de clasificación. El resultado es un gráfico que resume las predicciones precisas e imprecisas realizadas por el modelo. La matriz es una herramienta valiosa porque no sólo muestra la frecuencia con que el modelo predice un valor correctamente, sino que también muestra qué valores predice el modelo incorrectamente con más frecuencia.  
  
 [Matriz de clasificación &#40;complementos de minería de datos de SQL Server&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
## <a name="profit-chart"></a>Gráfico de beneficios  
 El **gráfico de beneficios** asistente le ayuda a sopesar las ventajas de utilizar un modelo de minería de datos y a evaluar los costos de falsos positivos y falsos negativos  
  
 Este tipo de gráfico mide la precisión de la predicción del modelo e incorpora los costos unitarios y totales que especifique.  
  
 [Gráfico de beneficios &#40;complementos de minería de datos de SQL Server&#41;](profit-chart-sql-server-data-mining-add-ins.md).  
  
## <a name="cross-validation"></a>Validación cruzada  
 La validación cruzada es una técnica establecida en la comunidad de la minería de datos para evaluar la validez de un conjunto de datos y la precisión de un modelo de minería de datos en dicho conjunto de datos. Divide un conjunto de datos en subconjuntos y, a continuación, va creando, entrenando y probando modelos de forma iterativa en cada subconjunto.  
  
 El **validación cruzada** asistente le permite especificar el número de subconjuntos para dividir los datos y, a continuación, proporciona un informe de validación cruzada que describe estadísticamente las diferencias entre estas secciones transversales. Con esta información, puede determinar si el modelo funciona bien con todos los datos de entrenamiento, o si está sesgado hacia un subconjunto determinado.  
  
 [La validación cruzada &#40;complementos de minería de datos de SQL Server&#41;](cross-validation-sql-server-data-mining-add-ins.md)  
  
## <a name="query-wizard"></a>Asistente para consultas  
 El **consulta** asistente es una herramienta interactiva que le ayuda a crear una consulta de predicción. Las consultas son la forma de generar recomendaciones, pronósticos futuros, etc.  
  
 En el **consulta** asistente, elija un modelo y, a continuación, proporcionar datos de entrada, como valores únicos o desde una tabla o un intervalo, y el asistente le ayuda a seleccionar columnas para la salida. También puede agregar funciones a la consulta para generar puntuaciones de probabilidad y otras estadísticas útiles.  
  
 [Consulta &#40;complementos de minería de datos de SQL Server&#41;](query-sql-server-data-mining-add-ins.md)  
  
## <a name="advanced-query-editor"></a>Editor de consultas avanzadas  
 El **Editor de consultas avanzadas** es un conjunto interactivo de cuadros de diálogo que le ayuda a generar todos los tipos de instrucciones de DMX, desde ejecutar consultas personalizadas para crear y entrenar modelos nuevos, eliminar modelos o crear nuevos datos establece.  
  
 [Editor de consultas de minería de datos avanzada](advanced-data-mining-query-editor.md)  
  
## <a name="see-also"></a>Vea también  
 [Exploración y limpieza de datos](exploring-and-cleaning-data.md)   
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Implementar y ampliar modelos de minería de datos &#40;datos complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  