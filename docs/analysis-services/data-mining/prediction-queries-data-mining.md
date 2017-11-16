---
title: "Consultas de predicción (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5e6686c-1360-480e-8c0d-8a56204fbed9
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 55dd3cf7af1721a958ebebb70d864a1fd0b873c6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="prediction-queries-data-mining"></a>Consultas de predicción (minería de datos)
  El objetivo de un proyecto de minería de datos típico es usar el modelo de minería de datos para realizar predicciones. Por ejemplo, quizás desee predecir el tiempo de inactividad esperado para un clúster de servidores determinado, o generar una puntuación que indique si es probable que los segmentos de clientes respondan a una campaña de publicidad. Para hacer todas estas cosas, crearía una consulta de predicción.  
  
 Funcionalmente, hay diferentes tipos de consultas de predicción admitidos en SQL Server, dependiendo del tipo de entradas a la consulta:  
  
|Tipo de consulta|Opciones de consulta|  
|----------------|-------------------|  
|Consultas de predicción singleton|Utilice una consulta singleton si desea predecir los resultados de un nuevo caso único, o de varios casos nuevos. Proporcione directamente los valores de entrada en la consulta, y la consulta se ejecuta como una sesión única.|  
|Predicciones por lotes|Utilice las predicciones por lotes si tiene datos externos que desea incorporar al modelo, para utilizarlos como base para las predicciones. Para realizar predicciones para un conjunto de datos completo, asigne los datos del origen externo a las columnas del modelo y, a continuación, especifique el tipo de datos predictivos que desea generar.<br /><br /> La consulta del conjunto de datos completo se ejecuta en una única sesión, siendo esta opción mucho más eficaz que enviar varias consultas repetidas.|  
|Predicciones de serie temporal|Utilice una consulta de serie temporal si desea predecir un valor para un número concreto de pasos futuros. La minería de datos de SQL Server también proporciona la siguiente funcionalidad en las consultas de serie temporal:<br /><br /> Puede ampliar un modelo existente agregando nuevos datos como parte de la consulta, y realizar predicciones basadas en la serie compuesta.<br /><br /> Puede aplicar un modelo existente a una nueva serie de datos usando la opción REPLACE_MODEL_CASES.<br /><br /> Puede realizar una predicción cruzada.|  
  
 En las secciones siguientes se describen la sintaxis general de las consultas de predicción, los diferentes tipos de consultas de predicción y cómo trabajar con los resultados de estas consultas.  
  
 [Diseño de una consulta de predicción básica](#bkmk_PredQuery)  
  
-   [Agregar funciones de predicción](#bkmk_PredFunc)  
  
-   [Consultas singleton](#bkmk_SingletonQuery)  
  
-   [Consultas de predicción por lotes](#bkmk_BatchQuery)  
  
-   [Consultas de serie temporal](#bkmk_TSQuery)  
  
 [Trabajar con los resultados de las consultas](#bkmk_WorkResults)  
  
##  <a name="bkmk_PredQuery"></a> Diseño de una consulta de predicción básica  
 Cuando se crea una predicción, normalmente se proporcionan algunos datos nuevos y se pide al modelo que genere la predicción basándose en dichos datos.  
  
-   En una consulta de predicción por lotes, puede asignar el modelo a un origen externo de datos mediante una *combinación de predicción*.  
  
-   En una consulta de predicción singleton, puede escribir uno o más valores para utilizar como entradas. Puede crear varias predicciones mediante una consulta de predicción singleton. Sin embargo, si necesita crear muchas predicciones, el rendimiento es mejor si utiliza una consulta por lotes.  
  
 Ambas consultas, las de predicción por lotes y las consultas singleton, usan la sintaxis de PREDICTION JOIN para definir los datos nuevos. La diferencia radica en cómo se especifica el lado de entrada de la combinación de predicción.  
  
-   En una consulta de predicción por lotes, los datos proceden de un origen de datos externo que se especifica usando la sintaxis de OPENQUERY.  
  
-   En una consulta de predicción singleton, los datos se proporcionan insertados como parte de la consulta.  
  
 Para los modelos de serie temporal, los datos de entrada no siempre son necesarios; es posible realizar predicciones simplemente utilizando los datos que ya se encuentran en el modelo. Sin embargo, si especifica nuevos datos de entrada, debe decidir si utilizará los nuevos datos para actualizar y ampliar el modelo, o reemplazar la serie de datos original que se utilizó en el modelo.  Para obtener más información acerca de estas opciones, consulte [Time Series Model Query Examples](../../analysis-services/data-mining/time-series-model-query-examples.md).  
  
###  <a name="bkmk_PredFunc"></a> Agregar funciones de predicción  
 Además de predecir un valor concreto, puede personalizar una consulta de predicción para que devuelva diversos tipos de información relacionados con la predicción. Por ejemplo, si la predicción crea una lista de productos para recomendar a un cliente, es posible que también desee devolver la probabilidad de cada predicción, de modo que pueda clasificarlas y mostrar únicamente las principales recomendaciones al usuario.  
  
 Para ello, agregue *funciones de predicción* a la consulta. Cada modelo o tipo de consulta admite unas determinadas funciones. Por ejemplo, los modelos de agrupación en clústeres admiten funciones de predicción especiales que proporcionan detalles adicionales sobre los clústeres creados por el modelo, mientras que los modelos de serie temporal tienen funciones que calculan las diferencias a lo largo del tiempo. También existen funciones de predicción generales que funcionan con casi todos los tipos de modelos. Para obtener una lista de las funciones de predicción admitidas en los diferentes tipos de consultas, vea este tema en la referencia de DMX: [Funciones de predicción generales &#40;DMX&#41;](../../dmx/general-prediction-functions-dmx.md).  
  
###  <a name="bkmk_SingletonQuery"></a> Crear consultas de predicción singleton  
 Las consultas de predicción singleton resultan de gran utilidad para crear predicciones rápidas en tiempo real. Un escenario habitual podría ser en el que ha obtenido información de un cliente, quizás mediante un formulario en un sitio web, y desea enviar dicha información como entrada a una consulta de predicción singleton. Por ejemplo, cuando un cliente elige un producto de una lista, podría utilizar esa selección como la entrada a una consulta que prediga los mejores productos que puede recomendar.  
  
 Las consultas de predicción singleton no requieren ninguna tabla independiente que contenga la entrada. En su lugar, se proporcionan una o varias filas de valores como entrada para el modelo, y las predicciones se devuelven en tiempo real.  
  
> [!WARNING]  
>  A pesar de su nombre, las consultas de predicción singleton no realizan solamente predicciones únicas, puede generar varias predicciones para cada conjunto de entradas. Puede proporcionar varios casos de entrada creando una instrucción SELECT para cada caso de entrada y combinándolas con el operador UNION.  
  
 Al crear una consulta de predicción singleton, debe proporcionar los nuevos datos al modelo con el formato PREDICTION JOIN. Esto significa que, aunque no se esté realizando una asignación a una tabla real, hay que asegurarse de que los nuevos datos coinciden con las columnas existentes en el modelo de minería de datos. Si las nuevas columnas de datos y los nuevos datos coinciden exactamente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] asignará las columnas. Esto se denomina *NATURAL PREDICTION JOIN*. Sin embargo, si las columnas no coinciden, o si los nuevos datos no contienen el mismo tipo y cantidad de datos que hay en el modelo, deberá especificar qué columnas del modelo se asignan a los nuevos datos, o especificar los valores que faltan.  
  
###  <a name="bkmk_BatchQuery"></a> Consultas de predicción por lotes  
 Una consulta de predicción por lotes resulta útil si tiene datos externos que desea utilizar para realizar predicciones. Por ejemplo, podría haber compilado un modelo que categorice los clientes por su actividad en línea y el historial de compras. Podría aplicar ese modelo a una lista de contactos de ventas obtenidos recientemente, para crear proyecciones de ventas o identificar objetivos de las campañas propuestas.  
  
 Al realizar una unión de predicción, debe asignar las columnas del modelo a las columnas del nuevo origen de datos. Por consiguiente, el origen de datos que elija para una entrada deberá tener datos que sean en cierto modo similares a los datos del modelo. La nueva información no tiene porqué coincidir exactamente y puede estar incompleta. Por ejemplo, suponga que el modelo se entrenó con información sobre los ingresos y la edad, pero la lista de clientes que utiliza para las predicciones incluye la edad pero no los ingresos. En este escenario, podría asignar los nuevos datos al modelo y crear una predicción para cada cliente. Sin embargo, si los ingresos fueran un elemento de predicción importante para el modelo, la falta de información completa afectaría a la calidad de las predicciones.  
  
 Para obtener los mejores resultados, se deben combinar tantas columnas coincidentes como sea posible entre los nuevos datos y el modelo. Sin embargo, la consulta se realizará correctamente incluso ni no hay ninguna coincidencia. Si no se combina ninguna columna, la consulta devolverá la predicción marginal, que equivale a la instrucción `SELECT <predictable-column> FROM <model>` sin una cláusula PREDICTION JOIN.  
  
 Después de haber asignado todas las columnas pertinentes correctamente, ejecute la consulta y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] realizará las predicciones para cada fila de los nuevos datos basándose en los patrones del modelo. Puede volver a guardar los resultados en una nueva tabla en la vista del origen de datos que contiene los datos externos, o puede copiar y pegar los datos que está utilizando en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!WARNING]  
>  Si usa el diseñador en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el origen de datos externo se debe definir primero como una vista del origen de datos.  
  
 Si utiliza DMX para crear una combinación de predicción, puede especificar el origen de datos externo utilizando los comandos OPENQUERY, OPENROWSET o SHAPE. El método de acceso a datos predeterminado en las plantillas DMX es OPENQUERY. Para más información sobre estos métodos, vea [&#60;source data query&#62;](../../dmx/source-data-query.md).  
  
###  <a name="bkmk_TSQuery"></a> Predicciones en modelos de minería de datos de serie temporal  
 Los modelos de serie temporal son diferentes de otros tipos de modelos; puede utilizar el modelo tal como está para crear predicciones, o puede proporcionar nuevos datos al modelo para actualizarlo y crear predicciones basadas en tendencias recientes. Si agrega nuevos datos, puede especificar la manera en que se deberían utilizar los nuevos datos.  
  
-   *Ampliar los casos del modelo* significa agregar los nuevos datos a la serie de datos existente en el modelo de serie temporal. De ahora en adelante, las predicciones se basarán en la nueva serie combinada. Esta opción es adecuada si solamente desea agregar algunos puntos de datos a un modelo existente.  
  
     Por ejemplo, suponga que tiene un modelo de serie temporal existente entrenado con los datos de ventas del año anterior. Después de haber recopilado varios meses de nuevos datos de ventas, decide actualizar los pronósticos de ventas para el año actual. Puede crear una combinación de predicción que actualice el modelo agregando los nuevos datos y que amplíe el modelo para que realice nuevas predicciones.  
  
-   *Reemplazar los casos del modelo* significa mantener el modelo entrenado, pero reemplazar los casos subyacentes por un nuevo conjunto de datos de casos. Esta opción resulta útil si desea mantener la tendencia del modelo, pero aplicarla a un conjunto de datos diferente.  
  
     Por ejemplo, su modelo original se podría haber entrenado en un conjunto de datos con volúmenes de ventas muy altos; al reemplazar los datos subyacentes por una nueva serie (quizás de un almacén con un volumen de ventas más bajo), se conserva la tendencia, pero las predicciones comienzan a partir de los valores de la serie de sustitución.  
  
 Independientemente del método utilizado, el punto inicial para las predicciones siempre es el final de la serie original.  
  
 Para más información sobre cómo crear combinaciones de predicción en modelos de serie temporal, vea [Ejemplos de consultas de modelos de serie temporal](../../analysis-services/data-mining/time-series-model-query-examples.md) o [PredictTimeSeries &#40;DMX&#41;](../../dmx/predicttimeseries-dmx.md).  
  
##  <a name="bkmk_WorkResults"></a> Trabajar con los resultados de una consulta de predicción  
 Las opciones para guardar los resultados de una consulta de predicción de minería de datos serán diferentes en función de cómo se cree la consulta.  
  
-   Al crear una consulta mediante el Generador de consultas de predicción en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se pueden guardar los resultados de una consulta de predicción en un origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente. Para más información, vea [Ver y guardar los resultados de una consulta de predicción](../../analysis-services/data-mining/view-and-save-the-results-of-a-prediction-query.md).  
  
-   Al crear consultas de predicción utilizando DMX en el panel Consulta de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede utilizar las opciones de salida de la consulta para guardar los resultados en un archivo, o en el panel Resultados de la consulta como texto o en una cuadrícula. Para obtener más información, vea [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
-   Cuando se ejecuta una consulta de predicción utilizando los componentes de Integration Services, las tareas ofrecen la posibilidad de escribir los resultados en una base de datos mediante un administrador de conexiones de ADO.NET o de OLE DB que esté disponible. Para obtener más información, consulte [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
 Es importante entender que los resultados de una consulta de predicción no son iguales que los resultados de una consulta realizada en una base de datos relacional, que siempre devuelve una sola fila de valores relacionados. Cada función de predicción DMX que se agrega a una consulta devuelve su propio conjunto de filas. Por consiguiente, si se realiza una predicción sobre un único caso, el resultado puede ser un valor predicho junto con varias columnas de tablas anidadas que contienen detalles adicionales.  
  
 Si se combinan varias funciones en una consulta, los resultados devueltos se combinarán como un conjunto de filas jerárquico. Por ejemplo, suponga que utiliza un modelo de serie temporal para predecir valores futuros para el importe de ventas y la cantidad de ventas mediante una consulta similar a esta instrucción DMX:  
  
```  
SELECT  
  PredictTimeSeries([Forecasting].[Amount]) as [PredictedAmount]  
, PredictTimeSeries([Forecasting].[Quantity]) as [PredictedQty]  
FROM  
  [Forecasting]  
  
```  
  
 Los resultados de esta consulta son dos columnas, una para cada serie de predicción, donde cada fila contiene una tabla anidada con los valores de predicción:  
  
 **PredictedAmount**  
  
|$TIME|Amount|  
|-----------|------------|  
|201101|172067.11|  
  
|$TIME|Amount|  
|-----------|------------|  
|201102|363390.68|  
  
 **PredictedQty**  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|201101|77|  
  
|$TIME|Cantidad|  
|-----------|--------------|  
|201102|260|  
  
 Si el proveedor no puede procesar conjuntos de filas jerárquicos, se puede eliminar la estructura de los resultados utilizando la palabra clave FLATTEN en la consulta de predicción. Para más información y ejemplos de conjuntos de filas planas, vea [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Consultas de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-queries-data-mining.md)   
 [Consultas de definición de datos &#40;minería de datos&#41;](../../analysis-services/data-mining/data-definition-queries-data-mining.md)  
  
  

