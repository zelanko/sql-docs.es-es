---
title: Conjuntos de datos de prueba y entrenamiento | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- testing mining models
- holdout [data mining]
- testing data mining models
- accuracy testing [data mining]
ms.assetid: 5798fa48-ef3c-4e97-a17c-38274970fccd
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 880f294f82a0aaa34904d78191d41217fecc78c9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="training-and-testing-data-sets"></a>Conjuntos de datos de entrenamiento y de prueba
  Separar los datos en conjuntos de entrenamiento y de prueba es una parte importante de la evaluación de los modelos de minería de datos. Normalmente, al dividir un conjunto de datos en un conjunto de entrenamiento y un conjunto de prueba, la mayoría de los datos se usan para el entrenamiento y una parte menor se emplea para las pruebas. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestrea los datos de forma aleatoria para asegurarse de que los conjuntos de entrenamiento y de prueba son similares. Si usa datos similares para el entrenamiento y las pruebas, puede minimizar los efectos de las diferencias en los datos y comprender mejor las características del modelo.  
  
 Una vez procesado un modelo utilizando el conjunto de entrenamiento, se prueba realizando predicciones con el conjunto de pruebas. Dado que los datos del conjunto de prueba ya contienen valores conocidos para el atributo que desea predecir, es fácil determinar si las estimaciones del modelo son correctas.  
  
## <a name="creating-test-and-training-sets-for-data-mining-structures"></a>Crear conjuntos de entrenamiento y de prueba para las estructuras de minería de datos  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], el conjunto de datos original se separa en el nivel de la estructura de minería de datos. La información sobre el tamaño de los conjuntos de datos de entrenamiento y de prueba, y qué filas pertenecen a cada conjunto, se almacena junto con la estructura, y todos los modelos basados en esa estructura pueden usar los conjuntos de entrenamiento y de prueba.  
  
 Para definir un conjunto de datos de prueba en una estructura de minería de datos puede realizar una de las acciones siguientes:  
  
-   Usar el Asistente para minería de datos para dividir la estructura de minería de datos en el momento de crearla.  
  
-   Modificar las propiedades de la estructura en la pestaña **Estructura de minería de datos** del Diseñador de minería de datos.  
  
-   Crear y modificar estructuras mediante programación si usa Objetos de administración de análisis (AMO) o el Lenguaje de definición de datos XML (DDL).  
  
### <a name="using-the-data-mining-wizard-to-divide-a-mining-structure"></a>Usar el Asistente para minería de datos para dividir una estructura de minería de datos  
 De forma predeterminada, después de haber definido los orígenes de datos para una estructura de minería de datos, el Asistente para minería de datos dividirá los datos en dos conjuntos: uno con el 70 por ciento de los datos de origen para entrenar el modelo y otro con el 30 por ciento para probarlo. Se ha elegido este valor predeterminado porque la proporción 70-30 suele usarse en la minería de datos, pero con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede cambiarla para que se ajuste a sus requisitos.  
  
 También puede configurar el asistente para establecer un número máximo de casos de entrenamiento o bien, puede combinar los límites para permitir un porcentaje máximo de casos hasta un número máximo especificado de casos. Al especificar ambos un porcentaje máximo de casos y un número máximo de casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa el menor de los dos límites como el tamaño del conjunto de pruebas. Por ejemplo, si especifica una exclusión del 30 por ciento para los casos de pruebas, y el número máximo de casos de pruebas como 1000, el tamaño del conjunto de pruebas nunca superará 1000 casos. Esto puede ser útil si desea asegurarse de que el tamaño de su conjunto de pruebas permanece coherente incluso si se agregan más datos de aprendizaje al modelo.  
  
 Si usa la misma vista del origen de datos para diferentes estructuras de minería de datos, y desea asegurarse de que los datos se dividen aproximadamente de la misma manera para todas las estructuras de minería de datos y sus modelos, debe especificar el valor de inicialización que se usa para inicializar el muestreo aleatorio. Al especificar un valor para **HoldoutSeed**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará ese valor para empezar el muestreo. De lo contrario, el muestreo aplica un algoritmo hash al nombre de la estructura de minería de datos para crear el valor de inicialización.  
  
