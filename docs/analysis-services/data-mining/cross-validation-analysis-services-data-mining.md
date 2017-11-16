---
title: "La validación cruzada (Analysis Services: minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
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
helpviewer_keywords:
- stored procedures [Analysis Services], data mining
- cross-validation [data mining]
- scoring [data mining]
- accuracy testing [data mining]
ms.assetid: 718b9072-0f35-482a-a803-9178002ff5b9
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 462c6fbc78f3a7c125dc82e8dd61d11cb2b99aaf
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cross-validation-analysis-services---data-mining"></a>Validación cruzada (Analysis Services - Minería de datos)
  La*validación cruzada* es una herramienta estándar de análisis que resulta muy útil a la hora de desarrollar y ajustar modelos de minería de datos. La validación cruzada se usa después de crear una estructura de minería de datos y los modelos de minería de datos relacionados para determinar la validez del modelo.  La validación cruzada tiene las aplicaciones siguientes:  
  
-   Validar la solidez de un modelo de minería de datos determinado.  
  
-   Evaluar varios modelos de una instrucción única.  
  
-   Generar varios modelos e identificar a continuación el mejor modelo basándose en estadísticas.  
  
 En esta sección se describe cómo usar las características de validación cruzada proporcionadas para la minería de datos y cómo interpretar sus resultados para un único modelo o para varios basados en un único conjunto de datos.  
  
## <a name="overview-of-cross-validation-process"></a>Información general sobre el proceso de validación cruzada  
 La validación cruzada consta de dos fases: entrenamiento y generación de resultados. En estas fases se incluyen los pasos siguientes:  
  
-   Debe seleccionar una estructura de minería de datos de destino.  
  
-   Luego especifica los modelos que desea probar. Este paso es opcional; puede probar solo la estructura de minería de datos.  
  
-   Especifique los parámetros para probar los modelos entrenados.  
  
    -   El atributo de predicción, el valor de predicción y el umbral de precisión.  
  
    -   El número de plegamientos en los que desea crear particiones de los datos del modelo o de la estructura.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea y entrena tantos modelos como plegamientos.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devuelve un conjunto de medidas de precisión para cada plegamiento de cada modelo o para el conjunto de datos en conjunto.  
  
## <a name="configuring-cross-validation"></a>Configurar la validación cruzada  
 Puede personalizar el modo de funcionamiento de la validación cruzada para controlar el número de secciones cruzadas, los modelos probados y la barra de precisión para las predicciones. Si usa los procedimientos almacenados de validación cruzada, también puede especificar el conjunto de datos que se usa para validar los modelos. Esta variedad de opciones implica que puede producir con facilidad muchos conjuntos de resultados diferentes que a continuación se deben comparar y analizar.  
  
 En esta sección se proporciona información para ayudarle a configurar la validación cruzada correctamente.  
  
### <a name="setting-the-number-of-partitions"></a>Establecer el número de particiones  
 Al especificar el número de particiones, se determina cuántos modelos temporales se van a crear. Para cada partición se marca una sección transversal de los datos para su uso como conjunto de pruebas y se crea un nuevo modelo mediante entrenamiento en los datos restantes y no en la partición. Este proceso se repite hasta que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ha creado y probado el número de modelos especificado. Los datos especificados como disponibles para validación cruzada se distribuyen uniformemente entre todas las particiones.  
  
 El ejemplo del diagrama muestra el uso de los datos si se especifican tres plegamientos.  
  
 ![Cómo segmenta la validación cruzada datos](../../analysis-services/data-mining/media/xvoverviewmain.gif "Cómo segmenta la validación cruzada datos")  
  
 En el escenario del diagrama, la estructura de minería de datos contiene un conjunto de datos de exclusión que se usa para pruebas, pero el conjunto de datos de pruebas no se ha incluido para la validación cruzada. Como resultado, todos los datos del conjunto de datos de aprendizaje, el 70 por ciento de los datos de la estructura de minería de datos, se usan para validación cruzada. El informe de validación cruzada muestra el número total de casos usados en cada partición.  
  
 También puede especificar la cantidad de datos que se usan durante la validación cruzada si especifica el número de casos totales que se van a usar. Los casos se distribuyen de forma uniforme en todos los plegamientos.  
  
 En las estructuras de minería de datos almacenada en una instancia de SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el valor máximo que puede establecer para el número de plegamientos es 256, o el número de casos, lo que sea menor. Si utiliza una estructura de minería de datos de sesión, el número máximo de plegamientos es 10.  
  
> [!NOTE]  
>  A medida que aumenta el número de plegamientos, aumenta en consecuencia el tiempo necesario para realizar la validación cruzada porque se debe generar y probar un modelo para cada plegamiento. Puede experimentar problemas de rendimiento si el número de plegamientos es demasiado alto.  
  
