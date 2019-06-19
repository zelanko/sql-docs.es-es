---
title: Personalizar y procesar el modelo de pronóstico (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4bd25e15-9d9e-4528-b7bc-ccb856643aec
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d2d0e73d1d9a4058ff63320552604b2bfa1bca8a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249400"
---
# <a name="customizing-and-processing-the-forecasting-model-intermediate-data-mining-tutorial"></a>Personalizar y procesar el modelo de pronóstico (tutorial intermedio de minería de datos)
  El algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] proporciona varios parámetros que afectan al modo de creación de un modelo y al modo en que se analizan los datos temporales. Cambiar estas propiedades puede afectar de forma significativa a la manera en que el modelo de minería de datos realiza las predicciones.  
  
 Para esta tarea del tutorial, modificará el modelo mediante las tareas siguientes:  
  
1.  Va a personalizar la manera en que el modelo controla los períodos de tiempo agregando un nuevo valor para el *PERIODICITY_HINT* parámetro.  
  
2.  Obtendrá información sobre otros aproximadamente dos parámetros importantes para el algoritmo de serie temporal de Microsoft: FORECAST_METHOD, que le permite controlar el método usado para la predicción, y PREDICTION_SMOOTHING, que le permite personalización la combinación de predicciones a corto plazo y a largo plazo.  
  
3.  Opcionalmente, indicará al algoritmo cómo desea que se imputen los valores ausentes.  
  
4.  Una vez realizados todos los cambios, implementará y procesará el modelo.  
  
## <a name="setting-time-series-parameters"></a>Establecer los parámetros de serie temporal  
 **Sugerencias de periodicidad**  
  
 El *PERIODICITY_HINT* parámetro proporciona al algoritmo información sobre los períodos de tiempo adicional que espera ver en los datos. De forma predeterminada, los modelos de serie temporal intentarán detectar automáticamente un patrón en los datos. Sin embargo, si ya conoce el período de tiempo esperado, proporcionar una sugerencia de periodicidad podría mejorar la exactitud del modelo. Sin embargo, si proporciona una sugerencia de periodicidad errónea, puede reducir la exactitud; por consiguiente, si no está seguro del valor que debe utilizarse, es mejor usar el valor predeterminado.  
  
 Por ejemplo, la vista utilizada para este modelo agrega datos de ventas mensuales de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Por consiguiente, cada segmento de tiempo utilizado en el modelo representa un mes y todas las predicciones también estarán en términos de meses. Dado que hay 12 meses en un año y esperar a que los patrones de ventas repetirán más o menos cada año, establecerá el *PERIODICITY_HINT* parámetro `12`para indicar que 12 segmentos de tiempo (meses) constituyen una ciclo de ventas completo.  
  
 **Método de pronóstico**  
  
 El *FORECAST_METHOD* parámetro controla si el algoritmo de serie temporal está optimizado para predicciones a corto o a largo plazo. De forma predeterminada, el *FORECAST_METHOD* parámetro está establecido en MIXED, lo que significa que dos diferentes algoritmos mezclan y equilibran para ofrecer resultados correctos para la predicción a corto y a largo plazo.  
  
 No obstante, si sabe que debe usar un algoritmo concreto, puede cambiar el valor a ARIMA o ARTXP.  
  
 **Ponderación vs a largo plazo. Predicciones a corto plazo**  
  
 También puede personalizar el modo en que las predicciones a largo plazo y a corto plazo se combinan mediante el parámetro PREDICTION_SMOOTHING. De forma predeterminada, este parámetro está establecido en 0,5, lo que generalmente proporciona el mayor equilibrio para conseguir la máxima precisión.  
  
#### <a name="to-change-the-algorithm-parameters"></a>Para cambiar los parámetros del algoritmo  
  
1.  En el **modelos de minería de datos** secundario **Forecasting**y seleccione **establecer parámetros de algoritmo**.  
  
2.  En el `PERIODICITY_HINT` fila de la **parámetros de algoritmo** cuadro de diálogo, haga clic en el **valor** columna, a continuación, escriba `{12}`, incluidas las llaves.  
  
     De forma predeterminada, el algoritmo también agregará el valor {1}.  
  
