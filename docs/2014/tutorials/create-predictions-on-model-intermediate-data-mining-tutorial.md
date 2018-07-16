---
title: Crear predicciones en una modelo (Tutorial de minería de datos intermedios) de clústeres de secuencia | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 94a8d4f9-a76a-49c5-9785-917010359511
caps.latest.revision: 20
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 006418a07f393fd50334a2ea9c122cdd92353cda
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198305"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>Crear predicciones en un modelo de agrupación en clústeres de secuencia (Tutorial intermedio de minería de datos)
  Una vez que comprenda el mejor modelo de clústeres examinando en el Visor de secuencia, puede crear consultas de predicción utilizando el generador de consultas de predicción en el **predicción de modelo de minería de datos** ficha en el Diseñador de minería de datos. Para crear una predicción, seleccione primero el modelo de agrupación en clústeres de secuencia y, a continuación, seleccione los datos de entrada. Para las entradas, puede utilizar un origen de datos externo o puede crear una consulta singleton y proporcionar los valores en un cuadro de diálogo.  
  
 En esta lección se presupone que sabe utilizar el Generador de consultas de predicción y desea obtener información acerca de cómo se crean consultas específicas para un modelo de agrupación en clústeres de secuencia. Para obtener información general acerca de cómo utilizar el generador de consultas de predicción, vea [Interfaces de consultas de minería de datos](../../2014/analysis-services/data-mining/data-mining-query-tools.md) o en la sección del tutorial básico de minería de datos, [crear predicciones &#40;Basic Data Mining Tutorial&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>Crear predicciones en el modelo regional  
 En este escenario, primero creará algunas consultas de predicción singleton para hacerse una idea del modo en que las predicciones pueden variar según la región.  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>Para crear una consulta singleton en un modelo de agrupación en clústeres de secuencia  
  
1.  Haga clic en el **predicción de modelo de minería de datos** ficha del Diseñador de minería de datos.  
  
2.  En el **Mining Model** menú de columna, seleccione **consulta Singleton**.  
  
     El **Mining Model** panel y **entrada de consulta Singleton** panel aparece.  
  
3.  En el **Mining Model** panel, haga clic en **Seleccionar modelo**. (Puede omitir este paso si el agrupación en clústeres de secuencia ya está seleccionado).  
  
     El **Seleccionar modelo de minería de datos** abre el cuadro de diálogo.  
  
4.  Expanda el nodo que representa la estructura de minería de datos **Sequence Clustering with Region**y seleccione el modelo **Sequence Clustering with Region**. Haga clic en **Aceptar**. De momento haga caso omiso al panel de entrada. Especificará los datos de entrada cuando haya configurado las funciones de predicción.  
  
5.  En la cuadrícula, haga clic en la celda vacía bajo **origen** y seleccione **función de predicción.** En la celda bajo **campo**, seleccione **PredictSequence**.  
  
    > [!NOTE]  
    >  También puede usar el **Predict** función. Si lo hace, asegúrese que elija la versión de la **Predict** función que toma como argumento una columna de tabla...  
  
6.  En el **Mining Model** panel, seleccione la tabla anidada `v Assoc Seq Line Items`y arrástrela hasta la cuadrícula, al **criterios o argumento** cuadro para la **PredictSequence** función.  
  
     Arrastrar y colocar los nombres de tabla y columna permite crear instrucciones complejas sin errores de sintaxis. Sin embargo, se reemplazará el contenido actual de la celda, que contiene otros argumentos opcionales para el **PredictSequence** función. Para consultar los demás argumentos, puede agregar provisionalmente una segunda instancia de la función a la cuadrícula como referencia.  
  
7.  Haga clic en el **resultado** situado en la esquina superior del generador de consultas de predicción.  
  
 Los resultados esperados contienen una sola columna con el encabezado **expresión**. El **expresión** columna contiene una tabla anidada con tres columnas como sigue:  
  
|$SEQUENCE|Line Number|Modelo|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 ¿Qué significan estos resultados? Recuerde que no especificó ninguna entrada. Por tanto, la predicción se realiza con todos los datos de casos rellenados, y Analysis Services devuelve la predicción que, en términos generales, es más probable.  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>Agregar entradas a una consulta de predicción singleton  
 Hasta ahora, no había especificado ninguna entrada. En la siguiente tarea, utilizará el **entrada de consulta Singleton** panel para especificar algunas entradas en la consulta. En primer lugar, utilizará [Region] como entrada en el modelo de agrupación en clústeres de secuencia regional para determinar si las secuencias predichas son las mismas en todas las regiones. A continuación, aprenderá a modificar la consulta para agregar la probabilidad de cada predicción y simplificará los resultados para que resulte más sencillo consultarlos.  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>Para generar predicciones de un grupo de clientes concreto  
  
1.  Haga clic en el **diseño** botón en la esquina superior izquierda del generador de consultas de predicción para volver a la cuadrícula de generación de consultas.  
  
2.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en el **valor** cuadro `Region`y seleccione **Europa**.  
  
3.  Haga clic en el **resultado** botón para ver las predicciones para los clientes de Europa.  
  
4.  Haga clic en el **diseño** botón en la esquina superior izquierda del generador de consultas de predicción para volver a la cuadrícula de generación de consultas.  
  
5.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en el **valor** cuadro `Region`y seleccione **Norteamérica**.  
  
6.  Haga clic en el **resultado** botón para ver las predicciones para los clientes en América del Norte.  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>Agregar probabilidades utilizando una expresión personalizada  
 Generar la probabilidad de cada predicción resulta algo más complicado, pues la probabilidad es un atributo de predicción y se genera como una tabla anidada. Si conoce las extensiones de minería de datos (DMX), puede modificar con facilidad la consulta y agregar una instrucción sub-SELECT a la tabla anidada. No obstante, también puede crear una instrucción sub-SELECT en el Generador de consultas de predicción mediante una expresión personalizada.  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>Para generar probabilidades de una secuencia de predicción utilizando una expresión personalizada  
  
1.  Haga clic en el **diseño** botón en la esquina superior izquierda del generador de consultas de predicción para volver a la cuadrícula de generación de consultas.  
  
2.  En la cuadrícula, en **origen**, haga clic en una nueva fila y seleccione **expresión personalizada**.  
  
3.  Deje la casilla bajo **campo** en blanco.  
  
4.  Para **Alias**, tipo `t`.  
  
5.  En el **criterios o argumento** , escriba la instrucción Sub-select completa tal como se muestra en el siguiente ejemplo de código. No olvide incluir los paréntesis de apertura y cierre.  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  Haga clic en el **resultado** botón para ver las predicciones para los clientes de Europa.  
  
 Los resultados contienen dos tablas anidadas: una con la predicción  y otra con la probabilidad de la predicción. Si la consulta no funciona, puede cambiar a la vista de diseño de consultas y revisar toda la instrucción de consulta, que debería ser como la siguiente:  
  
```  
SELECT  
  PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
  ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
FROM  
  [Sequence Clustering with Region]  
NATURAL PREDICTION JOIN  
(SELECT 'Europe' AS [Region]) AS t  
```  
  
### <a name="working-with-results"></a>Trabajar con resultados  
 Cuando hay muchas tablas anidadas en los resultados, es posible que desee simplificar los resultados para facilitar su consulta. Para ello, puede modificar la consulta manualmente y agregar la palabra clave `FLATTENED`.  
  
##### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>Para simplificar los conjuntos de filas anidados de una consulta de predicción  
  
1.  Haga clic en el **consulta** situado en la esquina del generador de consultas de predicción.  
  
     La cuadrícula cambia a un panel abierto donde puede ver y modificar la instrucción DMX que creó el Generador de consultas de predicción.  
  
2.  Después de la palabra clave `SELECT`, escriba `FLATTENED`.  
  
     El texto completo de la consulta debería ser similar al siguiente:  
  
    ```  
    SELECT FLATTENED  
      PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
      ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
    FROM  
      [Sequence Clustering with Region]  
    NATURAL PREDICTION JOIN  
    (SELECT 'Europe' AS [Region]) AS t  
    ```  
  
3.  Haga clic en el **resultados** situado en la esquina superior del generador de consultas de predicción.  
  
 Después de editar la consulta manualmente, no podrá volver a la vista Diseño sin perder los cambios. Sin embargo, puede guardar la instrucción DMX que creó manualmente en un archivo de texto y, a continuación, cambiar de nuevo a la vista Diseño. Al hacer esto, la consulta se revierte a la última versión que fue válida en la vista Diseño.  
  
## <a name="creating-predictions-on-the-related-model"></a>Crear predicciones en el modelo relacionado  
 En los ejemplos anteriores se utilizó una columna de una tabla de casos, Region, como entrada de la consulta de predicción singleton, porque lo que se pretendía era saber si el modelo encontraba diferencias entre las regiones. Sin embargo, después de analizar el modelo, decidió que las diferencias no eran lo suficientemente sólidas como para justificar que las recomendaciones del producto se personalizaran según la región. Lo que realmente le interesa predecir son los artículos que seleccionan los clientes. Por tanto, en las consultas siguientes, utilizará el modelo de agrupación en clústeres de secuencia que no incluye Region para generar las recomendaciones de todos los clientes.  
  
### <a name="using-nested-table-columns-as-input"></a>Utilizar las columnas de una tabla anidada como entrada  
 En primer lugar, creará una consulta de predicción singleton que tome un único elemento como entrada y devuelva el siguiente elemento más probable. Para obtener una predicción de este tipo, deberá utilizar una columna de tabla anidada como valor de entrada. Esto se debe a que el atributo que está prediciendo, Modelo, forma parte de una tabla anidada. Analysis Services proporciona la **entrada de tabla anidada** cuadro de diálogo que le ayudarán a crear fácilmente consultas de predicción en anidados atributos de tabla, utilizando el generador de consultas de predicción.  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>Para utilizar una tabla anidada como entrada de una predicción  
  
1.  Haga clic en el **diseño** botón en la esquina superior izquierda del generador de consultas de predicción para volver a la cuadrícula de generación de consultas.  
  
2.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en el **valor** cuadro `Region`y seleccione la fila vacía para borrar la entrada para este campo.  
  
3.  En el **entrada de consulta Singleton** cuadro de diálogo, haga clic en el **valor** cuadro `vAssocSeqLineItems`y, a continuación, haga clic en el botón (…).  
  
4.  En el **entrada de tabla anidada** cuadro de diálogo, haga clic en **agregar**.  
  
5.  En la nueva fila, haga clic en el cuadro en `Model`y seleccione Touring Tire en la lista. Haga clic en **Aceptar**.  
  
6.  Haga clic en el **resultado** botón para ver las predicciones.  
  
 El modelo recomienda los elementos siguientes para todos los clientes que eligen Touring Tire como primer artículo. Al examinar el modelo, ya sabe que los clientes compran con frecuencia los productos Touring Tire de y Touring Tire Tube juntos, por lo que estas recomendaciones parecen buenas.  
  
|$SEQUENCE|Line Number|Modelo|  
|---------------|-----------------|-----------|  
|1||Touring Tire Tube|  
|2||Sport-100|  
|3||Long-Sleeve Logo Jersey|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>Crear una consulta de predicción masiva utilizando entradas de una tabla anidada  
 Ahora que el modelo crea el tipo de predicciones adecuado, por lo que se puede utilizar para realizar recomendaciones, creará una consulta de predicción que se asignará a un origen de datos externo. Ese origen de datos proporcionará valores que representan los productos actuales. Dado que lo que le interesa es crear una consulta de predicción que proporcione un identificador de cliente y una lista de productos como entrada, incorporará la tabla de clientes como la tabla de casos y la tabla de compras como la tabla anidada. A continuación, agregará funciones de predicción, tal y como hizo anteriormente, para crear recomendaciones.  
  
 Este procedimiento es el mismo que el que utilizó para crear predicciones en el escenario de la cesta de compra de la lección 3; sin embargo, en un modelo de agrupación en clústeres de secuencia, las predicciones también necesitan el pedido como entrada.  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>Para crear una consulta de predicción utilizando las entradas de una tabla anidada  
  
1.  En el **Mining Model** panel, seleccione la agrupación en clústeres de secuencia del modelo, si aún no está seleccionada.  
  
2.  En el **Seleccionar tabla (s) de entrada** cuadro de diálogo, haga clic en **Seleccionar tabla de casos**.  
  
3.  En el **Seleccionar tabla** cuadro de diálogo origen de datos, seleccione Orders. En el **nombre de tabla o vista** lista, seleccione vAssocSeqOrders y, a continuación, haga clic en **Aceptar**.  
  
4.  En el **Seleccionar tabla (s) de entrada** cuadro de diálogo, haga clic en **Seleccionar tabla anidada**.  
  
5.  En el **Seleccionar tabla** cuadro de diálogo para **origen de datos**, seleccione Orders. En el **nombre de tabla o vista** lista, seleccione Vassocseqlineitem y, a continuación, haga clic en **Aceptar**.  
  
     Analysis Services intentará detectar las relaciones y crearlas automáticamente si los tipos de datos coinciden y los nombres de columna son similares. Si las relaciones que crea son erróneas, puede haga clic en la línea de combinación y seleccionar **modificar conexiones** para editar la columna asignación, o haga clic en la línea de combinación y seleccionar **eliminar** a quitar definitivamente la relación. En este caso, dado que las tablas ya estuvieron unidas en la vista del origen de datos, esas relaciones se agregan automáticamente al panel de diseño.  
  
6.  Agregue una nueva fila a la cuadrícula. Para **origen**, seleccione el vAssocSeqOrders y para **campo**, seleccione CustomerKey.  
  
7.  Agregue una nueva fila a la cuadrícula. Para **origen**, seleccione **función de predicción**y para **campo**, seleccione **PredictSequence**.  
  
8.  Arrastre vAssocSeqLineItems al **criterios o argumento** cuadro. Haga clic al final de la **criterios o argumento** cuadro y, a continuación, escriba los siguientes argumentos: `2`.  
  
     El texto completo en el **criterios o argumento** cuadro debe ser: `[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. Haga clic en el **resultado** botón para ver las predicciones para cada cliente.  
  
 Ha completado el tutorial sobre modelos de agrupación en clústeres de secuencia.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Si ya ha terminado todas las secciones de la [Tutorial intermedio de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md), podría ser el siguiente paso aprender a usar las instrucciones de extensiones de minería de datos (DMX) para crear modelos y generar predicciones. Para obtener más información, consulte [crear y consultar datos de modelos de minería con DMX: tutoriales &#40;Analysis Services - minería de datos&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md).  
  
 Si tiene algunos conceptos de programación, también puede utilizar Objetos de administración de análisis (AMO) para trabajar mediante programación con objetos de minería de datos. Para obtener más información, vea [Clases de minería de datos de AMO](../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md).  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de consultas de modelo de clústeres de secuencia](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Para los modelos de clústeres de secuencia de contenido del modelo de minería de datos &#40;Analysis Services - minería de datos&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
