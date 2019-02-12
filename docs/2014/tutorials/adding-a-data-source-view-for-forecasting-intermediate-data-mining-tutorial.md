---
title: Agregar datos de una vista del origen para la previsión (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2665040a-1291-4064-ba01-f458637dda57
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f60ea2b2a642cf9435ed8366c42e43abb927e426
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034806"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>Agregar una vista del origen de datos para las previsiones (tutorial intermedio de minería de datos)
  En esta tarea, agregará una vista del origen de datos que se utilizará para el escenario de pronóstico. Un modelo de previsión requiere que los datos contengan una columna que se pueda utilizar para identificar pasos en una serie temporal. Si piensa analizar varias series de datos, todas ellas deben finalizar en la misma fecha o estadio temporal.  
  
### <a name="to-add-a-data-source-view"></a>Para agregar una vista del origen de datos  
  
1.  En el Explorador de soluciones, haga clic en **vistas del origen de datos**y, a continuación, seleccione **nueva vista del origen de datos**.  
  
2.  En la página **Asistente para vistas del origen de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar un origen de datos** página, en **orígenes de datos relacionales**, seleccione el [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] origen de datos. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si no tiene este origen de datos, puede encontrar los pasos para crear el origen de datos en el [Basic Data Mining Tutorial](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
4.  En el **seleccionar tablas y vistas** , seleccione la tabla, vTimeSeries (dbo) y, a continuación, haga clic en la flecha derecha para agregarla a la vista del origen de datos.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **completando el Asistente para** página, de forma predeterminada la vista del origen de datos se denomina [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Cambie el nombre a **SalesByRegion**y, a continuación, haga clic en **finalizar**.  
  
     Se abre el Diseñador de vistas del origen de datos y el **SalesByRegion** aparece la vista del origen de datos.  
  
## <a name="working-with-the-data-source-view"></a>Trabajar con la vista del origen de datos  
 Una vez creada la vista del origen de datos, puede explorar los datos de la siguiente manera:  
  
-   Haga clic en la tabla vTimeSeries en el diseñador y seleccione **explorar datos** para abrir la tabla seleccionada en una cuadrícula.  
  
-   Haga clic en **opciones de muestreo** y, a continuación, utilice el **opciones de exploración de datos** cuadro de diálogo para cambiar el método de muestreo. Haga clic en **actualizar** para cargar datos en la tabla con la nueva opción de configuración. Por ejemplo, podría especificar el número de filas que se generarán en el ejemplo, o elija las primeras n filas.  
  
-   Haga clic en la tabla vTimeSeries y seleccione **propiedades** para asignar un nombre nuevo a la tabla. También puede seleccionar columnas individuales de la vista del origen de datos y modificar las propiedades de columna.  
  
-   Haga clic en cualquier lugar del área de diseño de la vista del origen de datos para crear una nueva consulta y asignarle un nombre, crear relaciones entre las tablas o cambiar la disposición del área de diseño.  
  
-   Haga clic en una tabla y seleccione **nuevo cálculo con nombre** para crear columnas derivadas, incluidas las agregaciones. También puede añadir nuevas tablas y vistas del origen de datos a esta vista.  
  
 En la tarea siguiente, explorará los datos de la serie temporal y determinará la mejor columna para utilizar como identificador de serie temporal. También aprenderá a administrar los vacíos en los datos de la serie temporal.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Descripción de los requisitos para una serie temporal modelo &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