### <a name="setting-the-accuracy-threshold"></a>Establecer el umbral de precisión  
 El umbral de estado le permite establecer la barra de precisión para las predicciones. Para cada caso, el modelo calcula la *probabilidad de predicción*, que indica la probabilidad de que el estado de predicción sea correcto. Si la probabilidad de predicción supera la barra de precisión, la predicción se considera correcta; de no ser así, la predicción se cuenta como incorrecta. Para controlar este valor, hay que establecer **State Threshold** en un número entre 0.0 y 1.0, donde los números más cercanos a 1 indican un alto nivel de confianza en las predicciones, y los números más próximos a 0 indican que hay mayor probabilidad de que la predicción sea verdadera. El valor predeterminado para el umbral de estado es NULL, lo que significa que el estado de predicción con la probabilidad superior se considera el valor de destino.  
  
 Debe tener en cuenta que el valor del umbral de estado afecta a las medidas de precisión del modelo. Por ejemplo, suponga que tiene tres modelos que desea probar. Todos se basan en la misma estructura de minería de datos y todos predicen la columna [Bike Buyer]. Además, desea predecir un único valor 1, lo que significa “sí, comprará”. Los tres modelos devuelven predicciones con probabilidades de predicción de 0.05, 0.15 y 0.8. Si establece el umbral de estado en 0.10, dos de las predicciones se cuentan como correctas. Si establece el umbral de estado en 0.5, solo se cuenta que un modelo ha devuelto una predicción correcta. Si usa el valor predeterminado, null, la predicción más probable se cuenta como correcta. En este caso, las tres predicciones se contarían como correctas.  
  
> [!NOTE]  
>  Puede establecer un valor de 0.0 para el umbral, pero el valor carece de significado porque todas las predicciones se contarán como correctas, incluso las de probabilidad cero. Tenga cuidado con no establecer por error **State Threshold** en 0.0.  
  
### <a name="choosing-models-and-columns-to-validate"></a>Elegir los modelos y columnas para la validación  
 Al utilizar la pestaña **Validación cruzada** del Diseñador de minería de datos, debe seleccionar primero la columna de predicción de la lista. Normalmente, una estructura de minería de datos puede admitir muchos modelos de minería, de los cuales no todos utilizan la misma columna de predicción. Al ejecutar una validación cruzada, solo se podrán incluir en el informe aquellos modelos que utilicen la misma columna de predicción.  
  
 Para elegir un atributo de predicción, haga clic en **Atributo de destino** y seleccione la columna de la lista. Si el atributo de destino es una columna anidada o una columna en una tabla anidada, debe escribir el nombre de la columna anidada con el formato \<nombre de tabla anidada > (clave).\< Anidar columnas >. Si la única columna utilizada de la tabla anidada es la columna de clave, puede usar \<nombre de tabla anidada > (clave).  
  
 Después de seleccionar el atributo de predicción, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] prueba todos los modelos que utilizan el mismo atributo de predicción automáticamente. Si el atributo de destino contiene valores discretos, después de haber seleccionado la columna de predicción, puede escribir un estado de destino, en caso de que haya un valor concreto que desee predecir.  
  
 La selección del estado de destino afectará a las medidas que se devuelvan. Si especifica que un atributo de destino (es decir, un nombre de columna) no obtiene un valor concreto que el modelo deba predecir, el modelo se evaluará, de forma predeterminada, de acuerdo a su predicción del estado más probable.  
  
 Cuando use una validación cruzada con modelos de agrupación en clústeres, no habrá ninguna columna de predicción; en su lugar, debe seleccionar **Nº de clústeres** en el cuadro de lista **Atributo de destino** . Cuando haya seleccionado esta opción, otras opciones que no son relevantes para los modelos de agrupación en clústeres, como **Estado del destino**, se deshabilitarán. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] probará a continuación todos los modelos de agrupación en clústeres que estén asociados a la estructura de minería de datos.  
  
## <a name="tools-for-cross-validation"></a>Herramientas para la validación cruzada  
 Puede utilizar la validación cruzada del Diseñador de minería de datos o puede realizar la validación cruzada ejecutando procedimientos almacenados.  
  
 Si utiliza las herramientas del Diseñador de minería de datos para realizar la validación cruzada, puede configurar los parámetros de resultados de precisión y entrenamiento en un solo cuadro de diálogo. Esto facilita la configuración y la visualización de resultados. Puede medir la precisión de todos los modelos de minería datos relacionados con una estructura de minería de datos única y, a continuación, ver inmediatamente los resultados en un informe HTML. Sin embargo, los procedimientos almacenados proporcionan algunas ventajas, como las personalizaciones agregadas y la capacidad de incluir en un script el proceso.  
  
