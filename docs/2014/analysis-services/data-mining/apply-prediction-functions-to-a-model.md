---
title: Aplicar funciones de predicción a un modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41c7c447af3eb7e0f40c10b98be827caa59867e0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086136"
---
# <a name="apply-prediction-functions-to-a-model"></a>Aplicar funciones de predicción a un modelo
  Para crear una consulta de predicción, antes debe seleccionar el modelo de minería de datos en el que se basará la consulta. Puede seleccionar cualquier modelo de minería de datos que esté incluido en el proyecto actual.  
  
 Cuando haya seleccionado un modelo, agregue una *función de predicción* a la consulta. Se trata de una importación para comprender que las funciones de predicción se usan para muchos propósitos: sí, puede predecir valores, pero también puede obtener estadísticas relacionadas, así como la información que se usó para generar la predicción. Las funciones de predicción pueden devolver los siguientes tipos de valores:  
  
-   El nombre del atributo de predicción y el valor que se predice.  
  
-   Estadísticas acerca de la distribución y la varianza de los valores previstos.  
  
-   La probabilidad del resultado especificado o todos los posibles resultados.  
  
-   Los valores o puntuaciones superiores o inferiores.  
  
-   Los valores asociados a un nodo, un objeto o un atributo especificado.  
  
 Hay una amplia variedad de funciones de predicción que puede utilizar, pero debe elegir la función que se ajuste al tipo de modelo que creó. Normalmente, esta opción depende del algoritmo utilizado para crear el modelo.  
  
