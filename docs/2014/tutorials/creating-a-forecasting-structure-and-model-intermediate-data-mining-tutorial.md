---
title: Crear una estructura de previsión y un modelo (Tutorial de minería de datos intermedios) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 47d6e75a691c53fe1658fb5f79ee2bde8e9c2d01
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312273"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Crear una estructura de pronóstico y un modelo (tutorial intermedio de minería de datos)
  A continuación utilizará el Asistente para minería de datos con el objeto de crear una nueva estructura de minería de datos y el modelo de minería de datos según la vista del origen de datos recién creada. En esta tarea, especificará que el modelo de minería de datos debería utilizar el algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Para crear una estructura de minería de datos de previsión  
  
1.  En el Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic en **estructuras de minería de datos** y seleccione **nueva estructura de minería de datos**.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar el método de definición** , comprueba que **de almacén de datos o base de datos relacional existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En el **crear la estructura de minería de datos** página, en **¿qué técnica de minería de datos que desea usar?**, seleccione **serie temporal de Microsoft**y, a continuación, haga clic en  **Siguiente**.  
  
5.  En el **seleccionar vista del origen de datos** página, en **vistas del origen de datos disponibles**, seleccione **SalesByRegion**.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En el **especificar tipos de tablas** página, asegúrese de que la casilla de verificación en la **caso** columna para la tabla vTimeSeries está seleccionada y, a continuación, haga clic en **siguiente**.  
  
8.  En el **especificar los datos de entrenamiento** , seleccione las casillas de verificación en la **clave** columna para las columnas ModelRegion y ReportingDate.  
  
     ReportingDate debería estar activada de forma predeterminada, porque esta columna se especificó como la clave principal lógica cuando se creó la vista del origen de datos. Al agregar la columna ModelRegion como una segunda clave, se está indicando al algoritmo que cree una serie temporal independiente para cada combinación de modelo y región enumerada en este campo.  
  
9. Seleccione las casillas de verificación en la **entrada** y **Predictable** columnas para la cantidad, columna y, a continuación, haga clic en **siguiente**.  
  
     Si selecciona **Predictable**, que indique que desea crear pronósticos con los datos de esta columna. Sin embargo, dado que desea basar los pronósticos en datos previos, también debe agregar la columna como una entrada.  
  
10. En la página **contenido y el tipo de datos de columnas Especifique**, revise las selecciones.  
  
     La columna ModelRegion se designa como un **clave** columna y la columna ReportingDate se designa automáticamente como un **Key Time** columna. Puede tener solo una clave de cada tipo.  
  
11. Haga clic en **Siguiente**.  
  
12. En el **finalización del Asistente para** página, para **nombre de la estructura de minería de datos**, tipo `Forecasting`.  
  
    > [!NOTE]  
    >  La opción para habilitar la obtención de detalles no está disponible para los modelos de serie temporal.  
  
13. En **nombre del modelo de minería de datos**, tipo `Forecasting`y, a continuación, haga clic en **finalizar**.  
  
     Diseñador de minería de datos se abre para mostrar el `Forecasting` estructura de minería de datos que acaba de crear.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Modificar la estructura de previsión &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Diseñador de minería de datos](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  