### <a name="cross-validation-in-data-mining-designer"></a>Validación cruzada en el Diseñador de minería de datos  
 Puede realizar la validación cruzada mediante la pestaña **Validación cruzada** de la vista Gráfico de precisión de minería de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o SQL Server Development Studio.  
  
 Para obtener un ejemplo de cómo crear un informe de validación cruzada mediante la interfaz de usuario, vea [Crear un informe de validación cruzada](../../analysis-services/data-mining/create-a-cross-validation-report.md).  
  
### <a name="cross-validation-stored-procedures"></a>Procedimientos almacenados de validación cruzada  
 Para los usuarios avanzados, la validación cruzada también está disponible en forma de procedimientos almacenados del sistema totalmente parametrizados. Puede ejecutar los procedimientos almacenados conectándose a una instancia de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o desde cualquier aplicación de código administrado.  
  
 Los procedimientos almacenados se agrupan por tipo de modelo de minería de datos. Un conjunto de procedimientos funciona solo con modelos de agrupación en clústeres. El otro conjunto de procedimientos funciona con otros modelos de minería de datos.  
  
 Para cada tipo de modelo de minería de datos, en clúster o sin clúster, los procedimientos almacenados realizan la validación cruzada en dos fases independientes.  
  
 **Realizar particiones de datos y generar métricas para particiones**  
  
 En la primera fase, llama a un procedimiento almacenado del sistema que crea tantas particiones como especifique dentro del conjunto de datos y devuelve los resultados de precisión para cada partición. Para cada métrica, Analysis Services calcula entonces las desviaciones media y estándar para las particiones.  
  
-   [SystemGetCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterCrossValidationResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)  
  
 **Generar métricas para todo el conjunto de datos**  
  
 En la segunda fase, llama a otro conjunto de procedimientos almacenados. Estos procedimientos almacenados no crean particiones del conjunto de datos, pero generan resultados de precisión para el conjunto de datos especificados como un todo. Si ha creado particiones y ha procesado una estructura de minería de datos, puede llamar a este segundo conjunto de procedimientos almacenados para obtener los resultados.  
  
-   [SystemGetAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)  
  
