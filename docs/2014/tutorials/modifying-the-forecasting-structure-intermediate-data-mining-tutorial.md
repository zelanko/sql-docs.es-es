---
title: Modificar la estructura de previsión (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 559f6aa6b31b8998703a93e84dc100ce375cbda8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48139535"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modificar la estructura de previsión (tutorial intermedio de minería de datos)
  La estructura de minería de datos que creó en la tarea anterior contiene un modelo de previsión (Forecasting) individual. Antes de procesar y explorar el modelo, debe cambiar su estructura ligeramente y modificar una de sus propiedades.  
  
## <a name="modifying-the-mining-structure"></a>Modificar la estructura de minería de datos  
 Puede cambiar la estructura de minería de datos mediante el **estructura de minería de datos** ficha del Diseñador de minería de datos. Al crear el modelo con el Asistente para minería de datos, se utilizaron tres columnas: ReportingDate, ModelRegion y Quantity. Sin embargo, el **Forecasting** tabla también contiene una columna Amount, que puede usar para predecir el importe de ventas. Mediante el uso de la **estructura de minería de datos** ficha, puede agregar esta columna de la vista del origen de datos a la estructura de minería de datos.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Para agregar la columna Amount a la estructura de minería de datos Forecasting  
  
1.  En el **Mining Structure** ficha del Diseñador de minería de datos, en el **vista del origen de datos** panel, seleccione la columna de cantidad en la tabla vTimeSeries.  
  
2.  Arrastre la columna Amount desde el **vista del origen de datos** panel en la lista de columnas para la **Forecasting** estructura.  
  
     La columna Amount se incluye ahora en el **Forecasting** estructura de minería de datos.  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modificar las columnas del modelo de minería de datos  
 Dado que ha agregado una columna nueva a la estructura, debe definir la forma en que el modelo utilizará la columna. Puede especificar cómo se utilizará la columna en la **modelos de minería de datos** ficha del Diseñador de minería de datos.  
  
 El **modelos de minería de datos** ficha enumera las columnas que contiene la estructura de minería de datos en el **estructura** columna de la cuadrícula y muestra las columnas que contiene el modelo de minería de datos en la columna que tiene el nombre de la modelo, en este caso **Forecasting**. Haga clic en los nombres de las columnas para hacer modificaciones. En el **Forecasting** modelo de minería de datos, la columna Amount se utiliza como columna de entrada y también se utiliza para pronosticar las ventas futuras. Por tanto, debe establecer las propiedades de la columna de manera que se pueda utilizar como columna de entrada y de predicción.  
  
> [!NOTE]  
>  En el **modelos de minería de datos** pestaña, también puede crear nuevos modelos basados en la misma estructura, y se pueden ajustar las propiedades de algoritmo y la columna para cada modelo. Sin embargo, debe procesar el modelo para que los cambios surtan efecto.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Para definir cómo se utilizará la columna Amount  
  
1.  En el **Forecasting** columna de la cuadrícula en el **modelos de minería de datos** pestaña, haga clic en la celda de la fila Amount.  
  
2.  Seleccione **Predict** en la lista.  
  
     La columna Amount es ahora una columna de entrada y una columna de predicción.  
  
 También puede cambiar las propiedades de columnas individuales seleccionando la columna y abriendo la **propiedades** ventana. Para abrir el **propiedades** , haga clic en el nombre de columna y, a continuación, seleccione **propiedades**. Si cambia una propiedad de la columna para un modelo individual, solo podrá cambiar las propiedades para ese modelo. Sin embargo, cuando cambia una propiedad de la **estructura** columna, el cambio afecta a cada modelo que está asociado con la estructura. Siempre que realice cambios en el modelo o la estructura, debe volver a procesarlos para ver el efecto de dicho cambios.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Personalizar y procesar el modelo de pronóstico &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Estructuras de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Los modelos de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