-   Para obtener una lista de las funciones de predicción admitidas por casi todos los tipos de modelo, vea [Funciones de predicción generales &#40;DMX&#41;](/sql/dmx/general-prediction-functions-dmx).  
  
-   Además, los algoritmos individuales admiten diversas funciones especializadas. Por ejemplo, si crea un modelo de minería de datos basado en el algoritmo de clústeres de Microsoft, puede utilizar funciones especializadas de predicción para buscar información sobre los clústeres, como la distancia de un valor de datos al centroide del clúster.  
  
     Para obtener ejemplos de cómo consultar un tipo específico de modelo de minería de datos, vea el tema de referencia del algoritmo, en [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>Elegir un modelo de minería de datos que utilizar en la predicción  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en el modelo y seleccione **Generar consulta de predicción**.  
  
     O bien  
  
     En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en la pestaña **Predicción de modelo de minería de datos**y, después, haga clic en **Seleccionar modelo** en la tabla  **Modelo de minería de datos** .  
  
2.  En el cuadro de diálogo **Seleccionar modelo de minería de datos** , seleccione un modelo de minería de datos y haga clic en **Aceptar**.  
  
     Puede elegir un modelo en la base de datos actual de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para crear una consulta con un modelo en una base de datos diferente, debe abrir una nueva ventana de consulta en el contexto de esa base de datos o abrir el archivo de solución que contiene el modelo.  
  
### <a name="add-prediction-functions-to-a-query"></a>Agregue funciones de predicción a una consulta  
  
1.  En **Generador de consultas de predicción**, configure los datos de entrada utilizados para la predicción, proporcionando los valores en el cuadro de diálogo **Entrada de consulta singleton** o asignando el modelo a un origen de datos externo.  
  
     Para más información, vea [Elegir y asignar datos de entrada para una consulta de predicción](choose-and-map-input-data-for-a-prediction-query.md).  
  
    > [!WARNING]  
    >  No es necesario proporcionar entradas para generar predicciones. Cuando no hay ninguna entrada, el algoritmo normalmente devolverá el valor predicho más probable en todas las entradas posibles.  
  
2.  Haga clic en la columna **Origen** y elija un valor en la lista:  
  
    |||  
    |-|-|  
    |**\<nombre del modelo>**|Seleccione esta opción para incluir los valores del modelo de minería de datos en la salida. Solo puede agregar nuevas columnas de predicción.<br /><br /> Cuando se agrega una columna del modelo, el resultado devuelto es la lista de valores no distintivos de esa columna.<br /><br /> Las columnas que agrega con esta opción se incluyen en la parte SELECT de la instrucción DMX resultante.|  
    |**función de predicción**|Seleccione esta opción para examinar una lista de funciones de predicción.<br /><br /> Los valores o funciones que seleccione se agregan a la parte SELECT de la instrucción DMX resultante.<br /><br /> La lista de funciones de predicción no se filtra ni se restringe por el tipo de modelo que ha seleccionado. Por consiguiente, si tiene alguna duda sobre si la función se admite para el tipo actual del modelo, basta con agregar la función a la lista y verla si hay un error.<br /><br /> Los elementos de lista que van precedidos por $ (como $AdjustedProbability) representan las columnas de la tabla anidada que se genera cuando se utiliza la función `PredictHistogram`. Estos son los métodos abreviados que puede usar para devolver una columna y no una tabla anidada.|  
    |**Expresión personalizada**|Seleccione esta opción para escribir una expresión personalizada y asignar después un alias a la salida.<br /><br /> La expresión personalizada se agrega a la parte SELECT de la consulta de predicción resultante DMX.<br /><br /> Esta opción es útil si desea agregar el texto de la salida a cada fila, llamar a funciones de VB o llamar a procedimientos almacenados personalizados.<br /><br /> Para más información sobre cómo usar funciones de Excel y VBA desde DMX, vea [Funciones de VBA en MDX y DAX](/sql/mdx/vba-functions-in-mdx-and-dax).|  
  
3.  Después de agregar cada función o expresión, cambie a la vista DMX para ver cómo se agrega la función dentro de la instrucción DMX.  
  
    > [!WARNING]  
    >  El generador de consultas de predicción no valida el DMX hasta que haga clic en **Resultados**. A menudo, encontrará que la expresión que genera el generador de consultas DMX es no válida. Algunas de las causas habituales son que se hace referencia a una columna que no está relacionada con la columna de predicción o bien que se intenta predecir una columna de una tabla anidada, lo que requiere una instrucción sub-SELECT. En este momento puede cambiar a la vista DMX y continuar modificando la instrucción.  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>Ejemplo: crear una consulta en un modelo de clústeres  
  
1.  Si no tiene un modelo de clústeres disponible para crear esta consulta de ejemplo, cree el modelo, [TM_Clustering], con el [Tutorial básico de minería de datos](../../tutorials/basic-data-mining-tutorial.md).  
  
2.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], haga clic con el botón derecho en el modelo, [TM_Clustering], y seleccione **Generar consulta de predicción**.  
  
3.  En el menú **Modelo de minería de datos** , seleccione **Consulta singleton**.  
  
4.  En el cuadro de diálogo **Entrada de consulta singleton** , establezca los siguientes valores como entradas:  
  
    -   Gender = M  
  
    -   Commute Distance = 5-10 miles  
  
5.  En la cuadrícula de la consulta, en **Origen**, seleccione el modelo de minería de datos TM_Clustering y agregue la columna [Bike Buyer].  
  
6.  En **origen**, seleccione **función de predicción**y agregue la función `Cluster`.  
  
7.  En **origen**, seleccione **función de predicción**, agregue la función `PredictSupport`,, y arrastre la columna modelo [Bike Buyer] al cuadro **criterios o argumento** . Escriba **Support** en la columna **Alias** .  
  
     Copie la expresión que represente la función de predicción y la referencia de columna del cuadro **Criterios y argumento** .  
  
8.  En **Origen**, seleccione **Expresión personalizada**, escriba una alias y, después, haga referencia a la función CEILING de Excel utilizando la sintaxis siguiente:  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     Pegue la referencia de columna como argumento de la función.  
  
     Por ejemplo, la siguiente expresión devuelve el valor CEILING del valor proporcionado:  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     Escriba CEILING en la columna **Alias** .  
  
9. Haga clic en **Cambiar a vista de texto de consulta** para revisar la instrucción DMX que se generó y haga clic en **Cambiar a vista de resultado de consulta** para ver el resultado de las columnas de la consulta de predicción.  
  
     En la tabla siguiente se muestran los resultados esperados:  
  
    |Bike Buyer|$Cluster|SOPORTE TÉCNICO|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|Clúster 8|954|953.948638926372|  
  
 Si desea agregar otras cláusulas en otra parte de la instrucción, por ejemplo, si desea agregar una cláusula WHERE, no puede agregarla mediante la cuadrícula; primero debe cambiar a la vista DMX.  
  
## <a name="see-also"></a>Consulte también  
 [Consultas de minería de datos](data-mining-queries.md)  
  
  
