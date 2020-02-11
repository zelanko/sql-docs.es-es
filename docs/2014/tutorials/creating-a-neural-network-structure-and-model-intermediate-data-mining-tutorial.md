---
title: Crear un modelo y una estructura de red neuronal (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- DISCRETIZED column
- DiscretizationBuckets property
- DiscretizationMethod property
- EQUAL_AREAS method
ms.assetid: 3f16215c-531e-4ecf-a11f-ee7c6a764463
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6787db165770f944838a312ecd3e0386d161da38
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856327"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>Crear una estructura y un modelo de red neuronal (Tutorial intermedio de minería de datos)
  Para crear un modelo de minería de datos, debe usar en primer lugar el Asistente para minería de datos con el objeto de crear una nueva estructura de minería de datos basada en la nueva vista del origen de datos. En esta tarea, utilizará el asistente para crear una estructura de minería de datos y al mismo tiempo crear el modelo inicial de minería de datos que se basa en el algoritmo de red neuronal de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Dado que las redes neuronales son extremadamente flexibles y pueden analizar diferentes combinaciones de entradas y salidas, debe realizar pruebas con diferentes métodos de procesamiento de los datos para obtener los mejores resultados. Por ejemplo, puede que desee personalizar la manera en que el destino numérico de la calidad del servicio es *discretizan*, o agrupado, para satisfacer los requisitos empresariales específicos. Para ello, agregará una columna nueva a la estructura de minería de datos que agrupa los datos numéricos de una manera diferente y, a continuación, creará un modelo que use la columna nueva. Utilizará estos modelos de minería de datos para hacer una exploración.  
  
 Finalmente, cuando haya aprendido del modelo de red neuronal qué factores tienen el mayor impacto para su cuestión comercial, construirá un modelo independiente para la predicción y evaluación. Usará el algoritmo de regresión logística de [!INCLUDE[msCoName](../includes/msconame-md.md)], que se basa en el modelo de redes neuronales, pero está optimizado para buscar una solución basada en entradas concretas.  
  
 **Pasos**  
  
 [Crear la estructura y el modelo de minería de datos predeterminados](#bkmk_defaul)  
  
 [Usar discretización para enlazar la columna de predicción](#bkmk_ColumnCopy)  
  
 [Copiar la columna y cambiar el método de discretización para un modelo diferente](#bkmk_Alias)  
  
 [Crear un alias para la columna de predicción de manera que se puedan comparar modelos](#bkmk_Alias2)  
  
 [Procesar todos los modelos](#bkmk_SeedProcess)  
  
## Crear la estructura predeterminada del centro de llamadas<a name="bkmk_defaul"></a>  
  
1.  En Explorador de soluciones en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], haga clic con el botón secundario en **estructuras de minería de datos** y seleccione **nueva estructura de minería de datos**.  
  
2.  En la página de inicio del **Asistente para minería de datos** , haga clic en **Siguiente**.  
  
3.  En la página **seleccionar el método de definición** , compruebe que la opción **de base de datos relacional o del almacenamiento de datos existente** está seleccionada y, a continuación, haga clic en **siguiente**.  
  
4.  En la página **crear la estructura de minería de datos** , compruebe que está seleccionada la opción **crear estructura de minería de datos con un modelo de minería de** datos.  
  
5.  Haga clic en la lista desplegable para la opción **¿Qué técnica de minería de datos desea utilizar?** y seleccione **Redes neuronales de Microsoft**.  
  
     Dado que los modelos de regresión logística se basan en las redes neuronales, puede volver a usar la misma estructura y agregar un nuevo modelo de minería de datos.  
  
6.  Haga clic en **Next**.  
  
     Aparece la página **seleccionar vista del origen de datos** .  
  
7.  En **vistas del origen de datos disponibles**, seleccione `Call Center`y haga clic en **siguiente**.  
  
8.  En la página **especificar tipos de tablas** , active la casilla **caso** junto a la tabla **FactCallCenter** . No seleccione nada para **DimDate**. Haga clic en **Next**.  
  
9. En la página **especificar los datos de entrenamiento** , seleccione **clave** junto a la columna **FactCallCenterID.**  
  
10. Active las `Predict` **casillas de verificación y** .  
  
11. Seleccione la **clave**, la **entrada**y `Predict` las casillas como se muestra en la tabla siguiente:  
  
    |Tablas y columnas|Clave/Entrada/Predicción|  
    |---------------------|-------------------------|  
    |AutomaticResponses|Entrada|  
    |AverageTimePerIssue|Entrada/Predicción|  
    |Calls|Entrada|  
    |DateKey|No usar|  
    |DayOfWeek|Entrada|  
    |FactCallCenterID|Clave|  
    |IssuesRaised|Entrada|  
    |LevelOneOperators|Entrada/Predicción|  
    |LevelTwoOperators|Entrada|  
    |Pedidos|Entrada/Predicción|  
    |ServiceGrade|Entrada/Predicción|  
    |Shift|Entrada|  
    |TotalOperators|No usar|  
    |WageType|Entrada|  
  
     Observe que se han seleccionado varias columnas de predicción. Uno de los puntos fuertes del algoritmo de red neuronal es que puede analizar todas las posibles combinaciones de atributos de entrada y salida. No querrá hacer esto para un conjunto de datos grande, ya que podría aumentar exponencialmente el tiempo de procesamiento.  
  
12. En la página **especificar el contenido y el tipo de datos de las columnas** , compruebe que la cuadrícula contiene las columnas, los tipos de contenido y los tipos de datos como se muestra en la tabla siguiente y, a continuación, haga clic en **siguiente**.  
  
    |Columnas|Tipo de contenido|Tipo de datos|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|Continuo|long|  
    |AverageTimePerIssue|Continuo|long|  
    |Calls|Continuo|long|  
    |DayOfWeek|Discrete|Texto|  
    |FactCallCenterID|Clave|long|  
    |IssuesRaised|Continuo|long|  
    |LevelOneOperators|Continuo|long|  
    |LevelTwoOperators|Continuo|long|  
    |Pedidos|Continuo|long|  
    |ServiceGrade|Continuo|DOUBLE|  
    |Shift|Discrete|Texto|  
    |WageType|Discrete|Texto|  
  
13. En la página **crear conjunto de pruebas** , desactive el cuadro de texto de la opción **porcentaje de datos para pruebas**. Haga clic en **Next**.  
  
14. En la página **finalización del asistente** , en **nombre**de la estructura de `Call Center`minería de datos, escriba.  
  
15. En el **nombre del modelo**de minería `Call Center Default NN`de datos, escriba y, a continuación, haga clic en **Finalizar**.  
  
     El cuadro **permitir obtención de detalles** está deshabilitado porque no se puede obtener detalles de los datos con modelos de red neuronal.  
  
16. En Explorador de soluciones, haga clic con el botón secundario en el nombre de la estructura de minería de datos que acaba de crear y seleccione **procesar**.  
  
## <a name="use-discretization-to-bin-the-target-column"></a>Usar discretización para enlazar la columna de destino  
 De forma predeterminada, cuando crea un modelo de red neuronal que incluye un atributo de predicción numérico, el algoritmo de red neuronal de Microsoft lo trata como un número continuo. Por ejemplo, el atributo ServiceGrade es un número que, en teoría, abarca desde 0,00 (se responden todas las llamadas) a 1,00 (cuelgan todos los que han llamado). En este conjunto de datos, los valores tienen la siguiente distribución:  
  
 ![distribución de valores de grado de servicio](../../2014/tutorials/media/skt-service-grade-valuesc.gif "distribución de valores de grado de servicio")  
  
 Como resultado, al procesar el modelo los resultados pueden aparecer de forma diferente a la que se espera. Por ejemplo, si usa la agrupación en clústeres para identificar los mejores grupos de valores, el algoritmo divide los valores de ServiceGrade en intervalos como este: 0,0748051948-0,09716216215. Aunque esta agrupación es matemáticamente precisa, tales intervalos podrían no ser significativos para los usuarios empresariales.  
  
 En este paso, para que el resultado sea más intuitivo, podrá agrupar los valores numéricos de manera diferente, creando copias de la columna de datos numérica.  
  
### <a name="how-discretization-works"></a>Cómo funciona la discretización  
 Analysis Services proporciona varios métodos para discretizar o procesar los datos numéricos. La tabla siguiente muestra las diferencias entre los resultados cuando el atributo ServiceGrade de salida se ha procesado de tres maneras diferentes:  
  
-   Se trata como un número continuo.  
  
-   Se hace que el algoritmo use la agrupación en clústeres para identificar la mejor organización de valores.  
  
-   Se especifica que los números se discreticen mediante el método de áreas iguales.  
  
 Modelo predeterminado (continuo)  
  
|VALOR|SOPORTE TÉCNICO|  
|-----------|-------------|  
|Missing|0|  
|0,09875|120|  
  
 Discretizado mediante agrupación en clústeres  
  
|VALOR|SOPORTE TÉCNICO|  
|-----------|-------------|  
|\<0,0748051948|34|  
|0,0748051948-0,09716216215|27|  
|0,09716216215-0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 Discretizado mediante áreas iguales  
  
|VALOR|SOPORTE TÉCNICO|  
|-----------|-------------|  
|\<0,07|26|  
|0,07-0,00|22|  
|0,09-0,11|36|  
|>= 0,12|36|  
  
> [!NOTE]  
>  Puede obtener estas estadísticas a partir del nodo de estadísticas marginales del modelo una vez que se hayan procesado todos los datos. Para obtener más información sobre el nodo de estadísticas marginales, vea [contenido del modelo de minería de datos para los modelos de red neuronal &#40;Analysis Services-&#41;de minería de datos ](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md).  
  
 En esta tabla, la columna VALUE muestra cómo se ha controlado el número para ServiceGrade. La columna SUPPORT muestra cuántos casos tenían ese valor o pertenecían a ese rango.  
  
-   **Usar números continuos (predeterminado)**  
  
     Si usa el método predeterminado, el algoritmo calcula los resultados de 120 valores distintos, cuyo valor medio es 0,09875. También puede ver el número de valores que faltan.  
  
-   **Discretizar mediante agrupación en clústeres**  
  
     Cuando permite que el algoritmo de clústeres de Microsoft determine la agrupación opcional de valores, el algoritmo agrupa los valores de ServiceGrade en cinco (5) rangos. El número de escenarios de cada rango no se distribuye por igual, como puede ver en la columna.  
  
-   **Discretizar mediante áreas iguales**  
  
     Si elige este método, el algoritmo exige que los valores de los cubos sean del mismo tamaño, lo que a su vez cambia los límites superior e inferior de cada rango. Puede especificar el número de cubos, pero es conveniente evitar que haya muy pocos valores en un cubo.  
  
 Para obtener más información sobre las opciones de discretización, vea [métodos de discretización &#40;&#41;de minería de datos ](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md).  
  
 Como alternativa, en lugar de usar los valores numéricos, podría agregar una columna derivada independiente que clasifique los grados de servicio en intervalos de destino predefinidos, como \<el **mejor** (ServiceGrade = 0,05), **aceptable** (0,10 > ServiceGrade > 0,05) y **malo** (ServiceGrade >= 0,10).  
  
###  <a name="bkmk_newColumn"></a>Crear una copia de una columna y cambiar el método de discretización  
 Realizará una copia de la columna de minería de datos que contiene el atributo de destino, ServiceGrade y cambia la forma en que se agrupan los números. Puede crear varias copias de cualquier columna de una estructura de minería de datos, incluido el atributo de predicción.  
  
 En este tutorial utilizará el método de discretización de áreas iguales y especificará cuatro cubos. Las agrupaciones que resultan de este método están bastante cerca de los valores objetivo que interesan a los usuarios empresariales.  
  
####  <a name="bkmk_ColumnCopy"></a>Para crear una copia personalizada de una columna en la estructura de minería de datos  
  
1.  En el Explorador de soluciones, haga doble clic en la estructura de minería de datos recién creada.  
  
2.  En la pestaña estructura de minería de datos, haga clic en **Agregar una columna de estructura de minería de datos**.  
  
3.  En el cuadro de diálogo **Seleccionar columna** , seleccione ServiceGrade en la columna lista de **origen**y, a continuación, haga clic en **Aceptar**.  
  
     Se agrega una columna nueva a la lista de columnas de la estructura de minería de datos. De forma predeterminada, la nueva columna de minería de datos tiene el mismo nombre que la columna existente, con un sufijo numérico: por ejemplo, ServiceGrade 1. Puede cambiar el nombre de esta columna para que sea más descriptivo.  
  
     También especificará el método de discretización.  
  
4.  Haga clic con el botón secundario en ServiceGrade 1 y seleccione **propiedades**.  
  
5.  En la ventana **propiedades** , busque la propiedad **Name** y cambie el nombre a **Service grade discretizan** .  
  
6.  Aparece un cuadro de diálogo en el que se pregunta si desea realizar el mismo cambio en el nombre de todas las columnas del modelo de minería de datos relacionadas. Haga clic en **No**.  
  
7.  En la ventana **propiedades** , busque el **tipo de datos** de la sección y expándalo si es necesario.  
  
8.  Cambie el valor de la propiedad `Content` de `Continuous` a `Discretized`.  
  
     Ahora están disponibles las propiedades siguientes. Cambie los valores de las propiedades tal como se muestra en la tabla siguiente:  
  
    |Propiedad|Valor predeterminado|Valor nuevo|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|Sin valor|4|  
  
    > [!NOTE]  
    >  El valor predeterminado de <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> es 0, que indica que el algoritmo determina automáticamente el número óptimo de cubos. Por tanto, si desea restablecer el valor predeterminado de esta propiedad, escriba 0.  
  
9. En el diseñador de minería de datos, haga clic en la pestaña **modelos de minería** de datos.  
  
     Observe que al agregar una copia de una columna de la estructura de minería de datos, la marca de uso de la copia se establece automáticamente en `Ignore`. Normalmente, al agregar una copia de una columna a una estructura de minería de datos, no utilizaría la copia para el análisis junto con la columna original o el algoritmo encontrará una correlación fuerte entre las dos columnas que podrían disimular otras relaciones.  
  
##  <a name="bkmk_NewModel"></a>Agregar un nuevo modelo de minería de datos a la estructura de minería de datos  
 Ahora que ha creado una nueva agrupación para el atributo de destino, necesita agregar un nuevo modelo de minería de datos que use la columna de datos discretos. Cuando lo haya hecho, la estructura de minería de datos CallCenter tendrá dos modelos de minería de datos:  
  
-   El modelo de minería de datos, Call Center Default NN, administra los valores de ServiceGrade como un intervalo continuo.  
  
-   Creará un nuevo modelo de minería de datos, Call Center Discretizan NN, que usará como resultado de destino los valores de la columna ServiceGrade, distribuidos en cuatro cubos de igual tamaño.  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>Para agregar un modelo de minería de datos basado en la nueva columna de datos discretos  
  
1.  En Explorador de soluciones, haga clic con el botón secundario en la estructura de minería de datos que acaba de crear y seleccione **abrir**.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Haga clic en **crear un modelo de minería de datos relacionado**.  
  
4.  En el cuadro de diálogo **nuevo modelo de minería de datos** , en `Call Center Binned NN`nombre del **modelo**, escriba. En la lista desplegable **nombre del algoritmo** , seleccione **red neuronal de Microsoft**.  
  
5.  En la lista de columnas contenida en el nuevo modelo de minería de datos, busque ServiceGrade y cambie el uso de `Predict` a `Ignore`.  
  
6.  De igual forma, busque ServiceGrade Binned y cambie el uso de `Ignore` a `Predict`.  
  
##  <a name="bkmk_Alias2"></a>Crear un alias para la columna de destino  
 Normalmente, no puede comparar modelos de minería de datos que usen atributos de predicción diferentes. Sin embargo, puede crear un alias para una columna del modelo de minería de datos. Es decir, puede cambiar el nombre de la columna ServiceGrade Discretizan en el modelo de minería de datos para que tenga el mismo nombre que la columna original. A continuación, puede comparar directamente estos dos modelos en un gráfico de precisión, aunque los datos se discreticen de manera diferente.  
  
###  <a name="bkmk_Alias"></a>Para agregar un alias para una columna de estructura de minería de datos en un modelo de minería de datos  
  
1.  En la pestaña **modelos de minería de datos** , en **estructura**, seleccione ServiceGrade discretizan.  
  
     Tenga en cuenta que la ventana **propiedades** muestra las propiedades del objeto, ScalarMiningStructure columna.  
  
2.  En la columna correspondiente al modelo de minería de datos, ServiceGrade Binned NN, haga clic en la celda que corresponde a la columna ServiceGrade Binned.  
  
     Tenga en cuenta que ahora la ventana **propiedades** muestra las propiedades del objeto, MiningModelColumn.  
  
3.  Busque la propiedad **Name** y cambie el valor a `ServiceGrade`.  
  
4.  Busque la propiedad **Description** y escriba **alias de columna temporal**.  
  
     La ventana **propiedades** debe contener la siguiente información:  
  
    |Propiedad|Value|  
    |--------------|-----------|  
    |**Descripción**|Alias de columna temporal|  
    |**SESIÓN**|ServiceGrade Discretizan|  
    |**Marcas de modelado**||  
    |**Nombre**|Service Grade|  
    |**SourceColumn ID**|Service Grade 1|  
    |**Uso**|Predict|  
  
5.  Haga clic en cualquier parte de la pestaña **modelo de minería de datos** .  
  
     La cuadrícula se actualiza para mostrar el nuevo alias de columna temporal `ServiceGrade`,, junto al uso de la columna. La cuadrícula que contiene la estructura de minería de datos y dos modelos de minería de datos debería tener una apariencia similar a la siguiente:  
  
    |Estructura|Call Center Default NN|Call Center Binned NN|  
    |---------------|----------------------------|---------------------------|  
    ||Red neuronal de Microsoft|Red neuronal de Microsoft|  
    |AutomaticResponses|Entrada|Entrada|  
    |AverageTimePerIssue|Predict|Predict|  
    |Calls|Entrada|Entrada|  
    |DayOfWeek|Entrada|Entrada|  
    |FactCallCenterID|Clave|Clave|  
    |IssuesRaised|Entrada|Entrada|  
    |LevelOneOperators|Entrada|Entrada|  
    |LevelTwoOperators|Entrada|Entrada|  
    |Pedidos|Entrada|Entrada|  
    |ServiceGrade Binned|Ignore|Predicción (ServiceGrade)|  
    |ServiceGrade|Predict|Ignore|  
    |Shift|Entrada|Entrada|  
    |Total Operators|Entrada|Entrada|  
    |WageType|Entrada|Entrada|  
  
## <a name="process-all-models"></a>Procesar todos los modelos  
 Finalmente, para asegurarse de que los modelos que ha creado se pueden comparar fácilmente, establecerá el parámetro de inicialización del modelo discretizado y del predeterminado. Al establecer un valor de inicialización se garantiza que cada modelo comienza el procesamiento de los datos desde el mismo punto.  
  
> [!NOTE]  
>  Si no se especifica un valor numérico para el parámetro de inicialización, SQL Server Analysis Services lo generará a partir del nombre del modelo. Dado que los modelos siempre tienen nombres diferentes, debe establecer un valor de inicialización para asegurarse de que procesan los datos en el mismo orden.  
  
###  <a name="bkmk_SeedProcess"></a>Para especificar el inicialización y procesar los modelos  
  
1.  En la pestaña **modelo de minería de datos** , haga clic con el botón secundario en la columna del modelo denominado Call Center-LR y seleccione **establecer parámetros de algoritmo**.  
  
2.  En la fila del parámetro HOLDOUT_SEED, haga clic en la celda vacía **** situada debajo de valor `1`y escriba. Haga clic en **OK**. Repita este paso para cada modelo asociado a la estructura.  
  
    > [!NOTE]  
    >  El valor de inicialización que elija no es importante siempre y cuando use el mismo para todos los modelos relacionados.  
  
3.  En el menú **modelos de minería de datos** , seleccione **procesar estructura de minería de datos y todos los modelos**. Haga clic en **sí** para implementar el proyecto de minería de datos actualizado en el servidor.  
  
4.  En el cuadro de diálogo **procesar modelo de minería de datos** , haga clic en **Ejecutar**.  
  
5.  Haga clic en **cerrar** para cerrar el cuadro de diálogo **progreso del proceso** y, a continuación, haga clic de nuevo en **cerrar** en el cuadro de diálogo **procesar modelo de minería de datos** .  
  
 Ahora que ha creado los dos modelos de minería de datos relacionados, explorará los datos para detectar relaciones.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Explorar el modelo de centro de llamadas &#40;tutorial intermedio de minería de datos&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Estructuras de minería de datos &#40;Analysis Services:&#41;de minería de datos](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
