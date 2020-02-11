---
title: Crear una estructura y un modelo de previsión (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63204812"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Crear una estructura de pronóstico y un modelo (tutorial intermedio de minería de datos)
  A continuación utilizará el Asistente para minería de datos con el objeto de crear una nueva estructura de minería de datos y el modelo de minería de datos según la vista del origen de datos recién creada. En esta tarea, especificará que el modelo de minería de datos debería utilizar el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Para crear una estructura de minería de datos de previsión  
  
1.  En Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic con el botón secundario en **estructuras de minería de datos** y seleccione **nueva estructura de minería de datos**.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En la página **seleccionar el método de definición** , compruebe que la opción **de base de datos relacional o del almacenamiento de datos existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En la página **crear la estructura de minería de datos** , en **¿qué técnica de minería de datos desea utilizar?**, seleccione **serie temporal de Microsoft**y, a continuación, haga clic en **siguiente**.  
  
5.  En la página **seleccionar vista del origen de datos** , en vistas del origen de **datos disponibles**, seleccione **SalesByRegion**.  
  
6.  Haga clic en **Next**.  
  
7.  En la página **especificar tipos de tablas** , asegúrese de que está seleccionada la casilla de la columna **caso** de la tabla vTimeSeries y, a continuación, haga clic en **siguiente**.  
  
8.  En la página **especificar los datos de aprendizaje** , active las casillas de la columna de **clave** para las columnas ModelRegion y ReportingDate.  
  
     ReportingDate debería estar activada de forma predeterminada, porque esta columna se especificó como la clave principal lógica cuando se creó la vista del origen de datos. Al agregar la columna ModelRegion como una segunda clave, se está indicando al algoritmo que cree una serie temporal independiente para cada combinación de modelo y región enumerada en este campo.  
  
9. Active las casillas de las columnas de **entrada** y de **predicción** para la columna quantity y, a continuación, haga clic en **siguiente**.  
  
     Al seleccionar predecible, indica que desea crear **predicciones**sobre los datos de esta columna. Sin embargo, dado que desea basar los pronósticos en datos previos, también debe agregar la columna como una entrada.  
  
10. En la página **especificar el contenido y el tipo de datos de las columnas**, revise las selecciones.  
  
     La columna ModelRegion se designa como columna de **clave** y la columna ReportingDate se designa automáticamente como una columna **key Time** . Puede tener solo una clave de cada tipo.  
  
11. Haga clic en **Next**.  
  
12. En la página **finalización del asistente** , en nombre de la estructura `Forecasting`de minería de **datos**, escriba.  
  
    > [!NOTE]  
    >  La opción para habilitar la obtención de detalles no está disponible para los modelos de serie temporal.  
  
13. En **nombre del modelo**de minería `Forecasting`de datos, escriba y, a continuación, haga clic en **Finalizar**.  
  
     El diseñador de minería de datos se `Forecasting` abre para mostrar la estructura de minería de datos que acaba de crear.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar la estructura de previsión &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Diseñador de minería de datos](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
