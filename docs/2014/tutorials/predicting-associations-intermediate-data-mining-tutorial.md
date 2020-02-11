---
title: Predecir asociaciones (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bee5ca4ded1b2fd5cbda0712cb766c825b9d0318
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62472850"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>Predecir asociaciones (Tutorial intermedio de minería de datos)
  Una vez procesados los modelos, puede utilizar la información sobre las asociaciones almacenada en el modelo para crear predicciones. En la tarea final de esta lección, aprenderá a generar consultas de predicción a partir de los modelos de asociación que creó. En esta lección se presupone que sabe cómo se utiliza el Generador de consultas de predicción y desea obtener información acerca de cómo se generan consultas de predicción a partir de modelos de asociación. Para obtener más información sobre cómo usar la predicción Generador de consultas, vea [interfaces de consulta de minería de datos](../../2014/analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="creating-a-singleton-prediction-query"></a>Crear una consulta de predicción singleton  
 Las consultas de predicción en un modelo de asociación pueden ser muy útiles para lo siguiente:  
  
-   Recomendar artículos a un cliente, en función de compras anteriores o relacionadas.  
  
-   Buscar eventos relacionados.  
  
-   identificar relaciones en o entre conjuntos de transacciones.  
  
 Para generar una consulta de predicción, seleccione primero el modelo de asociación que desee utilizar, y, a continuación, especifique los datos de entrada. Las entradas pueden proceder de un origen de datos externo, como una lista de valores. También puede generar una consulta singleton y proporcionar los valores sobre la marcha.  
  
 En este escenario, creará primero algunas consultas de predicción singleton para hacerse una idea de cómo funcionan las predicciones. A continuación, creará una consulta de las predicciones masivas que podría utilizar para hacer recomendaciones en función de las compras realizadas actualmente por un cliente.  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>Para crear una consulta de predicción en un modelo de asociación  
  
1.  Haga clic en la pestaña **predicción de modelo de minería** de datos del diseñador de minería de datos.  
  
2.  En el panel **modelo de minería de datos** , haga clic en **Seleccionar modelo**. (Puede omitir este paso y el siguiente si el modelo correcto ya está seleccionado).  
  
3.  En el cuadro de diálogo **Seleccionar modelo de minería de datos** , expanda el nodo que representa la **Asociación**de la estructura de minería de datos y seleccione la **Asociación**del modelo. Haga clic en **OK**.  
  
     De momento, puede hacer caso omiso al panel de entrada.  
  
4.  En la cuadrícula, haga clic en la celda vacía situada debajo de **origen** y seleccione **función de predicción.** En la celda situada **** debajo de campo `PredictAssociation`, seleccione.  
  
     También puede utilizar la función **PREDICT** para predecir las asociaciones. Si lo hace, asegúrese de elegir la versión de la función de **predicción** que toma una columna de tabla como argumento.  
  
5.  En el **Panel modelo de minería de datos** , seleccione la `vAssocSeqLineItems`tabla anidada y arrástrela hasta la cuadrícula hasta el cuadro **criterios o argumento** de la `PredictAssociation` función.  
  
     Al arrastrar y colocar la tabla y los nombres de columna, podrá crear instrucciones complejas sin errores sintácticos. Sin embargo, reemplaza el contenido actual de la celda, que incluye otros argumentos opcionales para la `PredictAssociation` función. Para consultar los demás argumentos, puede agregar provisionalmente una segunda instancia de la función a la cuadrícula como referencia.  
  
6.  Haga clic en el cuadro **criterios o argumento** y escriba el siguiente texto después del nombre de la tabla:`,3`  
  
     El texto completo del cuadro **criterios o argumento** debe ser el siguiente:  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  Haga clic en el botón **resultados** en la esquina superior de la generador de consultas de predicción.  
  
 Los resultados esperados contienen una sola columna con la **expresión**de encabezado. La columna **expresión** contiene una tabla anidada con una sola columna y las tres filas siguientes. Como no especificó un valor de entrada, estas predicciones representan las asociaciones de productos del modelo en su conjunto que tienen mayor probabilidad de producirse.  
  
|Modelo|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 A continuación, utilizará el panel **entrada de consulta singleton** para especificar un producto como entrada de la consulta y ver los productos que es más probable que estén asociados a ese elemento.  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>Para crear una consulta de predicción singleton con entradas de tabla anidada  
  
1.  Haga clic en el botón **diseño** en la esquina del generador de consultas de predicción para volver a la cuadrícula de creación de la consulta.  
  
2.  En el menú **modelo de minería de datos** , seleccione **consulta singleton**.  
  
3.  En el cuadro de diálogo **modelo de minería de datos** , seleccione el modelo de **Asociación** .  
  
4.  En la cuadrícula, haga clic en la celda vacía situada debajo de **origen** y seleccione **función de predicción.** En la celda situada **** debajo de campo `PredictAssociation`, seleccione.  
  
5.  En el **Panel modelo de minería de datos** , seleccione la `vAssocSeqLineItems`tabla anidada y arrástrela hasta la cuadrícula hasta el cuadro **criterios o argumento** de la `PredictAssociation` función. Escriba `,3` después del nombre de la tabla anidada como en el procedimiento anterior.  
  
6.  En el cuadro de diálogo **entrada de consulta singleton** , haga clic en el cuadro **valor** situado junto a **vAssoc SEQ line items**y, a continuación, haga clic en el botón **(...)** .  
  
7.  En el cuadro de diálogo **entrada de tabla anidada** , seleccione `Touring Tire` en el panel **columna de clave** y, a continuación, haga clic en **Agregar**.  
  
8.  Haga clic en el botón **resultados** .  
  
 Los resultados muestran ahora las predicciones de los productos que con mayor probabilidad estarán asociados a Touring Tire.  
  
|Modelo|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 Sin embargo, al explorar el modelo sabrá ya que Touring Tire Tube a menudo se compra junto con Touring Tire; lo que más le interesa saber es qué productos puede recomendar a los clientes que compran estos dos artículos juntos. Cambiará la consulta para que prediga productos relacionados en función de dos elementos de la cesta. Modificará también la consulta para agregar la probabilidad de cada producto predicho.  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>Para agregar entradas y probabilidades a la consulta de predicción singleton  
  
1.  Haga clic en el botón **diseño** en la esquina del generador de consultas de predicción para volver a la cuadrícula de creación de la consulta.  
  
2.  En el cuadro de diálogo **entrada de consulta singleton** , haga clic en el cuadro **valor** situado junto a **vAssoc SEQ line items**y, a continuación, haga clic en el botón **(...)** .  
  
3.  En el panel **columna de clave** , `Touring Tire`seleccione y, a continuación, haga clic en **Agregar**.  
  
4.  En la cuadrícula, haga clic en la celda vacía situada debajo de **origen** y seleccione **función de predicción.** En la celda situada **** debajo de campo `PredictAssociation`, seleccione.  
  
5.  En el **Panel modelo de minería de datos** , seleccione la `vAssocSeqLineItems`tabla anidada y arrástrela hasta la cuadrícula hasta el cuadro **criterios o argumento** de la `PredictAssociation` función. Escriba `,3` después del nombre de la tabla anidada como en el procedimiento anterior.  
  
6.  En el cuadro de diálogo **entrada de tabla anidada** , seleccione `Touring Tire Tube` en el panel **columna de clave** y, a continuación, haga clic en **Agregar**.  
  
7.  En la cuadrícula, en la fila de la `PredictAssociation` función, haga clic en el cuadro **criterios o argumento** y cambie los argumentos para agregar el argumento INCLUDE_STATISTICS.  
  
     El texto completo del cuadro **criterios o argumento** debe ser el siguiente:  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  Haga clic en el botón **resultados** .  
  
 Los resultados de la tabla anidada se modifican ahora para mostrar las predicciones, junto con la compatibilidad y probabilidad. Para obtener más información sobre cómo interpretar estos valores, vea [contenido del modelo de minería de datos para los modelos de asociación &#40;Analysis Services-&#41;de minería de datos ](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md).  
  
|Modelo|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0,291...|0,252...|  
|Water Bottle|2866|0,192...|0,175...|  
|Patch Kit|2113|0,142...|0,132|  
  
## <a name="working-with-results"></a>Trabajar con resultados  
 Cuando hay muchas tablas anidadas en los resultados, es posible que desee simplificar los resultados para facilitar su consulta. Para ello, puede modificar la consulta manualmente y agregar la palabra clave `FLATTENED`.  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para simplificar los conjuntos de filas anidados de una consulta de predicción  
  
1.  Haga clic en el botón **SQL** en la esquina del generador de consultas de predicción.  
  
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
  
3.  Haga clic en el botón **resultados** en la esquina superior de la generador de consultas de predicción.  
  
 Tenga en cuenta que después de editar una consulta manualmente, no podrá volver a cambiar a la vista Diseño sin perder los cambios. Si desea guardar la consulta, puede copiar la instrucción DMX que creó manualmente en un archivo de texto. Cuando cambie de nuevo a la vista Diseño, la consulta se revertirá a la última versión que fue válida en la vista Diseño.  
  
## <a name="creating-multiple-predictions"></a>Crear varias predicciones  
 Suponga que desea conocer las mejores predicciones de cada cliente en función de las compras realizadas en el pasado. Puede utilizar datos externos como entrada de la consulta de predicción, por ejemplo, tablas que contengan el identificador del cliente y las compras más recientes de productos. Los requisitos son que las tablas de datos ya estén definidas como una vista del origen de datos de Analysis Services; por otro lado, los datos de entrada deben contener una tabla de casos y una tabla anidada como las utilizadas en el modelo. No es necesario que tengan el mismo nombre, pero la estructura debe ser similar. Para los objetivos de este tutorial, utilizará las tablas originales en las que se entrenó el modelo.  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>Para cambiar el método de entrada de la consulta de predicción  
  
1.  En el menú **modelo de minería de datos** , seleccione **consulta singleton** de nuevo para borrar la marca de verificación.  
  
2.  Aparecerá un mensaje de error en el que se advierte que se perderá la consulta singleton. Haga clic en **Sí**.  
  
     El nombre del cuadro de diálogo de entrada cambia a **seleccionar tabla (s) de entrada**.  
  
 Dado que lo que le interesa es crear una consulta de predicción que proporcione un identificador de cliente y una lista de productos como entrada, incorporará la tabla de clientes como la tabla de casos y la tabla de compras como la tabla anidada. A continuación, agregará las funciones de predicción para crear recomendaciones.  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para crear una consulta de predicción utilizando las entradas de una tabla anidada  
  
1.  En el panel Modelo de minería de datos, seleccione el modelo Association Filtered.  
  
2.  En el cuadro de diálogo **seleccionar tabla (s) de entrada** , haga clic en **seleccionar tabla de casos**.  
  
3.  En el cuadro de diálogo **seleccionar tabla** , en **origen de datos**, seleccione AdventureWorksDW2008. En la lista **nombre de tabla o vista** , seleccione vAssocSeqOrders y, a continuación, haga clic en **Aceptar**.  
  
     La tabla vAssocSeqOrders se agrega al panel.  
  
4.  En el cuadro de diálogo **seleccionar tabla (s) de entrada** , haga clic en **seleccionar tabla anidada**.  
  
5.  En el cuadro de diálogo **seleccionar tabla** , en **origen de datos**, seleccione AdventureWorksDW2008. En la lista **nombre de tabla o vista** , seleccione vAssocSeqLineItems y, a continuación, haga clic en **Aceptar**.  
  
     La tabla vAssocSeqLineItems se agrega al panel.  
  
6.  En el cuadro de diálogo **especificar combinación anidada** , arrastre el campo ordernumber desde la tabla de casos y colóquelo en el campo ordernumber de la tabla anidada.  
  
     También puede hacer clic en **Agregar relación** y crear la relación seleccionando columnas de una lista.  
  
7.  En el cuadro de diálogo **especificar relación** , compruebe que los campos OrderNumber están asignados correctamente y, a continuación, haga clic en **Aceptar**.  
  
8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **especificar combinación anidada** .  
  
     La tabla anidada y la tabla de casos se actualizan en el panel de diseño para mostrar las combinaciones que conectan las columnas de datos externos con las columnas del modelo. Si las relaciones son erróneas, puede hacer clic con el botón secundario en la línea de combinación y seleccionar **modificar conexiones** para editar la asignación de columnas, o puede hacer clic con el botón secundario en la línea de combinación y seleccionar **eliminar** para quitar la relación por completo.  
  
9. Agregue una nueva fila a la cuadrícula. En **origen**, seleccione **tabla vAssocSeqOrders**. En **campo**, seleccione CustomerKey.  
  
10. Agregue una nueva fila a la cuadrícula. En **origen**, seleccione **tabla vAssocSeqOrders**. En **campo**, seleccione región.  
  
11. Agregue una nueva fila a la cuadrícula. En **origen**, seleccione **función de predicción**y, en **campo**, `PredictAssociation`seleccione.  
  
12. Arrastre vAssocSeqLineItems, al cuadro **criterios o argumento** de la `PredictAssociation` fila. Haga clic al final del cuadro **criterios o argumento** y escriba el siguiente texto:`INCLUDE_STATISTICS,3`  
  
     El texto completo del cuadro **criterios o argumento** debe ser:`[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. Haga clic en el botón **resultado** para ver las predicciones de cada cliente.  
  
 Puede intentar crear una consulta de predicción similar en varios modelos para ver si al aplicar filtros, cambian los resultados de predicción. Para obtener más información sobre cómo crear predicciones y otros tipos de consultas, vea [ejemplos de consultas de modelos de asociación](../../2014/analysis-services/data-mining/association-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte también  
 [Contenido del modelo de minería de datos para los modelos de asociación &#40;Analysis Services-minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [&#41;PredictAssociation &#40;DMX](/sql/dmx/predictassociation-dmx)   
 [Crear una consulta de predicción con el Generador de consultas de predicción](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
