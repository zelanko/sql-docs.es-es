---
title: Crear predicciones para los modelos de centro de llamadas (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5be0cec7-f639-4eeb-835e-e3204ae619e9
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 86ac24e1c67d062a0b9d0c2b9d2963bd9b8a479d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321505"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>Crear predicciones para los modelos de centro de llamadas (Tutorial intermedio de minería de datos)
  Ahora que ha aprendido algo acerca de las interacciones entre los turnos, el número de operadores, las llamadas y el grado de servicio, está en disposición de crear algunas consultas de predicción que se puedan usar en el análisis y el planeamiento empresarial. Primero, creará algunas predicciones en el modelo de exploración para probar varias suposiciones. A continuación, creará predicciones masivas usando el modelo de regresión logística.  
  
 En esta lección se presupone que ya está familiarizado con el concepto de consultas de predicción.  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>Crear predicciones utilizando el modelo de red neuronal  
 En el ejemplo siguiente se demuestra cómo crear una predicción singleton usando el modelo de red neuronal que se creó para la exploración. Las predicciones singleton constituyen un buen modo de probar valores diferentes para comprobar el efecto en el modelo. En este escenario, predecirá el grado de servicio para el turno de medianoche (no se especifica el día de la semana) si hay seis operadores experimentados de servicio.  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>Para crear una consulta singleton con el modelo de red neuronal  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución que contiene el modelo que desea usar.  
  
2.  En el Diseñador de minería de datos, haga clic en el **predicción de modelo de minería de datos** ficha.  
  
3.  En el **Mining Model** panel, haga clic en **Seleccionar modelo**.  
  
4.  El **Seleccionar modelo de minería de datos** cuadro de diálogo muestra una lista de estructuras de minería de datos. Expanda la estructura de minería de datos para ver una lista de modelos de minería de datos asociados con esa estructura.  
  
5.  Expanda la estructura de minería de datos Call Center Default y seleccione el modelo de red neuronal Call Center - LR.  
  
6.  En el menú **Modelo de minería de datos** , seleccione **Consulta singleton**.  
  
     El **entrada de consulta Singleton** aparece el cuadro de diálogo, con columnas asignadas a las columnas en el modelo de minería de datos.  
  
7.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en la fila de la tecla MAYÚS y, a continuación, seleccione *medianoche*.  
  
8.  Haga clic en la fila para los operadores de nivel 2 y tipo `6`.  
  
9. En la parte inferior de la mitad el **predicción de modelo de minería de datos** pestaña, haga clic en la primera fila de la cuadrícula.  
  
10. En el **origen** columna, haga clic en la flecha hacia abajo y seleccione **función de predicción**. En el **campo** columna, seleccione **PredictHistogram**.  
  
     Aparece una lista de argumentos que se pueden utilizar con esta función de predicción automáticamente en el **criterios o argumentos** cuadro.  
  
11. Arrastre la columna ServiceGrade de la lista de columnas en el **Mining Model** panel a la **criterios o argumentos** cuadro.  
  
     El nombre de la columna se inserta automáticamente como argumento. Puede elegir cualquier columna de atributo de predicción para arrastrarla a este cuadro de texto.  
  
12. Haga clic en el botón **cambiar a la consulta da como resultado de la vista**, en la esquina superior del generador de consultas de predicción.  
  
 Los resultados esperados contienen los posibles valores de predicción de cada grado de servicio, dadas estas entradas, junto con los valores de compatibilidad y probabilidad de cada predicción. Puede volver a la vista de diseño en cualquier momento y cambiar las entradas o agregar más.  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>Crear predicciones mediante un modelo de regresión logística  
 Si ya conoce los atributos que son pertinentes para el problema empresarial, puede usar un modelo de regresión logística con el fin de predecir el efecto de realizar cambios en ciertos atributos. La regresión logística es un método estadístico que se utiliza normalmente para realizar predicciones en función de cambios en variables independiente. Se usa, por ejemplo, en la evaluación financiera, para predecir el comportamiento de los clientes en función de datos estadísticos.  
  
 En esta tarea aprenderá a crear un origen de datos que se usará en las predicciones y hará que estas sirvan de ayuda para responder varias cuestiones empresariales.  
  
### <a name="generating-data-used-for-bulk-prediction"></a>Generar datos usados para la predicción masiva  
 Hay muchas formas de proporcionar datos de entrada: por ejemplo, podría importar niveles que proveían de personal de una hoja de cálculo y ejecutar los datos a través del modelo para predecir la calidad de servicio del mes próximo.  
  
 En esta lección, usará el diseñador de vista del origen de datos para crear una consulta con nombre. Esta consulta es una instrucción Transact-SQL personalizada que calcula, para cada turno de la programación, el número máximo de operadores del personal, el mínimo de llamadas recibidas y el número promedio de problemas que se generan. A continuación combinará esos datos en un modelo de minería de datos para realizar predicciones acerca de una serie de fechas próximas.  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>Para generar datos de entrada de una consulta de predicción masiva  
  
1.  En el Explorador de soluciones, haga clic en **vistas del origen de datos**y, a continuación, seleccione **nueva vista del origen de datos**.  
  
2.  En el Asistente para la vista del origen de datos, seleccione [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] como origen de datos y, a continuación, haga clic en **siguiente**.  
  
3.  En el **seleccionar tablas y vistas** página, haga clic en **siguiente** sin seleccionar ninguna tabla.  
  
4.  En el **completando el Asistente para** página, escriba el nombre, `Shifts`.  
  
     Este nombre aparecerá en el Explorador de soluciones como nombre de la vista del origen de datos.  
  
5.  Haga clic en el panel de diseño vacía y luego seleccione **nueva consulta con nombre**.  
  
6.  En el **crear consulta con nombre** cuadro de diálogo para **nombre**, tipo `Shifts for Call Center`.  
  
     Este nombre aparecerá en el diseñador de vistas del origen de datos como nombre de la consulta con nombre.  
  
7.  Pegue la instrucción de consulta siguiente en el panel de texto SQL en la mitad inferior del cuadro de diálogo.  
  
    ```  
    SELECT DISTINCT WageType, Shift,   
    AVG(Orders) as AvgOrders, MIN(Orders) as MinOrders, MAX(Orders) as MaxOrders,  
    AVG(Calls) as AvgCalls, MIN(Calls) as MinCalls, MAX(Calls) as MaxCalls,  
    AVG(LevelTwoOperators) as AvgOperators, MIN(LevelTwoOperators) as MinOperators, MAX(LevelTwoOperators) as MaxOperators,  
    AVG(IssuesRaised) as AvgIssues, MIN(IssuesRaised) as MinIssues, MAX(IssuesRaised) as MaxIssues  
    FROM dbo.FactCallCenter  
    GROUP BY Shift, WageType  
    ```  
  
8.  En el panel de diseño, haga clic en la tabla turnos del centro de llamadas y seleccione **explorar datos** para obtener una vista previa de los datos tal como lo devuelve la consulta de Transact-SQL.  
  
9. Haga clic en la ficha, **turnos.DSV (diseño),** y, a continuación, haga clic en **guardar** para guardar la nueva definición de vista del origen de datos.  
  
### <a name="predicting-service-metrics-for-each-shift"></a>Predecir la métrica de servicio de cada turno  
 Ahora que ha generado algunos valores para cada turno, los usará como entrada del modelo de regresión logística que ha creado, con el fin de generar algunas predicciones que se puedan usar en la planificación empresarial.  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>Para utilizar el nuevo DSV como entrada de una consulta de predicción  
  
1.  En el Diseñador de minería de datos, haga clic en el **predicción de modelo de minería de datos** ficha.  
  
2.  En el **Mining Model** panel, haga clic en **Seleccionar modelo**y elija Call Center - LR en la lista de modelos disponibles.  
  
3.  Desde el **Mining Model** menú, desactive la opción, **consulta Singleton**. Una advertencia indica que se perderán las entradas de la consulta singleton. Haga clic en **Aceptar**.  
  
     El **entrada de consulta Singleton** cuadro de diálogo se reemplaza por la **Seleccionar tabla (s) de entrada** cuadro de diálogo.  
  
4.  Haga clic en **Seleccionar tabla de casos**.  
  
5.  En el **Seleccionar tabla** cuadro de diálogo, selectShifts en la lista de orígenes de datos. En el **nombre de tabla o vista** lista, seleccione turnos del centro de llamadas (podría seleccionarse automáticamente) y, a continuación, haga clic en **Aceptar.**  
  
     El **predicción de modelo de minería de datos** superficie de diseño se actualiza para mostrar las asignaciones creadas según los tipos de datos y los nombres de las columnas de los datos de entrada y el modelo.  
  
6.  Haga clic en una de las líneas de combinación y, a continuación, seleccione **modificar conexiones**.  
  
     En este cuadro de diálogo puede ver exactamente qué columnas se asignan y cuáles no. El modelo de minería de datos contiene las columnas Calls, Orders, IssuesRaised y LvlTwoOperators, que puede asignar a cualquiera de los agregados que creó según estas columnas del origen de datos. En este escenario, asignará los promedios.  
  
7.  Haga clic en la celda vacía situada junto a LevelTwoOperators y seleccione **Shifts for Call Center.AvgOperators**.  
  
8.  Haga clic en la celda vacía situada junto a Calls, seleccione **Shifts for Call Center.AvgCalls**. y, a continuación, haga clic en **Aceptar**.  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>Para crear las predicciones de cada turno  
  
1.  En la cuadrícula en la parte inferior de la mitad de la **generador de consultas de predicción**, haga clic en la celda vacía bajo **origen,** y, a continuación, seleccione turnos del centro de llamadas.  
  
2.  En la celda vacía debajo **campo**, seleccione Shift.  
  
3.  Haga clic en la siguiente línea vacía de la cuadrícula y repita el procedimiento descrito para agregar otra fila para WageType.  
  
4.  Haga clic en la siguiente línea vacía de la cuadrícula. En el **origen** columna, seleccione **función de predicción**. En el **campo** columna, seleccione **Predict**.  
  
5.  Arrastre la columna ServiceGrade desde el **Mining Model** panel hasta la cuadrícula y en el **criterios o argumento** celda. En el **Alias** , escriba **Predicted Service Grade**.  
  
6.  Haga clic en la siguiente línea vacía de la cuadrícula. En el **origen** columna, seleccione **función de predicción**. En el **campo** columna, seleccione **PredictProbability**.  
  
7.  Arrastre la columna ServiceGrade desde el **Mining Model** panel hasta la cuadrícula y en el **criterios o argumento** celda. En el **Alias** , escriba **probabilidad**.  
  
8.  Haga clic en **cambiar a vista de resultado de consulta** para ver las predicciones.  
  
 La siguiente tabla muestra los resultados de ejemplo de cada turno.  
  
|Shift|WageType|Predicted Service Grade|Probabilidad|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|holiday|0.165|0.377520666|  
|midnight|holiday|0.105|0.364105573|  
|PM1|holiday|0.165|0.40056055|  
|PM2|holiday|0.165|0.338532973|  
|AM|weekday|0.165|0.370847617|  
|midnight|weekday|0,08|0.352999173|  
|PM1|weekday|0.165|0.317419177|  
|PM2|weekday|0.105|0.311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>Predecir el efecto del tiempo de respuesta reducido en la calificación del servicio  
 Ha generado algunos valores de promedio para cada turno y los ha usado como entrada del modelo de regresión logística. Sin embargo, dado que el objetivo de la empresa es mantener la tasa de abandonos dentro del intervalo 0,00-0,05, los resultados no son esperanzadores.  
  
 Por lo tanto, según el modelo original, que mostraba una gran influencia del tiempo de respuesta en la calificación del servicio, el equipo de operaciones decide realizar algunas predicciones para valorar si la reducción del tiempo promedio de respuesta a las llamadas podría mejorar la calificación del servicio. Por ejemplo, ¿qué ocurriría si se recorta el tiempo de respuesta en un 90% o incluso un 80% del tiempo actual de respuesta de las llamadas?, ¿qué ocurriría con los valores de calificación del servicio?  
  
 Es fácil crear una vista del origen de datos (DSV) que calcule el tiempo de respuesta promedio de cada turno y, a continuación, agregar columnas que calculen el 80% o 90% del tiempo de respuesta promedio. A continuación, puede utilizar la vista del origen de datos para el modelo.  
  
 Aunque los pasos exactos no se muestran aquí, en la tabla siguiente se comparan los efectos en la calificación del servicio cuando se reduce el tiempo de respuesta en un 80% o 90% de los tiempos de respuesta actuales.  
  
 A partir de estos resultados, podría concluir que, en los turnos de destino, debe reducir el tiempo de respuesta en un 90 por ciento de la tasa actual para mejorar la calidad del servicio.  
  
|Turno, salario y día|Calidad prevista del servicio con el tiempo de respuesta promedio actual|Calidad prevista del servicio con reducción del 90 por ciento en tiempo de respuesta|Calidad prevista del servicio con reducción en un 80 del tiempo de respuesta|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|Holiday AM|0.165|0.05|0.05|  
|Holiday PM1|0.05|0.05|0.05|  
|Holiday Midnight|0.165|0.05|0.05|  
  
 Hay varias consultas de predicción diferentes que puede crear en este modelo. Por ejemplo, podría predecir cuántos operadores son necesarios para cumplir un cierto nivel de servicio o para responder a un determinado número de llamadas entrantes. Dado que puede incluir varias salidas en un modelo de regresión logística, es fácil experimentar con variables independientes y resultados diferentes sin tener que crear varios modelos distintos.  
  
## <a name="remarks"></a>Notas  
 Los complementos de minería de datos para Excel 2007 ofrecen asistentes de regresión logística que facilitan el poder responder a cuestiones complejas, como cuántos operadores de nivel dos se necesitarían para mejorar el grado de servicio a un nivel determinado para un turno concreto. Los complementos de minería de datos se pueden descargar de forma gratuita e incluyen asistentes que se basan en los algoritmos de red neuronal o de regresión logística. Para obtener más información, vea los siguientes vínculos:  
  
-   [SQL Server 2005 Data minería complementos para Office 2007](http://www.microsoft.com/sql/technologies/dm/addins.mspx): Buscar objetivo y ¿qué ocurre si el análisis de escenario  
  
-   [SQL Server 2008 datos minería complementos para Office 2007](http://go.microsoft.com/fwlink/?LinkID=117790): Buscar objetivo análisis de escenario, ¿qué ocurre si el análisis de escenario y cálculo de predicción  
  
## <a name="conclusion"></a>Conclusión  
 Ha aprendido a crear, personalizar e interpretar los modelos de minería de datos que se basan en los algoritmos de red neuronal y/o de regresión logística de Microsoft. Estos tipos de modelos son sofisticados y permiten una variedad casi infinita de análisis, y, por tanto, pueden ser complejos y difíciles de dominar.  
  
 Sin embargo, estos algoritmos pueden recorrer muchas combinaciones de factores e identificar automáticamente las correlaciones más marcadas, lo que proporciona datos estadísticos para obtener una idea clara que sería muy difícil de detectar con la exploración manual de datos mediante Transact-SQL o incluso PowerPivot.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consultas de modelo de regresión logística](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Algoritmo de regresión logística de Microsoft](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Algoritmo de red neuronal de Microsoft](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [Ejemplos de consultas de modelos de red neuronal](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
