---
title: Descripción de los requisitos para una serie temporal de modelo (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1ce2b3e3-108a-4f7e-985f-a20b816d0da7
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 5b3438e832f28329cb0fec764d3a4846bae18ede
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043121"
---
# <a name="understanding-the-requirements-for-a-time-series-model-intermediate-data-mining-tutorial"></a>Descripción de los requisitos de un modelo de serie temporal (tutorial intermedio de minería de datos)
  Cuando vaya a preparar datos para un modelo de pronóstico, debe asegurarse de que los datos contengan una columna que se pueda usar para identificar los pasos en la serie temporal. Esa columna se definirá como columna `Key Time`. Dado que es una clave, la columna debe contener valores numéricos únicos.  
  
 La elección de la unidad correcta para la columna `Key Time` es una parte importante del análisis. Por ejemplo, suponga que los datos de ventas se actualizarán a cada minuto. No sería necesario usar minutos como unidad de la serie temporal; podría ser más relevante acumular los datos de ventas por día, semana o incluso mes. Si no está seguro de qué unidad de tiempo debe usar, puede crear una nueva vista del origen de datos para cada agregación y compilar modelos relacionados para ver si surgen distintas tendencias en cada nivel de agregación.  
  
 Para este tutorial, los datos de ventas se recopilan diariamente en la base de datos transaccional de ventas, pero para la minería de datos, los datos se han agregado previamente por mes mediante una vista.  
  
 Además, es conveniente para el análisis que los datos tengan tan pocos huecos como sea posible. Si piensa analizar varias series de datos, todas ellas deben empezar y terminar preferiblemente en la misma fecha. Si faltan datos que no corresponden al comienzo o al final de una serie, puede usar el parámetro MISSING_VALUE_SUBSTITUTION para rellenar la serie. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] también proporciona varias opciones para reemplazar los datos que faltan por valores, como medias o constantes.  
  
> [!WARNING]  
>  Las herramientas de gráfico dinámico y tabla dinámica que se incluyeron en versiones anteriores del diseñador de vistas de origen de datos ya no se proporcionan. Se recomienda identificar los huecos en los datos de serie temporal de antemano, mediante herramientas tales como el generador de perfiles de datos incluido en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-identify-the-time-key-for-the-forecasting-model"></a>Para identificar la clave temporal del modelo de pronóstico  
  
1.  En el panel, **SalesByRegion.dsv [Diseño]** , haga clic en la tabla vTimeSeries y, a continuación, seleccione **explorar datos**.  
  
     Una nueva ficha se abre, **explorar la tabla vTimeSeries**.  
  
2.  En el **tabla** pestaña, revise los datos que se usan en las columnas TimeIndex y Reporting Date.  
  
     Ambas son secuencias con valores únicos y se pueden usar como clave de serie temporal; sin embargo, los tipos de datos de las columnas son distintos. El algoritmo de serie temporal de Microsoft no requiere un tipo de datos `datetime`; solo exige que los valores sean distintos y estén ordenados. Por tanto, se puede utilizar cualquier columna como clave temporal para el modelo de pronóstico.  
  
3.  En la superficie de diseño de vista del origen de datos, seleccione la columna, Reporting Date y seleccione **propiedades**. A continuación, haga clic en la columna TimeIndex y seleccione **propiedades**.  
  
     El campo TimeIndex tiene el tipo de datos System.Int32, mientras que el campo Reporting Date tiene los datos de tipo System.DateTime. Muchos almacenamientos de datos convierten los valores de fecha y hora en enteros y usan la columna de enteros como clave para mejorar el rendimiento de la indización. Sin embargo, si usa esta columna, el algoritmo de serie temporal de Microsoft realizará las predicciones con valores futuros como 201014, 201014, etc. Dado que desea representar los datos de ventas mediante fechas del calendario de previsión, utilizará la columna Reporting Date como el identificador de serie únicos.  
  
### <a name="to-set-the-key-in-the-data-source-view"></a>Para establecer la clave en la vista del origen de datos  
  
1.  En el panel **SalesByRegion.dsv**, seleccione la tabla vTimeSeries.  
  
2.  Haga clic en la columna, Reporting Date y seleccione **establecer clave principal lógica**.  
  
## <a name="handling-missing-data-optional"></a>Manejar la ausencia de datos (opcional)  
 Si faltan datos en alguna serie, puede aparecer un error al intentar procesar el modelo. Existen varias formas de solucionar la ausencia de datos:  
  
-   Puede hacer que Analysis Services rellene los valores que faltan, ya sea mediante el cálculo de la media o mediante un valor anterior. Para ello, establezca el parámetro MISSING_VALUE_SUBSTITUTION en el modelo de minería de datos. Para obtener más información acerca de este parámetro, vea [Microsoft Time Series Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm-technical-reference.md). Para obtener información acerca de cómo cambiar los parámetros de un modelo de minería de datos existente, vea [ver o cambiar parámetros del algoritmo](../../2014/analysis-services/data-mining/view-or-change-algorithm-parameters.md).  
  
-   Puede modificar el origen de datos o filtrar la vista subyacente para eliminar la serie irregular o reemplazar los valores. Esto se puede hacer en el origen de datos relacionales, o bien puede modificar la vista del origen de datos creando consultas con nombre personalizadas o cálculos con nombre. Para más información, vea [Vistas del origen de datos en modelos multidimensionales](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md). En la última tarea de esta lección se proporciona un ejemplo de cómo generar una consulta con nombre y un cálculo personalizado.  
  
 En este escenario, faltan algunos datos al principio de una serie; es decir, no hay datos para la línea de productos T1000 hasta julio de 2007. Por lo demás, todas las series terminan en la misma fecha y no falta ningún valor.  
  
 El requisito del algoritmo de serie temporal de Microsoft es que cualquier serie que se incluya en un modelo único debe tener el mismo **final** punto. Como el modelo de bicicletas T1000 se introdujo en 2007, los datos de esta serie empiezan después que los de otros modelos de bicicletas, pero la serie termina en la misma fecha; por tanto, se pueden usar los datos.  
  
#### <a name="to-close-the-data-source-view-designer"></a>Para cerrar el diseñador de vistas del origen de datos  
  
-   Haga clic en la ficha, **explorar la tabla vTimeSeries**y seleccione **cerrar**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear una estructura de previsión y un modelo &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Algoritmo de serie temporal de Microsoft](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