-   [SystemGetClusterAccuracyResults &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
#### <a name="defining-the-testing-data"></a>Definir los datos de prueba  
 Al ejecutar los procedimientos almacenados de validación cruzada que calculan la precisión (SystemGetAccuracyResults o SystemGetClusterAccuracyResults), puede especificar el origen de los datos que se usan para realizar pruebas durante la validación cruzada. Esta opción no está disponible en la interfaz de usuario.  
  
 Puede especificar como origen de datos de prueba cualquiera de las siguientes opciones:  
  
-   Usar solo los datos de aprendizaje.  
  
-   Incluir un conjunto de datos de pruebas existente.  
  
-   Usar solo el conjunto de datos de pruebas.  
  
-   Aplicar los filtros existentes a cada modelo.  
  
-   Cualquier combinación del conjunto de entrenamiento, conjunto de pruebas y filtros de modelos.  
  
 Para especificar un origen de datos de prueba, proporcione un valor entero para el parámetro **DataSet** del procedimiento almacenado. Para obtener una lista de los valores de argumento, vea la sección Notas del tema de referencia sobre los procedimientos almacenados correspondiente.  
  
 Si realiza una validación cruzada mediante el informe **Validación cruzada** en el Diseñador de minería de datos, no puede cambiar el conjunto de datos que se usa. De forma predeterminada, se usan los casos de entrenamiento para cada modelo. Si un filtro está asociado a un modelo, se aplica dicho filtro.  
  
## <a name="results-of-cross-validation"></a>Resultados de la validación cruzada  
 Si usa el Diseñador de minería de datos, estos resultados se muestran en un visor Web similar a una cuadrícula. Si usa los procedimientos almacenados de validación cruzada, estos mismos resultados se devuelven como una tabla.  
  
 El informe contiene dos tipos de acciones: agregados que indican la variabilidad del conjunto de datos cuando se divide en subconjuntos y medidas específicas del modelo de la precisión para cada plegamiento. En los siguientes temas se proporciona más información sobre estas métricas:  
  
 [Fórmulas de validación cruzada](../../analysis-services/data-mining/cross-validation-formulas.md)  
  
 Enumera todas las medidas por el tipo de prueba. Describe en general cómo se pueden interpretar las medidas.  
  
 [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)  
  
 Describe las fórmulas para calcular cada medida y muestra el tipo de atributo en el que cada medida se puede aplicar.  
  
## <a name="restrictions-on-cross-validation"></a>Restricciones sobre la validación cruzada  
 Si realiza una validación cruzada utilizando el informe de validación cruzada de SQL Server Development Studio,, existen algunas limitaciones en los modelos que puede probar y en los parámetros que puede establecer.  
  
-   De forma predeterminada, se realizará una validación cruzada de todos los modelos asociados a la estructura de minería de datos seleccionada. No puede especificar el modelo o una lista de modelos.  
  
-   No se admite el uso de la validación cruzada en modelos que estén basados en el algoritmo de serie temporal de Microsoft o en el algoritmo de clústeres de secuencia de Microsoft.  
  
-   No se podrá crear el informe si su estructura de minería de datos no contiene ningún modelo que pueda probar la validación cruzada.  
  
-   Si la estructura de minería de datos contiene tanto modelos de agrupación en clústeres como modelos de no agrupación en clústeres y no elige la opción **Nº de clústeres** , los resultados para ambos tipos de modelos se mostrarán en el mismo informe, incluso aunque el atributo, el estado y la configuración del umbral no sean adecuados para el modelo de agrupación en clústeres.  
  
-   Algunos valores de los parámetros están restringidos. Por ejemplo, se mostrará una advertencia si el número de plegamientos es superior a 10, ya que generar tantos modelos podría provocar la ralentización de la presentación del informe.  
  
 Si prueba varios modelos de minería de datos y estos tienen filtros, cada modelo se filtra por separado. No se puede agregar a un modelo un nuevo filtro o cambiar uno existente durante la validación cruzada.  
  
 Dado que la validación cruzada prueba de manera predeterminada todos los modelos de minería de datos asociados a una estructura, puede recibir resultados incoherentes si algunos modelos tienen un filtro y otros no. Para asegurarse de que compara solo los modelos que tienen el mismo filtro, debería usar los procedimientos almacenados y especificar una lista de modelos de minería de datos. O bien, use solo el conjunto de pruebas de la estructura de minería de datos sin filtros para asegurarse de que se usa un conjunto coherente de datos para todos los modelos.  
  
 Si realiza una validación cruzada utilizando procedimientos almacenados, tiene la opción adicional de elegir el origen de datos de prueba. Si realiza una validación cruzada utilizando el Diseñador de minería de datos, debe utilizar el conjunto de datos de prueba que esté asociado al modelo o a la estructura, si existe. Por lo general, si desea especificar la configuración avanzada, debe utilizar los procedimientos almacenados de la validación cruzada.  
  
 La validación cruzada no se puede utilizar con modelos de clústeres de secuencia o serie temporal. Concretamente, ningún modelo que contenga una columna KEY TIME o una columna KEY SEQUENCE puede incluirse en la validación cruzada.  
  
## <a name="related-content"></a>Contenido relacionado  
 Vea los siguientes temas para obtener más información sobre la validación cruzada o la información sobre los métodos relacionados para probar los modelos de minería de datos, como gráficos de precisión.  
  
|Temas|Vínculos|  
|------------|-----------|  
|Describe cómo establecer los parámetros de validación cruzada en SQL Server Development Studio.|[Pestaña Validación cruzada &#40;vista Gráfico de precisión de minería de datos&#41;](http://msdn.microsoft.com/library/bd215a68-1ad7-4046-9c44-ec8e2be13a64)|  
|Describe las métricas que proporciona la validación cruzada|[Fórmulas de validación cruzada](../../analysis-services/data-mining/cross-validation-formulas.md)|  
|Explica el formato del informe de validación cruzada y define las medidas estadísticas proporcionadas para cada tipo de modelo.|[Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)|  
|Enumera los procedimientos almacenados para calcular las estadísticas de validación cruzada.|[Procedimientos almacenados de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/data-mining-stored-procedures-analysis-services-data-mining.md)|  
|||  
|Describe cómo crear un conjunto de datos de pruebas para las estructuras y los modelos relacionados.|[Conjuntos de datos de entrenamiento y de prueba](../../analysis-services/data-mining/training-and-testing-data-sets.md)|  
|Vea los ejemplos de otros tipos de gráficos de precisión.|[Matriz de clasificación &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)<br /><br /> [Gráfico de mejora respecto al modelo predictivo &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de beneficios &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/profit-chart-analysis-services-data-mining.md)<br /><br /> [Gráfico de dispersión &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/scatter-plot-analysis-services-data-mining.md)|  
|Describe los pasos para crear varios gráficos de precisión.|[Tareas y procedimientos de prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)|  
  
## <a name="see-also"></a>Vea también  
 [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  

