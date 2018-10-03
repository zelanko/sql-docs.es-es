---
title: Predecir asociaciones (Tutorial de minería de datos intermedios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 09084760637464c5e985eeb17762959c8576c5ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222811"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>Predecir asociaciones (Tutorial intermedio de minería de datos)
  Una vez procesados los modelos, puede utilizar la información sobre las asociaciones almacenada en el modelo para crear predicciones. En la tarea final de esta lección, aprenderá a generar consultas de predicción a partir de los modelos de asociación que creó. En esta lección se presupone que sabe cómo se utiliza el Generador de consultas de predicción y desea obtener información acerca de cómo se generan consultas de predicción a partir de modelos de asociación. Para obtener más información cómo usar el generador de consultas de predicción, vea [Interfaces de consultas de minería de datos](../../2014/analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="creating-a-singleton-prediction-query"></a>Crear una consulta de predicción singleton  
 Las consultas de predicción en un modelo de asociación pueden ser muy útiles para lo siguiente:  
  
-   Recomendar artículos a un cliente, en función de compras anteriores o relacionadas.  
  
-   Buscar eventos relacionados.  
  
-   identificar relaciones en o entre conjuntos de transacciones.  
  
 Para generar una consulta de predicción, seleccione primero el modelo de asociación que desee utilizar, y, a continuación, especifique los datos de entrada. Las entradas pueden proceder de un origen de datos externo, como una lista de valores. También puede generar una consulta singleton y proporcionar los valores sobre la marcha.  
  
 En este escenario, creará primero algunas consultas de predicción singleton para hacerse una idea de cómo funcionan las predicciones. A continuación, creará una consulta de las predicciones masivas que podría utilizar para hacer recomendaciones en función de las compras realizadas actualmente por un cliente.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>Para crear una consulta de predicción en un modelo de asociación  
  
1.  Haga clic en el **predicción de modelo de minería de datos** ficha del Diseñador de minería de datos.  
  
2.  En el **Mining Model** panel, haga clic en **Seleccionar modelo**. (Puede omitir este paso y el siguiente si el modelo correcto ya está seleccionado).  
  
3.  En el **Seleccionar modelo de minería de datos** diálogo cuadro, expanda el nodo que representa la estructura de minería de datos **asociación**y seleccione el modelo **asociación**. Haga clic en **Aceptar**.  
  
     De momento, puede hacer caso omiso al panel de entrada.  
  
4.  En la cuadrícula, haga clic en la celda vacía bajo **origen** y seleccione **función de predicción.** En la celda bajo **campo**, seleccione `PredictAssociation`.  
  
     También puede usar el **Predict** función para predecir las asociaciones. Si lo hace, asegúrese que elija la versión de la **Predict** función que toma una columna de tabla como argumento.  
  
5.  En el **Mining Model** panel, seleccione la tabla anidada `vAssocSeqLineItems`y arrástrela hasta la cuadrícula, al **criterios o argumento** cuadro para el `PredictAssociation` función.  
  
     Al arrastrar y colocar la tabla y los nombres de columna, podrá crear instrucciones complejas sin errores sintácticos. Sin embargo, se reemplazará el contenido actual de la celda, que contiene otros argumentos opcionales para el `PredictAssociation` función. Para consultar los demás argumentos, puede agregar provisionalmente una segunda instancia de la función a la cuadrícula como referencia.  
  
6.  Haga clic en el **criterios o argumento** cuadro y escriba el texto siguiente después del nombre de tabla: `,3`  
  
     El texto completo en el **criterios o argumento** cuadro debería ser como sigue:  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  Haga clic en el **resultados** situado en la esquina superior del generador de consultas de predicción.  
  
 Los resultados esperados contienen una sola columna con el encabezado **expresión**. El **expresión** columna contiene una tabla anidada con una sola columna y las siguientes tres filas. Como no especificó un valor de entrada, estas predicciones representan las asociaciones de productos del modelo en su conjunto que tienen mayor probabilidad de producirse.  
  
|Modelo|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 A continuación, usará el **entrada de consulta Singleton** panel para especificar un producto como entrada para la consulta y ver los productos que tienen más probabilidades asociadas con ese elemento.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>Para crear una consulta de predicción singleton con entradas de tabla anidada  
  
1.  Haga clic en el **diseño** situado en la esquina del generador de consultas de predicción para volver a la cuadrícula de generación de consultas.  
  
2.  En el **Mining Model** menú, seleccione **consulta Singleton**.  
  
3.  En el **Mining Model** cuadro de diálogo, seleccione el **asociación** modelo.  
  
4.  En la cuadrícula, haga clic en la celda vacía bajo **origen** y seleccione **función de predicción.** En la celda bajo **campo**, seleccione `PredictAssociation`.  
  
5.  En el **Mining Model** panel, seleccione la tabla anidada `vAssocSeqLineItems`y arrástrela hasta la cuadrícula, al **criterios o argumento** cuadro para el `PredictAssociation` función. Tipo `,3` después del nombre de tabla anidada, al igual que en el procedimiento anterior.  
  
6.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en el **valor** situada al lado **vAssoc Seq Line Items**y, a continuación, haga clic en el **(...)**  botón.  
  
7.  En el **entrada de tabla anidada** cuadro de diálogo, seleccione `Touring Tire` en el **columna clave** panel y, a continuación, haga clic en **agregar**.  
  
8.  Haga clic en el **resultados** botón.  
  
 Los resultados muestran ahora las predicciones de los productos que con mayor probabilidad estarán asociados a Touring Tire.  
  
|Modelo|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 Sin embargo, al explorar el modelo sabrá ya que Touring Tire Tube a menudo se compra junto con Touring Tire; lo que más le interesa saber es qué productos puede recomendar a los clientes que compran estos dos artículos juntos. Cambiará la consulta para que prediga productos relacionados en función de dos elementos de la cesta. Modificará también la consulta para agregar la probabilidad de cada producto predicho.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>Para agregar entradas y probabilidades a la consulta de predicción singleton  
  
1.  Haga clic en el **diseño** situado en la esquina del generador de consultas de predicción para volver a la cuadrícula de generación de consultas.  
  
2.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en el **valor** situada al lado **vAssoc Seq Line Items**y, a continuación, haga clic en el **(...)**  botón.  
  
3.  En el **columna clave** panel, seleccione `Touring Tire`y, a continuación, haga clic en **agregar**.  
  
4.  En la cuadrícula, haga clic en la celda vacía bajo **origen** y seleccione **función de predicción.** En la celda bajo **campo**, seleccione `PredictAssociation`.  
  
5.  En el **Mining Model** panel, seleccione la tabla anidada `vAssocSeqLineItems`y arrástrela hasta la cuadrícula, al **criterios o argumento** cuadro para el `PredictAssociation` función. Tipo `,3` después del nombre de tabla anidada, al igual que en el procedimiento anterior.  
  
6.  En el **entrada de tabla anidada** cuadro de diálogo, seleccione `Touring Tire Tube` en el **columna clave** panel y, a continuación, haga clic en **agregar**.  
  
7.  En la cuadrícula, en la fila de la `PredictAssociation` de función, haga clic en el **criterios o argumento** cuadro y cambie los argumentos para agregar el argumento INCLUDE_STATISTICS.  
  
     El texto completo en el **criterios o argumento** cuadro debería ser como sigue:  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  Haga clic en el **resultados** botón.  
  
 Los resultados de la tabla anidada se modifican ahora para mostrar las predicciones, junto con la compatibilidad y probabilidad. Para obtener más información sobre cómo interpretar estos valores, vea [Mining Model Content los modelos de asociación &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291...|0.252...|  
|Water Bottle|2866|0,192...|0.175...|  
|Patch Kit|2113|0,142...|0.132|  
  
## <a name="working-with-results"></a>Trabajar con resultados  
 Cuando hay muchas tablas anidadas en los resultados, es posible que desee simplificar los resultados para facilitar su consulta. Para ello, puede modificar la consulta manualmente y agregar la palabra clave `FLATTENED`.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para simplificar los conjuntos de filas anidados de una consulta de predicción  
  
1.  Haga clic en el **SQL** situado en la esquina del generador de consultas de predicción.  
  
     La cuadrícula cambia a un panel abierto donde puede ver y modificar la instrucción DMX que creó el Generador de consultas de predicción.  
  
2.  Después de la palabra clave `SELECT`, escriba `FLATTENED`.  
  
     El texto completo de la consulta debería ser el siguiente:  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  Haga clic en el **resultados** situado en la esquina superior del generador de consultas de predicción.  
  
 Tenga en cuenta que después de editar una consulta manualmente, no podrá volver a cambiar a la vista Diseño sin perder los cambios. Si desea guardar la consulta, puede copiar la instrucción DMX que creó manualmente en un archivo de texto. Cuando cambie de nuevo a la vista Diseño, la consulta se revertirá a la última versión que fue válida en la vista Diseño.  
  
## <a name="creating-multiple-predictions"></a>Crear varias predicciones  
 Suponga que desea conocer las mejores predicciones de cada cliente en función de las compras realizadas en el pasado. Puede utilizar datos externos como entrada de la consulta de predicción, por ejemplo, tablas que contengan el identificador del cliente y las compras más recientes de productos. Los requisitos son que las tablas de datos ya estén definidas como una vista del origen de datos de Analysis Services; por otro lado, los datos de entrada deben contener una tabla de casos y una tabla anidada como las utilizadas en el modelo. No es necesario que tengan el mismo nombre, pero la estructura debe ser similar. Para los objetivos de este tutorial, utilizará las tablas originales en las que se entrenó el modelo.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>Para cambiar el método de entrada de la consulta de predicción  
  
1.  En el **Mining Model** menú, seleccione **consulta Singleton** nuevo, para borrar la marca de verificación.  
  
2.  Aparecerá un mensaje de error en el que se advierte que se perderá la consulta singleton. Haga clic en **Sí**.  
  
     El nombre del cuadro de diálogo de entrada cambia a **seleccionar tablas de entrada**.  
  
 Dado que lo que le interesa es crear una consulta de predicción que proporcione un identificador de cliente y una lista de productos como entrada, incorporará la tabla de clientes como la tabla de casos y la tabla de compras como la tabla anidada. A continuación, agregará las funciones de predicción para crear recomendaciones.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para crear una consulta de predicción utilizando las entradas de una tabla anidada  
  
1.  En el panel Modelo de minería de datos, seleccione el modelo Association Filtered.  
  
2.  En el **Seleccionar tabla (s) de entrada** cuadro de diálogo, haga clic en **Seleccionar tabla de casos**.  
  
3.  En el **Seleccionar tabla** cuadro de diálogo para **origen de datos**, seleccione AdventureWorksDW2008. En el **nombre de tabla o vista** lista, seleccione vAssocSeqOrders y, a continuación, haga clic en **Aceptar**.  
  
     La tabla vAssocSeqOrders se agrega al panel.  
  
4.  En el **Seleccionar tabla (s) de entrada** cuadro de diálogo, haga clic en **Seleccionar tabla anidada**.  
  
5.  En el **Seleccionar tabla** cuadro de diálogo para **origen de datos**, seleccione AdventureWorksDW2008. En el **nombre de tabla o vista** lista, seleccione Vassocseqlineitem y, a continuación, haga clic en **Aceptar**.  
  
     La tabla vAssocSeqLineItems se agrega al panel.  
  
6.  En el **especificar combinación anidada** cuadro de diálogo, arrastre el OrderNumber el campo de la tabla de casos y colóquelo en el campo OrderNumber de la tabla anidada.  
  
     También puede hacer clic en **agregar relación** y crear la relación seleccionando las columnas de una lista.  
  
7.  En el **especificar relación** diálogo cuadro, compruebe que los campos OrderNumber están asignados correctamente y, a continuación, haga clic en **Aceptar**.  
  
8.  Haga clic en **Aceptar** para cerrar el **especificar combinación anidada** cuadro de diálogo.  
  
     La tabla anidada y la tabla de casos se actualizan en el panel de diseño para mostrar las combinaciones que conectan las columnas de datos externos con las columnas del modelo. Si las relaciones son erróneas, puede haga clic en la línea de combinación y seleccionar **modificar conexiones** para editar la columna asignación, o haga clic en la línea de combinación y seleccionar **eliminar** para quitar el relación completamente.  
  
9. Agregue una nueva fila a la cuadrícula. Para **origen**, seleccione **tabla vAssocSeqOrders**. Para **campo**, seleccione CustomerKey.  
  
10. Agregue una nueva fila a la cuadrícula. Para **origen**, seleccione **tabla vAssocSeqOrders**. Para **campo**, seleccione la región.  
  
11. Agregue una nueva fila a la cuadrícula. Para **origen**, seleccione **función de predicción**y para **campo**, seleccione `PredictAssociation`.  
  
12. Arrastre vAssocSeqLineItems al **criterios o argumento** cuadro de la `PredictAssociation` fila. Haga clic al final de la **criterios o argumento** cuadro y, a continuación, escriba el texto siguiente: `INCLUDE_STATISTICS,3`  
  
     El texto completo en el **criterios o argumento** cuadro debe ser: `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. Haga clic en el **resultado** botón para ver las predicciones para cada cliente.  
  
 Puede intentar crear una consulta de predicción similar en varios modelos para ver si al aplicar filtros, cambian los resultados de predicción. Para obtener más información sobre cómo crear predicciones y otros tipos de consultas, vea [ejemplos de consultas de modelo de asociación](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
## <a name="see-also"></a>Vea también  
 [Contenido para los modelos de asociación del modelo de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)   
 [Crear una consulta de predicción con el Generador de consultas de predicción](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
