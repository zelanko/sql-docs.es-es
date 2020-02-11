---
title: Comparar las predicciones de los modelos de predicción (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ead8a1fe-60d8-4017-8fb8-6fe32168e46d
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 26cc445d3bad5c628628353d5c0c84ffa4755e97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63066344"
---
# <a name="comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial"></a>Comparar las predicciones de los modelos de predicción (Tutorial intermedio de minería de datos)
  En los pasos anteriores de este tutorial, ha creado varios modelos de serie temporal:  
  
-   Predicciones para cada combinación de región y modelo, basadas únicamente en los datos del modelo y región individual.  
  
-   Predicciones para cada región, en función de los datos actualizados.  
  
-   Predicciones para todos los modelos en un ámbito mundial, basadas en datos agregados.  
  
-   Predicciones para el modelo M200 de la región de Norteamérica, basadas en el modelo agregado.  
  
 Para resumir las características de las predicciones de serie temporal, también revisará los cambios para ver cómo ha afectado a los resultados de predicción el uso de las opciones para ampliar o reemplazar datos.  
  
 [EXTEND_MODEL_CASES](#bkmk_EXTEND)  
  
 [REPLACE_MODEL_CASES](#bkmk_REPLACE)  
  
##  <a name="bkmk_EXTEND"></a>Comparar los resultados originales con los resultados después de agregar datos  
 Echemos un vistazo a los datos de la línea de productos de M200 en la región del Pacífico para ver cómo afecta a los resultados la actualización del modelo con nuevos datos. Recuerde que la serie de datos original finalizó en junio de 2004 y que hemos obtenido datos nuevos para julio, agosto y septiembre.  
  
-   La primera columna muestra los datos nuevos que se han agregado.  
  
-   La segunda columna muestra la previsión para julio y los meses siguientes, basada en la serie de datos original.  
  
-   La tercera columna muestra el pronóstico basado en los datos extendidos.  
  
|**M200 Pacific**|Datos actualizados de ventas reales|Previsión antes de agregar datos|Predicción ampliada|  
|----------------------|-----------------------------|------------------------------------|-------------------------|  
|7-25-2008|**65**|32|**65**|  
|8-25-2008|**54**|37|**54**|  
|9-25-2008|**61**|32|**61**|  
|10-25-2008|No aparecen datos|36|32|  
|11-25-2008|No aparecen datos|31|41|  
|12-25-2008|No aparecen datos|34|32|  
  
 Puede observar que los pronósticos con los datos extendidos (que se muestran aquí en negrita) repiten exactamente los puntos de datos reales. La repetición es por diseño. Mientras haya puntos de datos reales para usar, la consulta de predicción devolverá los valores reales y generará nuevos valores de predicción solo después de que se hayan usado los nuevos puntos de datos reales.  
  
 En general, el algoritmo pondera los cambios en los datos nuevos más que los datos del principio de los datos del modelo. Sin embargo, en este caso, las nuevas cifras de ventas representan un incremento de solo el 20-30 por ciento durante el período anterior, por lo que hubo tan solo un ligero repunte de las ventas previstas, tras el cual las proyecciones de ventas vuelven a descender, más en línea con la tendencia de los meses anteriores a los datos nuevos.  
  
##  <a name="bkmk_REPLACE"></a>Comparar los resultados originales y entre predicciones  
 Recuerde que el modelo de minería de datos original revelaba grandes diferencias entre las regiones y las líneas de productos. Por ejemplo, las ventas para el modelo M200 fueron muy marcadas, mientras que las ventas del modelo T1000 fueron bastante bajas en todas las regiones. Además, algunas series no tenían muchos datos. Las series eran desiguales, lo que significa que no tenían el mismo punto de partida.  
  
 ![Serie que predice la cantidad de M200 y T1000](../../2014/tutorials/media/6series-defaultforecasting.gif "Serie que predice la cantidad de M200 y T1000")  
  
 Por lo tanto, ¿cómo cambiaron las predicciones cuando se realizaron proyecciones basadas en el modelo general, que se basaba a su vez en las ventas mundiales, no en los conjuntos de datos originales? Para asegurarse de que no ha perdido ninguna información ni ha sesgado las predicciones, puede guardar los resultados en una tabla, combinar la tabla de predicciones con la de datos históricos y, después, crear un gráfico de los dos conjuntos de datos históricos y predicciones.  
  
 El siguiente diagrama se basa solo en una línea de productos, M200. En el gráfico se comparan las predicciones del modelo de minería de datos inicial con las predicciones que usan el modelo de minería de datos agregado.  
  
 ![Gráfico de Excel que compara las predicciones](../../2014/tutorials/media/m200-predictions-compared.gif "Gráfico de Excel que compara las predicciones")  
  
 En este diagrama, se puede ver que el modelo de minería agregado conserva los intervalos y tendencias generales de los valores, a la vez que reduce las fluctuaciones de las series de datos individuales.  
  
## <a name="conclusion"></a>Conclusión  
 Ha aprendido a crear y personalizar un modelo de serie temporal que se puede usar para la predicción.  
  
 Ha aprendido a actualizar los modelos de serie temporal sin tener que volver a procesarlos, y ha agregado nuevos datos y creado predicciones mediante el parámetro EXTEND_MODEL_CASES.  
  
 Ha aprendido a crear modelos que se pueden usar para la predicción cruzada y ha utilizado el parámetro REPLACE_MODEL_CASES y aplicado el modelo a una serie de datos diferente.  
  
## <a name="see-also"></a>Consulte también  
 [Tutorial intermedio de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)   
 [Ejemplos de consultas de modelos de serie temporal](../../2014/analysis-services/data-mining/time-series-model-query-examples.md)  
  
  
