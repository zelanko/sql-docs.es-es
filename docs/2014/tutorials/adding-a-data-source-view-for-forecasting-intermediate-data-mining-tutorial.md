---
title: Agregar una vista del origen de datos para la previsión (tutorial intermedio de minería de datos) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62823135"
---
# <a name="adding-a-data-source-view-for-forecasting-intermediate-data-mining-tutorial"></a>Agregar una vista del origen de datos para las previsiones (tutorial intermedio de minería de datos)
  En esta tarea, agregará una vista del origen de datos que se utilizará para el escenario de pronóstico. Un modelo de previsión requiere que los datos contengan una columna que se pueda utilizar para identificar pasos en una serie temporal. Si piensa analizar varias series de datos, todas ellas deben finalizar en la misma fecha o estadio temporal.  
  
### <a name="to-add-a-data-source-view"></a>Para agregar una vista del origen de datos  
  
1.  En Explorador de soluciones, haga clic con el botón secundario en **vistas del origen de datos**y seleccione **nueva vista del origen de datos**.  
  
2.  En la página inicial del **Asistente para orígenes de datos**, haga clic en **Siguiente**.  
  
3.  En la página **seleccionar un origen de datos** , en **orígenes de datos relacionales**, seleccione el origen de [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] datos. Haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Si no tiene este origen de datos, puede encontrar los pasos para crear el origen de datos en el [tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md).  
  
4.  En la página **seleccionar tablas y vistas** , seleccione la tabla vTimeSeries (DBO) y, a continuación, haga clic en la flecha derecha para agregarla a la vista del origen de datos.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **finalización del asistente** , la vista del origen de datos se [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]denomina de forma predeterminada. Cambie el nombre a **SalesByRegion**y, a continuación, haga clic en **Finalizar**.  
  
     Se abre el diseñador de vistas del origen de datos y aparece la vista del origen de datos **SalesByRegion** .  
  
## <a name="working-with-the-data-source-view"></a>Trabajar con la vista del origen de datos  
 Una vez creada la vista del origen de datos, puede explorar los datos de la siguiente manera:  
  
-   Haga clic con el botón secundario en la tabla vTimeSeries en el diseñador y seleccione **explorar datos** para abrir la tabla seleccionada en una cuadrícula.  
  
-   Haga clic en **Opciones de muestreo** y, a continuación, use el cuadro de diálogo Opciones de **exploración de datos** para cambiar el método de muestreo. Haga clic en **Actualizar** para cargar los datos en la tabla con la nueva configuración de opciones. Por ejemplo, puede especificar el número de filas que se van a generar en el ejemplo o elegir las n primeras filas.  
  
-   Haga clic con el botón secundario en la tabla vTimeSeries y seleccione **propiedades** para asignar un nuevo nombre a la tabla. También puede seleccionar columnas individuales de la vista del origen de datos y modificar las propiedades de columna.  
  
-   Haga clic en cualquier lugar del área de diseño de la vista del origen de datos para crear una nueva consulta y asignarle un nombre, crear relaciones entre las tablas o cambiar la disposición del área de diseño.  
  
-   Haga clic con el botón secundario en una tabla y seleccione **nuevo cálculo con nombre** para crear columnas derivadas, incluidas las agregaciones. También puede añadir nuevas tablas y vistas del origen de datos a esta vista.  
  
 En la tarea siguiente, explorará los datos de la serie temporal y determinará la mejor columna para utilizar como identificador de serie temporal. También aprenderá a administrar los vacíos en los datos de la serie temporal.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Descripción de los requisitos de un modelo de serie temporal &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/time-series-model-requirements-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
