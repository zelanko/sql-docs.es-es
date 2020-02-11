---
title: Modificar la estructura de previsión (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1a6c138e-643b-4ae6-ad08-93631f149c20
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a86ddf0a715fc3a2313f555e898b3bd94cf66d8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63301299"
---
# <a name="modifying-the-forecasting-structure-intermediate-data-mining-tutorial"></a>Modificar la estructura de previsión (tutorial intermedio de minería de datos)
  La estructura de minería de datos que creó en la tarea anterior contiene un modelo de previsión (Forecasting) individual. Antes de procesar y explorar el modelo, debe cambiar su estructura ligeramente y modificar una de sus propiedades.  
  
## <a name="modifying-the-mining-structure"></a>Modificar la estructura de minería de datos  
 Puede cambiar la estructura de minería de datos mediante la pestaña **estructura de minería** de datos del diseñador de minería de datos. Al crear el modelo con el Asistente para minería de datos, se utilizaron tres columnas: ReportingDate, ModelRegion y Quantity. Sin embargo, la tabla **Forecasting** también contiene una columna amount, que puede usar para predecir la cantidad de ventas. Mediante la pestaña **estructura de minería** de datos, puede Agregar esta columna desde la vista del origen de datos a la estructura de minería de datos.  
  
#### <a name="to-add-the-amount-column-to-the-forecasting-mining-structure"></a>Para agregar la columna Amount a la estructura de minería de datos Forecasting  
  
1.  En la pestaña **estructura de minería** de datos del diseñador de minería de datos, en el panel vista del origen de **datos** , seleccione la columna amount de la tabla vTimeSeries.  
  
2.  Arrastre la columna amount desde el panel **vista del origen de datos** hasta la lista de columnas de la estructura **Forecasting** .  
  
     La columna amount se incluye ahora en la estructura de minería de datos **Forecasting** .  
  
## <a name="modifying-the-columns-in-the-mining-model"></a>Modificar las columnas del modelo de minería de datos  
 Dado que ha agregado una columna nueva a la estructura, debe definir la forma en que el modelo utilizará la columna. Puede especificar cómo se utilizará la columna en la pestaña **modelos de minería** de datos del diseñador de minería de datos.  
  
 En la pestaña **modelos de minería de datos** se muestran las columnas que contiene la estructura de minería de datos en la columna **estructura** de la cuadrícula y se enumeran las columnas que contiene el modelo de minería de datos en la columna que tiene el nombre del modelo, en este caso **Forecasting**. Haga clic en los nombres de las columnas para hacer modificaciones. En el modelo de minería de datos **Forecasting** , la columna amount se utiliza como columna de entrada y también se utiliza para pronosticar las ventas futuras. Por tanto, debe establecer las propiedades de la columna de manera que se pueda utilizar como columna de entrada y de predicción.  
  
> [!NOTE]  
>  En la pestaña **modelos de minería de datos** , también puede crear nuevos modelos basados en la misma estructura, y puede ajustar las propiedades de los algoritmos y las columnas de cada modelo. Sin embargo, debe procesar el modelo para que los cambios surtan efecto.  
  
#### <a name="to-define-how-the-amount-column-will-be-used"></a>Para definir cómo se utilizará la columna Amount  
  
1.  En la columna **Forecasting** de la cuadrícula de la pestaña **modelos de minería de datos** , haga clic en la celda de la fila amount.  
  
2.  Seleccione **predicción** en la lista.  
  
     La columna Amount es ahora una columna de entrada y una columna de predicción.  
  
 También puede cambiar las propiedades de columnas individuales seleccionando la columna y abriendo la ventana **propiedades** . Para abrir la ventana **propiedades** , haga clic con el botón secundario en el nombre de la columna y, a continuación, seleccione **propiedades**. Si cambia una propiedad de la columna para un modelo individual, solo podrá cambiar las propiedades para ese modelo. Sin embargo, al cambiar una propiedad dentro de la columna de **estructura** , el cambio afecta a todos los modelos que están asociados a la estructura. Siempre que realice cambios en el modelo o la estructura, debe volver a procesarlos para ver el efecto de dicho cambios.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Personalizar y procesar el modelo de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/customize-process-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Estructuras de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [Modelos de minería de datos &#40;Analysis Services&#41;de minería de datos](../../2014/analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
  
