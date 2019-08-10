---
title: Funciones de predicción generales (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 57909c1bb4009ae85b7e1b38b8b3cf3fa0e70ea9
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892770"
---
# <a name="general-prediction-functions-dmx"></a>Funciones de predicción generales (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede utilizar la instrucción **Select** en extensiones de minería de datos (DMX) para crear diferentes tipos de consultas. Se puede utilizar una consulta para devolver información sobre el modelo de minería de datos, para realizar predicciones nuevas o para modificar el modelo entrenándolo con datos nuevos. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]proporciona diversas funciones especializadas que controlan el tipo de información que se devuelve en una consulta. Si agrega estas funciones a una consulta de DMX, puede recuperar estadísticas o columnas de datos adicionales. Sin embargo, cada tipo de consulta y cada tipo de modelo solamente admite determinadas funciones.  
  
## <a name="common-functions"></a>Funciones comunes  
 Puede utilizar funciones para ampliar los resultados que devuelve un modelo de minería de datos. Puede utilizar las siguientes funciones para cualquier instrucción **Select** que devuelva una expresión de tabla:  
  
|||  
|-|-|  
|[DMX &#40;BottomCount&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[DMX &#40;BottomPercent&#41;](../dmx/bottompercent-dmx.md)|[DMX de &#40;topcount&#41;](../dmx/topcount-dmx.md)|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|[DMX de &#40;porcentaje&#41;](../dmx/toppercent-dmx.md)|  
|[DMX &#40;de RangeMax&#41;](../dmx/rangemax-dmx.md)|[&#40;DMX de tops&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 Además, las funciones siguientes son compatibles con casi todos los tipos de modelo:  
  
-   [DMX &#40;existe&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [DMX &#40;IsTestCase&#41;](../dmx/istestcase-dmx.md)  
  
-   [DMX &#40;IsTrainingCase&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [DMX &#40;de RangeMax&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [DMX &#40;StructureColumn&#41;](../dmx/structurecolumn-dmx.md)  
  
 Algunos algoritmos pueden ser compatibles con funciones adicionales. Para obtener una lista de las funciones admitidas por cada tipo de modelo, vea [consultas de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).  
  
## <a name="functions-specific-to-select-syntax"></a>Funciones específicas para la sintaxis SELECT  
 En la tabla siguiente se enumeran las funciones que puede usar para cada tipo de instrucción **Select** .  
  
 Para obtener información general sobre las funciones de DMX, vea [referencia &#40;de&#41; funciones DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo de consulta|Funciones admitidas|Comentarios|  
|----------------|-------------------------|-------------|  
|[Seleccione DISTINCT \<from Model >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [DMX &#40;de RangeMax&#41;](../dmx/rangemax-dmx.md)|Estas funciones se pueden utilizar para proporcionar valores máximos, valores mínimos y valores medios para cualquier columna que contenga datos numéricos, con independencia de si la columna es continua o de datos discretos.|  
|[Seleccione del \<modelo >. CONTENT](../dmx/select-from-model-content-dmx.md)<br /><br /> o Administrador de configuración de<br /><br /> [Seleccione del \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Esta función recupera los nodos secundarios para el nodo especificado del modelo y se puede utilizar, por ejemplo, para recorrer en iteración los nodos del contenido del modelo de minería de datos. La organización de los nodos en el contenido del modelo de minería de datos depende del tipo de modelo. Para obtener información sobre la estructura de cada tipo de modelo de minería de datos, vea [Mining &#40;Model&#41;Content Analysis Services-Data Mining](https://docs.microsoft.com/analysis-services/data-mining/mining-model-content-analysis-services-data-mining).<br /><br /> Si ha guardado el contenido del modelo de minería de datos como una dimensión, también puede utilizar otras funciones de MDX (Expresiones multidimensionales) que permiten consultar una jerarquía de atributos.|  
|[Seleccione del \<modelo >. VECES](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [Clase ClientSettingsGeneralFlag](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [DMX &#40;IsTrainingCase&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [DMX &#40;IsTestCase&#41;](../dmx/istestcase-dmx.md)|La función lag solo se admite para los modelos de serie temporal.<br /><br /> La función IsTestCase se admite en los modelos basados en una estructura que se creó mediante la opción de exclusión, para crear un conjunto de datos de prueba. Si el modelo no se basa en una estructura con el conjunto de datos de pruebas con exclusión, todos los casos se consideran casos de entrenamiento.|  
|[Seleccione del \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|En este contexto, la función IsInNode devuelve un caso que pertenece a un conjunto de casos de ejemplo ideales.|  
|Seleccione del \<modelo >. PMML|No aplicable. En su lugar, utilice las funciones de consultas XML.|Las representaciones PMML solo son compatibles con los tipos de modelo siguientes:<br /><br /> Árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)]<br /><br /> Agrupación en clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)]|  
|[Seleccionar del \<modelo > combinación de predicción](../dmx/select-from-model-prediction-join-dmx.md)|Funciones de predicción específicas del algoritmo que se emplea para generar el modelo.|Para obtener una lista de las funciones de predicción para cada tipo de modelo, vea [consultas de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
|[Seleccionar del \<modelo >](../dmx/select-from-model-dmx.md)|Funciones de predicción específicas del algoritmo que se emplea para generar el modelo.|Para obtener una lista de las funciones de predicción para cada tipo de modelo, vea [consultas de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries).|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de funciones &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia del operador &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de la &#40;instrucción&#41; DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Elementos de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