> [!NOTE]  
>  Si crea una copia de la estructura de minería de datos mediante las instrucciones **EXPORT** e **IMPORT** , la nueva estructura de minería de datos tendrá los mismos conjuntos de datos de entrenamiento y de prueba porque el proceso de exportación crea un nuevo identificador, aunque usa el mismo nombre. Sin embargo, si dos estructuras de minería de datos usan el mismo origen de datos subyacente, pero tienen nombres diferentes, los conjuntos creados para cada estructura de minería de datos serán diferentes.  
  
### <a name="modifying-structure-properties-to-create-a-test-data-set"></a>Modificar las propiedades de la estructura para crear un conjunto de datos de prueba  
 Si crea y procesa una estructura de minería de datos y, a continuación, decide que desea reservar un conjunto de datos de prueba, puede modificar las propiedades de la estructura de minería de datos. Para cambiar la manera en que se crean las particiones de los datos, modifique las propiedades siguientes:  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**HoldoutMaxCases**|Especifica el número máximo de casos que se van a incluir en el conjunto de pruebas.|  
|**HoldoutMaxPercent**|Especifica el número de casos que se van a incluir en el conjunto de pruebas como porcentaje del conjunto de datos completo. Para no tener ningún conjunto de datos, especificaría 0.|  
|**HoldoutSeed**|Especifica un valor entero para usarlo como valor de inicialización al seleccionar los datos para las particiones de forma aleatoria. Este valor no afecta al número de casos del conjunto de entrenamiento; sino que sirve para asegurarse de que la partición se puede repetir.|  
  
 Si agrega un conjunto de datos de prueba a una estructura existente, o lo cambia, deberá volver a procesar la estructura y todos los modelos asociados. Además, dado que dividir el origen de datos hace que el modelo se entrene con un subconjunto diferente de los datos, podría ver resultados diferentes del modelo.  
  
### <a name="specifying-holdout-programmatically"></a>Especificar los datos de exclusión mediante programación  
 Puede definir conjuntos de datos de entrenamiento y de prueba en una estructura de minería de datos usando instrucciones DMX, AMO o XML DDL. La instrucción ALTER MINING STRUCTURE no admite el uso de parámetros de datos de exclusión.  
  
-   **DMX** En el lenguaje de Extensiones de minería de datos (DMX), la instrucción CREATE MINING STRUCTURE se ha extendido para incluir una cláusula WITH HOLDOUT.  
  
-   **ASSL** Puede crear una estructura de minería de datos o agregar un conjunto de datos de prueba a una estructura de minería de datos existente con el lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL).  
  
-   **AMO** También puede ver y modificar los conjuntos de datos de exclusión mediante AMO.  
  
 Para ver información sobre el conjunto de datos de exclusión de una estructura de minería de datos existente, haga una consulta en el conjunto de filas de esquema de minería de datos. Para hacer esto, puede realizar una llamada a DISCOVER ROWSET o puede usar una consulta DMX.  
  
## <a name="retrieving-information-about-holdout-data"></a>Recuperar información acerca de los datos de exclusión  
 De forma predeterminada, toda la información sobre los conjuntos de datos de entrenamiento y de prueba se almacena en la memoria caché con el fin de que pueda usar los datos existentes para entrenar y probar los nuevos modelos. También puede definir filtros y aplicarlos a los datos de exclusión almacenados en caché para evaluar el modelo con los subconjuntos de los datos.  
  
 La manera en que los casos se dividen en conjuntos de datos de entrenamiento y de prueba depende de la forma en que se configuren los datos de exclusión y en los datos que se proporcionen. Si desea determinar el número de casos usados para el entrenamiento o las pruebas, o buscar detalles adicionales sobre los casos incluidos en los conjuntos de entrenamiento y de prueba, puede consultar la estructura de modelo creando una consulta DMX. Por ejemplo, la consulta siguiente devuelve los casos usados en el conjunto de entrenamiento del modelo.  
  
