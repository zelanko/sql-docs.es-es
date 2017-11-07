---
title: "Elija la columna que se usan para probar un modelo de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [data mining], predictable mining columns
- Mining Accuracy Chart [Analysis Services], columns
- predictable mining columns [Analysis Services]
ms.assetid: c6a8f23a-da21-4f31-9521-99460d624649
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 995738c17a385d26e647a6c650c21a791b872a0e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="choose-the-column-to-use-for-testing-a-mining-model"></a>Elija la columna que se va a utilizar para probar un modelo de minería de datos
  Para poder medir la exactitud de un modelo de minería de datos, debe decidir qué resultado desea devolver. La mayoría de los modelos de minería de datos requieren que seleccione al menos una columna para utilizarla como atributo de predicción al crear el modelo. Por consiguiente, al probar la precisión del modelo, normalmente debe seleccionar ese atributo para las pruebas.  
  
 En la siguiente lista se describen algunas consideraciones adicionales para elegir el atributo de predicción para utilizarlo en las pruebas:  
  
-   Algunos tipos de modelos de minería de datos pueden predecir varios atributos, como las redes neuronales, que pueden explorar las relaciones entre muchos atributos.  
  
-   Otros tipos de modelos de minería de datos, como los modelos de clústeres, no tienen, necesariamente, un atributo de predicción. Los modelos de clústeres no se pueden probar a menos que tengan un atributo de predicción.  
  
-   Para crear un gráfico de dispersión o medir la exactitud de un modelo de regresión es necesario que elija un atributo de predicción continuo como resultado. En ese caso, no puede especificar un valor de destino. Si va a crear algo distinto de un gráfico de dispersión, la columna de la estructura de minería de datos subyacente también debe tener un tipo de contenido **Discreto** o **Discretizado**.  
  
-   Si elige un atributo discreto como resultado de predicción, puede especificar un valor de destino o puede dejar en blanco el campo **Valor de predicción** . Si incluye un **Valor de predicción**, el gráfico medirá solo la eficacia del modelo para predecir el valor de destino. Si no especifica un resultado de destino, se mide la precisión del modelo al predecir los resultados.  
  
-   Si desea incluir varios modelos y compararlos en un único gráfico de precisión, todos los modelos deben usar la misma columna de predicción.  
  
-   Al crear un informe de validación cruzada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] analizará de modo automático todos los modelos que tengan el mismo atributo de predicción.  
  
-   Cuando la opción **Sincronizar valores y columnas de predicción**está seleccionado, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elige automáticamente las columnas de predicción que tienen los mismos nombres y tipos de datos coincidentes. Si las columnas no cumplen estos criterios, puede desactivar esta opción y elegir manualmente una columna de predicción. Puede que tenga que hacer esto si va a probar el modelo con un conjunto de datos externo que tenga columnas distintas a las del modelo. Sin embargo, si elige una columna con el del tipo de datos incorrecto, obtendrá un error o resultados erróneos.  
  
### <a name="specify-the-outcome-to-predict"></a>Especifique el resultado de la predicción  
  
1.  Haga doble clic en la estructura de minería de datos para abrirla en el Diseñador de minería de datos.  
  
2.  Seleccione la pestaña **Gráfico de precisión de minería de datos** .  
  
3.  Seleccione la pestaña **Selección de entrada** .  
  
4.  En la pestaña **Selección de entrada** , en **Nombre de columna de predicción**, seleccione una columna de predicción para cada modelo que vaya a incluir en el gráfico.  
  
     Las columnas del modelo de minería de datos que están disponibles en el cuadro **Nombre de columna de predicción** solo son aquellas cuyo tipo de uso se ha establecido en **Predicción** o **Solo predicción**.  
  
5.  Si desea determinar la elevación de un modelo, debe seleccionar un valor específico del resultado para la medición, eligiéndolo en la lista **Valor de predicción** .  
  
## <a name="see-also"></a>Vea también  
 [Elegir y asignar datos de prueba para el modelo](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)   
 [Elegir un tipo de gráfico de precisión y establecer opciones del gráfico](../../analysis-services/data-mining/choose-an-accuracy-chart-type-and-set-chart-options.md)  
  
  