3.  En el `FORECAST_METHOD` la fila, compruebe que la **valor** cuadro de texto está en blanco o establecido en `MIXED`. Si se ha especificado un valor diferente, escriba `MIXED` para cambiar el parámetro en el valor predeterminado.  
  
4.  En el **PREDICTION_SMOOTHING** la fila, compruebe que la **valor** cuadro de texto está en blanco o establecido en 0,5. Si se ha especificado un valor diferente, haga clic en **valor** y tipo `0.5` para cambiar el parámetro en el valor predeterminado.  
  
    > [!NOTE]  
    >  El parámetro PREDICTION_SMOOTHING solo está disponible en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise. Por consiguiente, en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard no puede ver ni cambiar el valor del parámetro PREDICTION_SMOOTHING. Sin embargo, el comportamiento predeterminado es utilizar los dos algoritmos y ponderarlos de forma equitativa.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="handling-missing-data-optional"></a>Manejar la ausencia de datos (opcional)  
 En muchos casos, los datos de ventas podrían tener huecos que se rellenan con caracteres nulos, o es posible que un almacén no haya podido cumplir la fecha tope de notificación, con lo que se ha dejado una celda vacía al final de la serie. En estos escenarios, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] genera el error siguiente y no procesa el modelo.  
  
 "Error (minería de datos): Marcas de tiempo no sincronizadas empiezan con la serie \<nombre de la serie >, del modelo de minería de datos, \<nombre de modelo >. Todas las series temporales deben terminar en la misma marca de tiempo y no pueden tener puntos de datos ausentes arbitrarios. Cuando el valor del parámetro MISSING_VALUE_SUBSTITUTION es Previous o una constante numérica, se revisarán automáticamente los puntos de datos ausentes siempre que sea posible."  
  
 Para evitar este error, puede especificar que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporcione automáticamente los valores nuevos para rellenar los huecos utilizando uno de los métodos siguientes:  
  
-   Utilizar un valor promedio. El promedio se calcula utilizando todos los valores válidos en la misma serie de datos.  
  
-   Utilizar el valor anterior. Puede sustituir los valores anteriores para varias celdas que falten, pero no puede rellenar los valores de iniciales.  
  
-   Utilizar un valor constante que proporcione el usuario.  
  
#### <a name="to-specify-that-gaps-be-filled-by-averaging-values"></a>Para especificar que los huecos se rellenen calculando el promedio de los valores  
  
1.  En el **modelos de minería de datos** pestaña, haga clic en el **Forecasting** columna y seleccione **establecer parámetros de algoritmo**.  
  
2.  En el **parámetros de algoritmo** cuadro de diálogo el **MISSING_VALUE_SUBSTITUTION** la fila, haga clic en el **valor** columna y escriba `Mean`.  
  
## <a name="build-the-model"></a>Generar el modelo  
 Para usar el modelo, debe implementarlo en un servidor y procesarlo ejecutando los datos de aprendizaje a través del algoritmo.  
  
#### <a name="to-process-the-forecasting-model"></a>Para procesar el modelo de pronóstico  
  
1.  En el menú **Modelo de minería de datos** de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], seleccione **Procesar estructura de minería de datos y todos los modelos**.  
  
2.  En la advertencia en la que se pregunta si desea generar e implementar el proyecto, haga clic en **Sí**.  
  
3.  En el **procesar estructura de minería de datos - pronóstico** cuadro de diálogo, haga clic en **ejecutar**.  
  
     Se abre el cuadro de diálogo **Progreso del proceso** para mostrar información acerca del procesamiento del modelo. El procesamiento del modelo puede tardar algún tiempo.  
  
4.  Cuando se complete el proceso, haga clic en **Cerrar** para salir del cuadro de diálogo **Progreso del proceso** .  
  
5.  Haga clic en **cerrar** nuevo para salir del **procesar estructura de minería de datos - pronóstico** cuadro de diálogo.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar el modelo de previsión &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/exploring-the-forecasting-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