```  
SELECT * from <structure>.CASES WHERE IsTrainingCase()  
```  
  
 Para recuperar solo los casos de prueba y además filtrarlos según el valor contenido en una de las columnas de la estructura de minería de datos, use la sintaxis siguiente:  
  
```  
SELECT * from <structure>.CASES WHERE IsTestCase() AND <structure column name> = '<value>'  
```  
  
## <a name="limitations-on-the-use-of-holdout-data"></a>Limitaciones en el uso de los datos de exclusión  
  
-   Para usar datos de exclusión, es necesario establecer la propiedad <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> de la estructura de minería en el valor predeterminado, **KeepTrainingCases**. Si cambia la propiedad **CacheMode** a **ClearAfterProcessing**y, a continuación, vuelve a procesar la estructura de minería de datos, se perderá la partición.  
  
-   No puede quitar datos de un modelo de serie temporal; por consiguiente, no puede dividir los datos de origen en conjuntos de entrenamiento y de prueba. Si empieza a crear una estructura y un modelo de minería de datos, y elige el algoritmo de serie temporal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , la opción que permite crear un conjunto de datos de exclusión aparece deshabilitada. También se deshabilita el uso de datos de exclusión si la estructura de minería de datos contiene una columna KEY TIME en el nivel de tabla anidada o caso.  
  
-   Se puede configurar accidentalmente el conjunto de datos de exclusión de tal manera que el conjunto de datos completo se use para las pruebas y no queden datos para el entrenamiento. Sin embargo, si lo hace, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mostrará un error para que pueda corregir el problema. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también le advierte si al procesar la estructura más del 50 por ciento de los datos se han reservado para las pruebas.  
  
-   En la mayoría de los casos, el valor de exclusión predeterminado de 30 proporciona un buen equilibrio entre los datos de pruebas y los de entrenamiento. No es fácil determinar lo grande que debería ser el conjunto de datos para proporcionar entrenamiento suficiente, ni el grado de dispersión que puede alcanzar el conjunto de entrenamiento antes de que se llegue al sobreajuste. Sin embargo, después de haber generado un modelo, puede usar la validación cruzada para evaluar el conjunto de datos con respecto a un modelo determinado.  
  
-   Además de las propiedades indicadas en la tabla anterior, se proporciona una propiedad de solo lectura, **HoldoutActualSize**, en AMO y XML DDL. Sin embargo, dado que el tamaño real de una partición no se puede determinar con precisión hasta que se ha procesado la estructura, debería comprobar si se ha procesado el modelo antes de recuperar el valor de la propiedad **HoldoutActualSize** .  
  
## <a name="related-content"></a>Contenido relacionado  
  
|Temas|Vínculos|  
|------------|-----------|  
|Describe cómo interactúan los filtros de un modelo con los conjuntos de datos de entrenamiento y de prueba.|[Filtros para modelos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)|  
|Describe cómo afecta a la validación cruzada el uso de los datos de entrenamiento y de prueba.|[Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md)|  
|Proporciona información sobre las interfaces de programación para trabajar con conjuntos de entrenamiento y de prueba en una estructura de minería de datos.|[Modelo de objetos y conceptos de AMO](../../analysis-services/multidimensional-models/analysis-management-objects/amo-concepts-and-object-model.md)<br /><br /> [Elemento MiningStructure &#40;ASSL&#41;](../../analysis-services/scripting/objects/miningstructure-element-assl.md)|  
|Proporciona la sintaxis DMX para crear conjuntos de datos de exclusión.|[CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md)|  
|Recupera información sobre los casos de los conjuntos de entrenamiento y de prueba.|[Conjuntos de filas de esquema de minería de datos](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)<br /><br /> [Conjuntos de filas de esquema de minería de datos &#40;SSA&#41;](../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)|  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)   
 [Conceptos de minería de datos](../../analysis-services/data-mining/data-mining-concepts.md)   
 [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
  
