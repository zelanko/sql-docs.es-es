---
title: Explorar y limpiar datos | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7c888c95-8986-461e-9f11-2395044b9d97
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79d356aa1b14ac30ba5bc9a8f579fc66ddebea92
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081268"
---
# <a name="exploring-and-cleaning-data"></a>Explorar y limpiar datos
  La preparación de los datos es mucho más que limpiarlos. Recuerde que el modo en que los datos se preparan también afecta al modo en que los resultados se interpretan en el extremo. La preparación de los datos implica estas tareas:  
  
-   Explorar y comprobar la distribución de los datos.  
  
-   Limpiar los registros no válidos y elegir las columnas para la minería de datos.  
  
-   Controlar los valores NULL correctamente.  
  
-   Discretizar los valores o agregar valores en distintos fragmentos de tiempo.  
  
-   Agregar etiquetas para mejorar la utilidad de los resultados.  
  
-   Convertir los tipos de datos o categorizar los valores en caso necesario para el análisis.  
  
 Si no está familiarizado con el modelado de datos, se recomienda leer el tema relacionado, [lista de comprobación de preparación para la minería de datos](checklist-of-preparation-for-data-mining.md).  
  
## <a name="data-preparation-tools"></a>Herramientas de preparación de datos  
 Complementos de minería de datos para Office incluye las herramientas siguientes para la limpieza y preparación de los datos:  
  
### <a name="explore-data"></a>Explorar datos  
 Use el Asistente para **explorar datos** para estas tareas de preparación de datos:  
  
-   Obtener una vista previa de los datos e identificar errores que se deben corregir antes del análisis.  
  
-   Recopile información estadística que sea útil para comprender el equilibrio de los datos y las tareas necesarias de limpieza.  
  
-   Identificar columnas que son útiles para el análisis y planear la fase de modelado de datos.  
  
 [Explore los datos &#40;SQL Server complementos de minería de datos&#41;](explore-data-sql-server-data-mining-add-ins.md).  
  
### <a name="detect-and-handle-outliers"></a>Detectar y administrar valores atípicos  
 El asistente valores **atípicos** representa gráficamente la distribución de los valores de los datos y ayuda a quitar los valores extremos. Use la herramienta **valores atípicos** para las siguientes tareas de preparación de datos:  
  
-   Determinar si los distintos valores son confiables, basándose en los patrones encontrados en los datos.  
  
-   Revisar valores inusuales y eliminarlos o reemplazarlos.  
  
-   Definir el ámbito de un modelo a un intervalo de valores específico. Por ejemplo, si sabe que tiene valores atípicos en un almacén determinado, puede eliminar ese valor y obtener un modelo que obtenga mejores predicciones en otros almacenes.  
  
 [Valores atípicos &#40;SQL Server complementos de minería de datos&#41;](outliers-sql-server-data-mining-add-ins.md).  
  
### <a name="relabel-and-bin-data"></a>Cambiar etiquetas y discretizar datos  
 El Asistente para cambiar **etiquetas** agrupa los datos por valores para que pueda cambiar las etiquetas de los datos. Utilice la herramienta Cambiar etiquetas para estas tareas de preparación de datos:  
  
-   Cambiar los códigos numéricos utilizados en los resultados de una encuesta por una descripción de texto con el significado de los códigos numéricos.  
  
     Por ejemplo, puede reemplazar entradas de datos como Sexo = 1 por Sexo = Mujer.  
  
-   Discretizar datos mediante la creación de grupos que representen intervalos de números.  
  
     Por ejemplo, puede que desee reemplazar una columna ingresos de números por etiquetas como **ingresos-moderado** e **ingresos-alto**.  
  
-   Contraer valores discretos en categorías.  
  
     Por ejemplo, si tiene demasiados productos individuales que le imposibilitan detectar un patrón de compras, puede intentar reagrupar los productos en categorías.  
  
 [Cambiar la etiqueta de &#40;SQL Server complementos de minería de datos&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
### <a name="cleanse-data"></a>Limpiar datos  
 La limpieza de datos abarca una amplia variedad de actividades, la mayoría de las cuales se realizan mediante los complementos  
  
-   Identificar valores NULL y determinar si se deben cambiar por valores reales o se deben considerar valores `Missing`.  
  
-   Detectar valores ausentes y quitarlos o imputarles un valor adecuado, como una media, un valor NULL u otro valor.  
  
 [Explorar datos &#40;SQL Server complementos de minería de datos&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
 [Cambiar la etiqueta de &#40;SQL Server complementos de minería de datos&#41;](relabel-sql-server-data-mining-add-ins.md)  
  
 [Rellenar desde ejemplo](fill-from-example-table-analysis-tools-for-excel.md)  
  
### <a name="sample-data"></a>Datos de ejemplo  
 El Asistente para datos de muestra proporciona dos métodos para crear conjuntos de datos equilibrados para entrenar y probar modelos.  
  
-   **Muestreo aleatorio.** Utilice esta opción para extraer un conjunto de datos representativo de un conjunto de datos más grande y usarlos como datos de entrenamiento o de prueba. Los complementos de minería de datos usan el *muestreo estratificado* para asegurarse de que se obtiene un conjunto equilibrado de valores para cada variable muestreada.  
  
-   **Sobremuestreo.** Utilice esta opción cuando disponga de menos datos de los que le gustaría para un resultado de destino, y necesite dar a dichos datos un peso mayor. Por ejemplo, el fraude puede ser relativamente poco frecuente, pero puede sobremuestrear los casos que implican fraude para obtener datos apropiados para el modelado.  
  
 [&#40;de datos de ejemplo SQL Server complementos de minería de datos&#41;](sample-data-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Validar modelos y usar modelos para la predicción &#40;complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Implementar y escalar modelos de minería de datos &#40;complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
