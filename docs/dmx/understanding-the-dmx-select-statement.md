---
title: Descripción de la instrucción SELECT de DMX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8cc28e9394cabee4dd32e8e84ee02517de415a75
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893068"
---
# <a name="understanding-the-dmx-select-statement"></a>Descripción de la instrucción Select de DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  La instrucción [Select](../dmx/select-dmx.md) es la base de la mayoría de las consultas que se crean con extensiones de minería de [!INCLUDE[msCoName](../includes/msconame-md.md)] datos (DMX) en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Puede realizar muchos tipos distintos de tareas, como examinar modelos de minería de datos y realizar predicciones con ellos.  
  
 A continuación se indican las tareas que puede realizar con la instrucción **Select** :  
  
-   Examinar un modelo de minería de datos. El conjunto de filas de esquema define la estructura de un modelo.  
  
-   Descubrir los valores posibles de una columna de modelo de minería de datos.  
  
-   Examinar los casos asignados a nodos en un modelo de minería de datos u obtener un caso representativo.  
  
-   Crear predicciones mediante diversas entradas.  
  
-   Copiar modelos de minería de datos.  
  
 Cada una de estas tareas utiliza un conjunto de datos diferente, al que llamaremos un *dominio de datos*. El dominio de datos se define en la cláusula **from** de la instrucción.  
  
-   Desea buscar objetos en el propio modelo de minería de datos, como la regla que define un conjunto de datos, o una fórmula empleada para realizar predicciones.  
  
     En ese caso, debe examinar los metadatos almacenados en el propio modelo. Por tanto, el dominio de datos lo forman las columnas del conjunto de filas del esquema de minería de datos.  
  
-   Desea obtener información detallada de los casos usados para generar el modelo.  
  
     En ese caso, debe obtener detalles de la estructura de minería de datos, que es el dominio de datos, y examinar las filas individuales de columnas como Gender, Bike Buyer, etc.  
  
 **IMPORTANTE:** Todo lo que se incluye en la lista de expresiones o en la cláusula **Where** debe proviene del dominio de datos definido por la cláusula **from** . No puede mezclar dominios de datos.  
  
##  <a name="Select_Types"></a>SELECCIONAR tipos  
 La sintaxis de la instrucción **Select** admite muchas tareas diferentes. Use los patrones siguientes para realizar estas tareas:  
  
-   [Predecir](#Predicting)  
  
-   [Exploración](#Browsing)  
  
-   [Instantánea](#Copying)  
  
-   [Detalles](#Drillthrough)  
  
###  <a name="Predicting"></a>Predecir  
 Puede realizar predicciones basadas en un modelo de minería usando los siguientes tipos de consulta.  
  
 Puede incluir cualquiera de las instrucciones **Select** de exploración o de predicción en las cláusulas **from** y **Where** de una instrucción de **selección** de combinación de predicción.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|SELECCIONAR DESDE [NATURAL] COMBINACIÓN DE PREDICCIÓN|Devuelve una predicción que se crea combinando las columnas del modelo de minería de datos con las columnas de un origen de datos interno.<br /><br /> El dominio de este tipo de consulta lo forman las columnas de predicción del modelo y las columnas del origen de datos de entrada.<br /><br /> [Seleccionar de &#60;la&#62; combinación &#40;de predicción de modelo DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Consultas de predicción &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|Seleccionar del  *\<modelo >*|Devuelve el estado más probable de la columna de predicción, basándose únicamente en el modelo de minería de datos. Este tipo de consulta es un método abreviado para crear una predicción con una combinación de predicción vacía.<br /><br /> El dominio de este tipo de consulta lo forman las columnas de predicción del modelo.<br /><br /> [Seleccionar del &#60;modelo&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Consultas de predicción &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [Volver a seleccionar tipos](#Select_Types)  
  
###  <a name="Browsing"></a>Exploración  
 Puede examinar el contenido de un modelo de minería de datos usando los siguientes tipos de consulta.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|Seleccione DISTINCT from  *\<Model >*|Devuelve todos los valores de estado del modelo de minería de datos para la columna especificada.<br /><br /> El dominio de datos de este tipo de consulta es el modelo de minería de datos.<br /><br /> [Seleccione DISTINCT &#60;from &#62; &#40;Model DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Consultas de contenido &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Seleccione del  *\<modelo >* . CONTENT|Devuelve contenido que describe el modelo de minería de datos.<br /><br /> El dominio de datos este tipo de consulta es el conjunto de filas de esquema CONTENT.<br /><br /> [Seleccione del &#60;modelo&#62;. CONTENT &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Consultas de contenido &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Seleccione del  *\<modelo >* . DIMENSION_CONTENT|Devuelve contenido que describe el modelo de minería de datos.<br /><br /> El dominio de datos este tipo de consulta es el conjunto de filas de esquema CONTENT.<br /><br /> [Seleccione del &#60;modelo&#62;. DMX &#40;DIMENSION_CONTENT&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|Seleccione del  *\<modelo >* . PMML|Devuelve la representación PMML (Lenguaje de marcado de modelos de predicción) del modelo de minería de datos para los algoritmos que admiten esta funcionalidad.<br /><br /> El dominio de este tipo de consulta es el conjunto de filas de esquema PMML.<br /><br /> [Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|  
  
 [Volver a seleccionar tipos](#Select_Types)  
  
###  <a name="Copying"></a>Instantánea  
 Puede copiar un modelo de minería de datos y su estructura de minería de datos asociada a un nuevo modelo y cambiar después el nombre del modelo dentro de la instrucción.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|Seleccione en  *\<nuevo modelo >*|Crea una copia del modelo de minería de datos.<br /><br /> El dominio de este tipo de consulta es el modelo de minería de datos.<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [Volver a seleccionar tipos](#Select_Types)  
  
###  <a name="Drillthrough"></a>Detalles  
 Puede examinar los escenarios (o una representación de los escenarios) que se emplearon para entrenar el modelo usando los siguientes tipos de consulta.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|Seleccione del  *\<modelo >* . VECES|Devuelve los casos empleados para entrenar el modelo de minería de datos.<br /><br /> El dominio de este tipo de consulta es el modelo de minería de datos.<br /><br /> [Seleccione del &#60;modelo&#62;. DMX &#40;de casos&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Crear consultas de obtención de detalles usando DMX](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|Seleccione del  *\<modelo >* . SAMPLE_CASES|Devuelve un caso de ejemplo, representativo de los casos empleados para entrenar el modelo de minería de datos.<br /><br /> El dominio de este tipo de consulta es el modelo de minería de datos.<br /><br /> [Seleccione del &#60;modelo&#62;. DMX &#40;SAMPLE_CASES&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|Seleccione de  *\<la estructura >* . VECES|Devuelve las filas de datos detalladas de la estructura de minería de datos subyacente, aunque algunos detalles no se usaran al entrenar el modelo de minería de datos.<br /><br /> [Seleccione de &#60;la&#62;estructura. VECES](../dmx/select-from-structure-cases.md)<br /><br /> [Consultas de obtención de detalles &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [Volver a seleccionar tipos](#Select_Types)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de la &#40;instrucción&#41; DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
