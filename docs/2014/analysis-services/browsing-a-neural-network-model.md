---
title: Examinar un modelo de red neuronal | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- mining model, neural network
- neural networks
- dependency network
ms.assetid: e4224cb7-115b-4889-ac07-03f096fb55fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4dcb323a309125695df6d3c483f8996d36fdfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66088452"
---
# <a name="browsing-a-neural-network-model"></a>Examinar un modelo de red neuronal
  Cuando abre un modelo de red neuronal o de regresión lógica a través de **Examinar**, el modelo se muestra en un visor interactivo, similar al visor de modelos de red neuronal en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. El visor sirve para explorar correlaciones y obtener información sobre los patrones del modelo y los datos subyacentes.  
  
##  <a name="BKMK_Tabs"></a> Explorar el modelo  
 Los modelos que se basan en algoritmos de red neuronal o de regresión lógica de [!INCLUDE[msCoName](../includes/msconame-md.md)] se parecen en que analizan los datos como un conjunto de conexiones entre las entradas y salidas conocidas. El visor **Examinar** ayuda a explorar esas conexiones mediante los controles siguientes:  
  
-   [Variables](#BKMK_Variables)  
  
-   [Entradas](#BKMK_Inputs)  
  
-   [Salidas](#BKMK_Outputs)  
  
 Si quiere experimentar con este visor, puede crear un modelo con el [Asistente para clasificación &#40;Complementos de minería de datos para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md) y usar las opciones **avanzadas** para cambiar el algoritmo al de Regresión logística de Microsoft en el cuadro de diálogo **Parámetros de algoritmo**.  
  
###  <a name="BKMK_Variables"></a> Variables  
 El panel **Variables** muestra una lista de variables de entrada según el orden en el que surten efecto en el modelo. Para filtrar el modelo, se usan los controles de **Entrada** y de **Salida**, que afectan a las variables que se muestran, así como a su orden.  
  
 Con este visor, podrá explorar los factores más importantes para determinar si un cliente pertenece con más probabilidad a la categoría Bike Buyer o a la categoría Non-buyer.  
  
 ![Probar el efecto en el resultado de los atributos seleccionados](media/dm13-neuralnet-agebuyer1.gif "probar el efecto en el resultado de los atributos seleccionados")  
  
##### <a name="explore-variables"></a>Explorar las variables  
  
1.  Inicialmente, el panel **Variables** se ordenaba por la importancia de los atributos, en función de los filtros actuales. La longitud de la barra indica la fuerza del factor.  
  
     En el ejemplo, puede ver que los ingresos son el factor con mayor influencia, seguido de la región. Por otra parte, los clientes con muchos automóviles y muchos hijos probablemente no comprarán una bicicleta.  
  
2.  En el panel **Variables**, haga clic en el encabezado de columna para **Atributo**.  
  
     Al ordenar según los atributos, puede ver las discretizaciones que se crearon para cada una de las columnas de entrada. Los valores literales *discretizan* las columnas con valores discretos, como por ejemplo, empleo.  
  
3.  Observe los intervalos de valores que se encontraron para **Edad** e **Ingresos**.  
  
     Si ninguna de las columnas de entrada son números (es decir, la totalidad de la columna de datos es un tipo de dato numérico continuo), los números se depositan o discretizan en intervalos discretos.  
  
     Para los ingresos, la columna se ha subdividido de grupos, como por ejemplo, 78,4-154,06 (para el nivel de ingresos más elevado).  
  
     ![Ordenar para ver cómo se agrupan las variables](media/dm13-nn-bucketing-variables.gif "ordenar para ver cómo se agrupan las variables")  
  
     Si quiere hacer grupos diferentes, use la herramienta [Cambiar etiquetas &#40;Complementos de minería de datos de SQL Server&#41;](relabel-sql-server-data-mining-add-ins.md) o las funciones de Excel para crear nuevas categorías de ingresos antes de generar el modelo.  
  
4.  Haga clic en **Favorece Sí** para restaurar el gráfico a la vista predeterminada.  
  
     De manera predeterminada, la vista se ordena según el valor de **Favorece** para el primer valor que aparece como resultado. Puede cambiar los resultados que se asignan a la primera y segunda columna; para ello, elija un valor nuevo para **Valor 1** y **Valor 2** en **Resultados**.  
  
5.  Sitúe el mouse sobre la barra coloreada superior del gráfico.  
  
     Aparece una ventana con información sobre herramientas que incluye una puntuación de *importancia*, un par de puntuaciones de *probabilidad* y un par de valores de *mejora respecto al modelo predictivo*.  
  
    -   La **importancia** se calcula en la totalidad del conjunto de datos y se identifica el atributo que, teniendo en cuenta todas las entradas, tiene mayor correlación con el resultado de destino. El visor ordena los valores del gráfico según las puntuaciones de importancia.  
  
    -   La **probabilidad** se calcula para cada conjunto de pares atributo-valor, para los resultados de destino, en la totalidad del conjunto de datos.  
  
    -   La **mejora respecto al modelo predictivo** indica el grado de utilidad de un par atributo-valor determinado para promover un resultado u otro.  
  
     Nota: La información sobre herramientas contiene la misma información independientemente de si coloca el mouse sobre una columna u otra.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_Inputs"></a> Entradas  
 El panel **Entradas** le permite elegir un conjunto de entradas y aplicarlo como filtro para el modelo, lo cual le permite ver el efecto de esas opciones en el resultado en función de los datos de entrenamiento.  
  
##### <a name="explore-inputs"></a>Explorar entradas  
  
1.  Imagine que desea fijar como destino un grupo específico y que sabe los factores que influencian en mayor medida a las compras de ese grupo.  
  
     En el **entrada** panel, haga clic en el  **\<todas >** celda bajo **atributo**y seleccione **Age**.  
  
     Para **Valor**, seleccione la categoría de edad más joven.  
  
2.  Observe que incluso cuando filtra en una categoría de edad específica, la región Pacífico pasa casi al principio de la lista. Esto se debe a que los clientes de la región del Pacífico son más proclives a comprar una bicicleta que los clientes de otras regiones.  
  
     Puesto que la región no es algo en que se pueda influir, se puede quitar esta variable para que no se tenga en cuenta y ver otros factores y volver a cambiar las entradas.  
  
     En el panel **Entrada**, haga clic en la celda vacía en **Edad** y seleccione **Región**.  
  
     En **Valor**, seleccione **Europa**.  
  
3.  Siga agregando filtros de entrada para centrarse en un grupo de interés particular.  
  
     Por ejemplo, para el atributo de entrada, agregue **Sexo** y seleccione **Femenino** como valor.  
  
     ![Probar el efecto en el resultado de los atributos seleccionados](media/dm13-neuralnet-agebuyer2.gif "probar el efecto en el resultado de los atributos seleccionados")  
  
     Observe cómo cambia la lista de variables. Ahora **Ingresos** es la variable más importante para predecir el resultado de destino.  
  
     El orden en el que se aplican los filtros de entrada no afecta a los resultados.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="BKMK_Outputs"></a> Salidas  
 En el panel **Resultados**, puede elegir el resultado que le interesa. Las redes neuronales le permiten especificar tantas columnas de resultados como desee, aunque al agregar más resultados aumenta la complejidad del modelo y su procesamiento podría requerir mucho más tiempo.  
  
 Para comparar dos resultados, se deben haber designado como columnas **Predicción** o **Solo predicción**.  
  
##### <a name="explore-outputs"></a>Explorar resultados  
  
1.  Use la lista **Atributo de salida** para seleccionar un atributo.  
  
2.  Seleccione dos resultados en las listas de Valor 1 y Valor 2. Estos dos estados del atributo de salida se compararán en el panel **Variables** .  
  
 [Volver al principio](#BKMK_Tabs)  
  
## <a name="more-about-neural-network-models"></a>Más información acerca de los modelos de red neuronal  
 La información en el Visor se recupera desde el servidor mediante un procedimiento almacenado específico para este tipo de modelo: System.Microsoft.AnalysisServices.System.DataMining.NeuralNet.GetAttributeScores.  
  
 Si quiere crear un modelo con varios atributos de predicción mediante complementos, use las opciones de modelado **avanzadas**.  
  
 Para más información, vea [Crear estructura de minería de datos &#40;Complementos de minería de datos de SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md) y [Agregar modelo a estructura &#40;Complementos de minería de datos para Excel&#41;](add-model-to-structure-data-mining-add-ins-for-excel.md).  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
