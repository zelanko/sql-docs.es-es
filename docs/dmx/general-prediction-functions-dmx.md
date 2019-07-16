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
ms.openlocfilehash: 8eff7603fa0d0be0e90af201e524554f5e336ea8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67937799"
---
# <a name="general-prediction-functions-dmx"></a>Funciones de predicción generales (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede usar el **seleccione** instrucción minería de datos extensiones (DMX) para crear diferentes tipos de consultas. Se puede utilizar una consulta para devolver información sobre el modelo de minería de datos, para realizar predicciones nuevas o para modificar el modelo entrenándolo con datos nuevos. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Proporciona una variedad de funciones especializadas que controlan el tipo de información que se devuelve en una consulta. Si agrega estas funciones a una consulta de DMX, puede recuperar estadísticas o columnas de datos adicionales. Sin embargo, cada tipo de consulta y cada tipo de modelo solamente admite determinadas funciones.  
  
## <a name="common-functions"></a>Funciones comunes  
 Puede utilizar funciones para ampliar los resultados que devuelve un modelo de minería de datos. Puede usar las siguientes funciones para cualquier **seleccione** instrucción que devuelve una expresión de tabla:  
  
|||  
|-|-|  
|[BottomCount &#40;DMX&#41;](../dmx/bottomcount-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)|  
|[BottomPercent &#40;DMX&#41;](../dmx/bottompercent-dmx.md)|[TopCount &#40;DMX&#41;](../dmx/topcount-dmx.md)|  
|[Predict &#40;DMX&#41;](../dmx/predict-dmx.md)|[TopPercent &#40;DMX&#41;](../dmx/toppercent-dmx.md)|  
|[RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|[TopSum &#40;DMX&#41;](../dmx/topsum-dmx.md)|  
|[RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)||  
  
 Además, las funciones siguientes son compatibles con casi todos los tipos de modelo:  
  
-   [Existe &#40;DMX&#41;](../dmx/exists-dmx.md)  
  
-   [IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)  
  
-   [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)  
  
-   [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)  
  
-   [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)  
  
-   [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)  
  
-   [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)  
  
-   [RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)  
  
-   [StructureColumn &#40;DMX&#41;](../dmx/structurecolumn-dmx.md)  
  
 Algunos algoritmos pueden ser compatibles con funciones adicionales. Para obtener una lista de las funciones que son compatibles con cada tipo de modelo, vea [consultas de minería de datos](../analysis-services/data-mining/data-mining-queries.md).  
  
## <a name="functions-specific-to-select-syntax"></a>Funciones específicas para la sintaxis SELECT  
 En la tabla siguiente se enumera las funciones que puede usar para cada tipo de **seleccione** instrucción.  
  
 Para obtener información general sobre las funciones de DMX, vea [extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md).  
  
|Tipo de consulta|Funciones admitidas|Comentarios|  
|----------------|-------------------------|-------------|  
|[SELECT DISTINCT FROM \<modelo >](../dmx/select-distinct-from-model-dmx.md)|[RangeMin &#40;DMX&#41;](../dmx/rangemin-dmx.md)<br /><br /> [RangeMid &#40;DMX&#41;](../dmx/rangemid-dmx.md)<br /><br /> [RangeMax &#40;DMX&#41;](../dmx/rangemax-dmx.md)|Estas funciones se pueden utilizar para proporcionar valores máximos, valores mínimos y valores medios para cualquier columna que contenga datos numéricos, con independencia de si la columna es continua o de datos discretos.|  
|[SELECT FROM \<modelo >. CONTENIDO](../dmx/select-from-model-content-dmx.md)<br /><br /> o Administrador de configuración de<br /><br /> [SELECT FROM \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md)|[IsDescendant &#40;DMX&#41;](../dmx/isdescendant-dmx.md)|Esta función recupera los nodos secundarios para el nodo especificado del modelo y se puede utilizar, por ejemplo, para recorrer en iteración los nodos del contenido del modelo de minería de datos. La organización de los nodos en el contenido del modelo de minería de datos depende del tipo de modelo. Para obtener información acerca de la estructura para cada tipo de modelo de minería de datos, vea [contenido del modelo de minería de datos &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md).<br /><br /> Si ha guardado el contenido del modelo de minería de datos como una dimensión, también puede utilizar otras funciones de MDX (Expresiones multidimensionales) que permiten consultar una jerarquía de atributos.|  
|[SELECT FROM \<modelo >. CASOS](../dmx/select-from-model-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)<br /><br /> [Clase ClientSettingsGeneralFlag](../relational-databases/wmi-provider-configuration-classes/clientsettingsgeneralflag-class/clientsettingsgeneralflag-class.md)<br /><br /> [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md)<br /><br /> [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md)|La función Lag solo se admite para los modelos de serie temporal.<br /><br /> La función IsTestCase se admite en los modelos que se basan en una estructura que se creó con la opción de exclusión, para crear un conjunto de datos de prueba. Si el modelo no se basa en una estructura con el conjunto de datos de pruebas con exclusión, todos los casos se consideran casos de entrenamiento.|  
|[SELECT FROM \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md)|[IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md)|En este contexto, la función IsInNode devuelve un caso de que pertenece a un conjunto de casos de ejemplo idealizados.|  
|SELECT FROM \<modelo >. PMML|No aplicable. En su lugar, utilice las funciones de consultas XML.|Las representaciones PMML solo son compatibles con los tipos de modelo siguientes:<br /><br /> Árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)]<br /><br /> Agrupación en clústeres de [!INCLUDE[msCoName](../includes/msconame-md.md)]|  
|[SELECT FROM \<modelo > PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md)|Funciones de predicción específicas del algoritmo que se emplea para generar el modelo.|Para obtener una lista de funciones de predicción para cada tipo modelo, vea [consultas de minería de datos](../analysis-services/data-mining/data-mining-queries.md).|  
|[SELECT FROM \<modelo >](../dmx/select-from-model-dmx.md)|Funciones de predicción específicas del algoritmo que se emplea para generar el modelo.|Para obtener una lista de funciones de predicción para cada tipo modelo, vea [consultas de minería de datos](../analysis-services/data-mining/data-mining-queries.md).|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
