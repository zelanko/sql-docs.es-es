---
title: Advanced predicciones de serie temporal (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b614ebdb-07ca-44af-a0ff-893364bd4b71
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f575a51d34bfaa6b8a4ca1a6200cf60f9d89a870
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48122745"
---
# <a name="advanced-time-series-predictions-intermediate-data-mining-tutorial"></a>Predicciones de serie temporal avanzadas (Tutorial intermedio de minería de datos)
  Al explorar el modelo de predicción, observó que, aunque las ventas de la mayoría de las regiones siguen un patrón similar, algunas regiones y algunos modelos, como el modelo M200 en la región del Pacífico, muestran tendencias muy diferentes. Esto no le sorprende, ya que sabe que las diferencias entre regiones son comunes y pueden deberse a muchos factores, como las promociones de marketing, los informes inexactos o los acontecimientos geopolíticos.  
  
 Sin embargo, los usuarios piden un modelo que se puede aplicar a todo el mundo. Por consiguiente, para reducir el efecto de los factores individuales en las proyecciones, decide crear un modelo de minería de datos basado en medidas agregadas de ventas mundiales. Puede usar este modelo para realizar las predicciones de cada región individual.  
  
 En esta tarea, creará todos los orígenes de datos que necesita para realizar las tareas de predicción avanzada. Creará dos vistas de origen de datos que usará como entradas en la consulta de predicción, y una vista de origen de datos que usará para crear un nuevo modelo.  
  
 **Pasos**  
  
1.  [Preparar los datos extendidos de ventas (para la predicción)](#bkmk_newExtendData)  
  
2.  [Preparar los datos agregados (para generar el modelo)](#bkmk_newReplaceData)  
  
3.  [Preparar los datos de series (para la predicción cruzada)](#bkmk_CrossData2)  
  
4.  [Predecir mediante EXTEND](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
5.  [Crear el modelo de predicción cruzada](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
6.  [Predecir con REPLACE](../../2014/tutorials/time-series-predictions-replacement-data-intermediate-data-mining.md)  
  
7.  [Revise las nuevas predicciones](../../2014/tutorials/comparing-predictions-for-forecasting-models-intermediate-data-mining-tutorial.md)  
  
##  <a name="bkmk_newExtendData"></a> Creación de nuevos datos extendidos de ventas  
 Para actualizar los datos de ventas, necesitará obtener las últimas cifras de ventas. Los datos que se acaban de introducir de la región del Pacífico son de interés particular. Allí se inició una promoción de ventas regional para llamar la atención sobre las nuevas tiendas y aumentar el conocimiento de sus productos.  
  
 En este escenario, asumiremos que los datos se han importado de un libro de Excel que contiene únicamente tres meses de los nuevos datos para un par de regiones. Creará una tabla para los datos mediante un script Transact-SQL y, a continuación, definirá una vista de origen de datos que usará para la predicción.  
  
#### <a name="create-the-table-with-new-sales-data"></a>Crear la tabla con nuevos datos de ventas  
  
1.  En una ventana de consulta de Transact-SQL, ejecute la instrucción siguiente para agregar los datos de ventas a la base de datos AdventureWorksDW (o a cualquier otra base de datos).  
  
    ```  
    USE [database name];  
    GO  
    IF OBJECT_ID ([dbo].[NewSalesData]) IS NOT NULL   
        DROP TABLE [dbo].[NewSalesData];  
    GO  
    CREATE TABLE [dbo].[NewSalesData]([Series] [nvarchar](255) NULL,  
    [NewDate] [datetime] NULL,  
    [NewQty] [float] NULL,  
    [NewAmount] [money] NULL) ON [PRIMARY]  
  
    GO  
    ```  
  
2.  Inserte los nuevos valores mediante el siguiente script.  
  
    ```  
    INSERT INTO [NewSalesData]  
    (Series,NewDate,NewQty,NewAmount)  
    VALUES('T1000 Pacific', '7/25/08', 55, '$130,170.22'),  
    ('T1000 Pacific', '8/25/08', 50, '$114,435.36 '),  
    ('T1000 Pacific', '9/25/08', 50, '$117,296.24 '),  
    ('T1000 Europe', '7/25/08', 37, '$88,210.00 '),  
    ('T1000 Europe', '8/25/08', 41, '$97,746.00 '),  
    ('T1000 Europe', '9/25/08', 37, '$88,210.00 '),  
    ('T1000 North America', '7/25/08', 69, '$164,500.00 '),  
    ('T1000 North America', '8/25/08', 66, '$157,348.00 '),  
    ('T1000 North America', '9/25/08', 58, '$138,276.00 '),  
    ('M200 Pacific', '7/25/08', 65, '$149,824.35'),  
    ('M200 Pacific', '8/25/08', 54,  '$124,619.46'),  
    ('M200 Pacific', '9/25/08', 61, '$141,143.39'),  
    ('M200 Europe', '7/25/08', 75, '$173,026.00'),  
    ('M200 Europe', '8/25/08', 76, '$175,212.00'),  
    ('M200 Europe', '9/25/08', 84, '$193,731.00'),  
    ('M200 North America', '7/25/08', 94, '$216,916.00'),  
    ('M200 North America', '8/25/08', 94, '$216,891.00'),  
    ('M200 North America', '9/25/08', 91,'$209,943.00');  
    ```  
  
    > [!WARNING]  
    >  Se usan comillas con los valores de moneda para evitar problemas con el separador de coma y el símbolo de moneda. También podría pasar los valores de moneda en este formato: `130170.22`  
    >   
    >  Observe que las fechas usadas en la base de datos de ejemplo han cambiado en esta versión. Si está usando una edición anterior de AdventureWorks, quizás necesite ajustar las fechas insertadas en consecuencia.  
  
###  <a name="bkmk_newReplaceData"></a> Crear una vista del origen de datos con nuevos datos de ventas  
  
1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Vistas del origen de datos**y, a continuación, seleccione **Nueva vista del origen de datos**.  
  
2.  En el Asistente para vistas del origen de datos, realice las selecciones siguientes:  
  
     **Origen de datos**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Seleccionar tablas y vistas**: seleccione la tabla que acaba de crear, NewSalesData.  
  
3.  Haga clic en **Finalizar**.  
  
4.  En la superficie de diseño de la vista del origen de datos, haga clic en NewSalesData y, a continuación, seleccione **explorar datos** para comprobar los datos.  
  
> [!WARNING]  
>  Usará estos datos solo para la predicción, por lo que no importa que sean incompletos.  
  
##  <a name="bkmk_CrossData2"></a> Creación de los datos para el modelo de predicción cruzada  
 Los datos que se usan en el original ya estaba el modelo de previsión agrupados de algún modo por la vista vTimeSeries que contraen los diversos modelos de bicicletas en un número menor de categorías y combinar los resultados de países individuales en las regiones. Para crear un modelo que se puede usar para las proyecciones mundiales, creará algunas agregaciones simples adicionales directamente en el Diseñador de vistas del origen de datos. La nueva vista del origen de datos contiene solo una suma y un promedio de las ventas de todos los productos para todas las regiones.  
  
 Después de crear el origen de datos usado para el modelo, debe crear una nueva vista del origen de datos que usará para la predicción. Por ejemplo, si desea predecir las ventas de Europa con el nuevo modelo mundial, debe suministrar los datos de la región de Europa solamente. De esta forma, configurará una nueva vista del origen de datos que filtra los datos originales y cambiará la condición de filtro para cada conjunto de consultas de predicción.  
  
#### <a name="to-create-the-model-data-using-a-custom-data-source-view"></a>Para crear los datos del modelo mediante una vista personalizada del origen de datos  
  
1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Vistas del origen de datos**y, a continuación, seleccione **Nueva vista del origen de datos**.  
  
2.  En la página de bienvenida del asistente, haga clic en **Siguiente**.  
  
3.  En el **Seleccionar origen de datos** , seleccione [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]y, a continuación, haga clic en **siguiente**.  
  
4.  En la página, **Seleccionar tablas y vistas**, no agregue ninguna tabla; sólo haga clic en **Siguiente**.  
  
5.  En la página, **completando el Asistente para**, escriba el nombre `AllRegions`y, a continuación, haga clic en **finalizar**.  
  
6.  Después, haga clic con el botón secundario en la superficie de diseño de la vista del origen de datos en blanco y seleccione **Nueva consulta con nombre**.  
  
7.  En el **crear consulta con nombre** cuadro de diálogo para **nombre**, tipo `AllRegions`y para **descripción**, tipo **suma y promedio de ventas para todos los modelos y regiones**.  
  
8.  En el panel de texto SQL, escriba la siguiente instrucción y, a continuación, haga clic en Aceptar:  
  
    ```  
    SELECT ReportingDate,   
    SUM([Quantity]) as SumQty, AVG([Quantity]) as AvgQty,  
    SUM([Amount]) AS SumAmt, AVG([Amount]) AS AvgAmt,  
    'All Regions' as [Region]  
    FROM dbo.vTimeSeries   
    GROUP BY ReportingDate  
    ```  
  
9. Haga clic en el `AllRegions` de tabla y, a continuación, seleccione **explorar datos**.  
  
###  <a name="bkmk_CrossData"></a> Para crear los datos de serie para la predicción cruzada  
  
1.  En el **Explorador de soluciones**, haga clic con el botón secundario en **Vistas del origen de datos**y, a continuación, seleccione **Nueva vista del origen de datos**.  
  
2.  En el Asistente para vistas del origen de datos, realice las selecciones siguientes:  
  
     **Origen de datos**: [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]  
  
     **Seleccionar tablas y vistas**: no seleccione ninguna tabla  
  
     **Nombre**: `T1000 Pacific Region`  
  
3.  Haga clic en **Finalizar**.  
  
4.  Haga clic con el botón secundario en la superficie de diseño vacía correspondiente a **T1000 Pacific Region.dsv**y, después, seleccione **Nueva consulta con nombre**.  
  
     Aparecerá el cuadro de diálogo **Crear consulta con nombre** . Vuelva a escribir el nombre y agregue la descripción siguiente:  
  
     **Nombre**: `T1000 Pacific Region`  
  
     **Descripción**: **filtro`vTimeSeries`por región y modelo**  
  
5.  En el panel de texto, escriba la siguiente consulta y, a continuación, haga clic en Aceptar:  
  
    ```  
    SELECT ReportingDate, ModelRegion, Quantity, Amount  
    FROM dbo.vTimeSeries  
    WHERE (ModelRegion = N'T1000 Pacific')  
    ```  
  
    > [!NOTE]  
    >  Puesto que deberá crear predicciones para cada serie por separado, puede que desee copiar el texto de la consulta y guardarlo en un archivo de texto para poder usarlo de nuevo con la otra serie de datos.  
  
6.  En la superficie de diseño de la vista del origen de datos, haga clic en T1000 Pacific y, a continuación, seleccione **explorar datos** para comprobar que los datos se filtran correctamente.  
  
     Usará estos datos como la entrada del modelo al crear consultas de predicción cruzada.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Usan datos actualizados de predicciones de serie temporal &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/time-series-predictions-using-updated-data-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)   
 [Referencia técnica del algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md)   
 [Vistas del origen de datos en modelos multidimensionales](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
