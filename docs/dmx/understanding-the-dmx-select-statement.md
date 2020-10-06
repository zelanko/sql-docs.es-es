---
description: Descripción de la instrucción Select de DMX
title: Descripción de la instrucción SELECT de DMX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 14e4c99cd907a5f9a18dd11d77988d728557c4bd
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726066"
---
# <a name="understanding-the-dmx-select-statement"></a>Descripción de la instrucción Select de DMX
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  La instrucción [Select](../dmx/select-dmx.md) es la base de la mayoría de las consultas que se crean con extensiones de minería de datos (DMX) en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Puede realizar muchos tipos distintos de tareas, como examinar modelos de minería de datos y realizar predicciones con ellos.  
  
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
  
 **Importante:** Todo lo que se incluye en la lista de expresiones o en la cláusula **Where** debe proviene del dominio de datos definido por la cláusula **from** . No puede mezclar dominios de datos.  
  
##  <a name="select-types"></a><a name="Select_Types"></a> SELECCIONAR tipos  
 La sintaxis de la instrucción **Select** admite muchas tareas diferentes. Use los patrones siguientes para realizar estas tareas:  
  
-   [Predecir](#Predicting)  
  
-   [Exploración](#Browsing)  
  
-   [asincrónica](#Copying)  
  
-   [Obtención de detalles](#Drillthrough)  
  
###  <a name="predicting"></a><a name="Predicting"></a> Predecir  
 Puede realizar predicciones basadas en un modelo de minería usando los siguientes tipos de consulta.  
  
 Puede incluir cualquiera de las instrucciones **Select** de exploración o de predicción en las cláusulas **from** y **Where** de una instrucción de **selección** de combinación de predicción.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|SELECCIONAR DESDE [NATURAL] COMBINACIÓN DE PREDICCIÓN|Devuelve una predicción que se crea combinando las columnas del modelo de minería de datos con las columnas de un origen de datos interno.<br /><br /> El dominio de este tipo de consulta lo forman las columnas de predicción del modelo y las columnas del origen de datos de entrada.<br /><br /> [Seleccione entre &#60;modelo&#62; combinación de predicción &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Consultas de predicción &#40;minería de datos&#41;](/analysis-services/data-mining/prediction-queries-data-mining)|  
|SELECCIONAR DE *\<model>*|Devuelve el estado más probable de la columna de predicción, basándose únicamente en el modelo de minería de datos. Este tipo de consulta es un método abreviado para crear una predicción con una combinación de predicción vacía.<br /><br /> El dominio de este tipo de consulta lo forman las columnas de predicción del modelo.<br /><br /> [SELECT FROM &#60;Model&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Consultas de predicción &#40;minería de datos&#41;](/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [Volver a Tipos SELECT](#Select_Types)  
  
###  <a name="browsing"></a><a name="Browsing"></a> Exploración  
 Puede examinar el contenido de un modelo de minería de datos usando los siguientes tipos de consulta.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|SELECCIONE DISTINCT FROM *\<model>*|Devuelve todos los valores de estado del modelo de minería de datos para la columna especificada.<br /><br /> El dominio de datos de este tipo de consulta es el modelo de minería de datos.<br /><br /> [Seleccione DISTINCt FROM &#60;Model &#62; &#40;DMX&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Consultas de contenido &#40;minería de datos&#41;](/analysis-services/data-mining/content-queries-data-mining)|  
|Seleccione desde *\<model>* . CONTENT|Devuelve contenido que describe el modelo de minería de datos.<br /><br /> El dominio de datos este tipo de consulta es el conjunto de filas de esquema CONTENT.<br /><br /> [Seleccione entre &#60;modelo&#62;. CONTENIDO &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Consultas de contenido &#40;minería de datos&#41;](/analysis-services/data-mining/content-queries-data-mining)|  
|Seleccione desde *\<model>* . DIMENSION_CONTENT|Devuelve contenido que describe el modelo de minería de datos.<br /><br /> El dominio de datos este tipo de consulta es el conjunto de filas de esquema CONTENT.<br /><br /> [Seleccione entre &#60;modelo&#62;. DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|Seleccione desde *\<model>* . PMML|Devuelve la representación PMML (Lenguaje de marcado de modelos de predicción) del modelo de minería de datos para los algoritmos que admiten esta funcionalidad.<br /><br /> El dominio de este tipo de consulta es el conjunto de filas de esquema PMML.<br /><br /> [Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML](/previous-versions/sql/sql-server-2012/ms126283(v=sql.110))|  
  
 [Volver a Tipos SELECT](#Select_Types)  
  
###  <a name="copying"></a><a name="Copying"></a> Instantánea  
 Puede copiar un modelo de minería de datos y su estructura de minería de datos asociada a un nuevo modelo y cambiar después el nombre del modelo dentro de la instrucción.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|SELECT INTO *\<new model>*|Crea una copia del modelo de minería de datos.<br /><br /> El dominio de este tipo de consulta es el modelo de minería de datos.<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [Volver a Tipos SELECT](#Select_Types)  
  
###  <a name="drillthrough"></a><a name="Drillthrough"></a> Detalles  
 Puede examinar los escenarios (o una representación de los escenarios) que se emplearon para entrenar el modelo usando los siguientes tipos de consulta.  
  
|Tipo de consulta|Descripción|  
|----------------|-----------------|  
|Seleccione desde *\<model>* . VECES|Devuelve los casos empleados para entrenar el modelo de minería de datos.<br /><br /> El dominio de este tipo de consulta es el modelo de minería de datos.<br /><br /> [Seleccione entre &#60;modelo&#62;. CASOS &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Crear consultas de obtención de detalles usando DMX](/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|Seleccione desde *\<model>* . SAMPLE_CASES|Devuelve un caso de ejemplo, representativo de los casos empleados para entrenar el modelo de minería de datos.<br /><br /> El dominio de este tipo de consulta es el modelo de minería de datos.<br /><br /> [Seleccione entre &#60;modelo&#62;. SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|Seleccione desde *\<structure>* . VECES|Devuelve las filas de datos detalladas de la estructura de minería de datos subyacente, aunque algunos detalles no se usaran al entrenar el modelo de minería de datos.<br /><br /> [Seleccione de &#60;estructura&#62;. VECES](../dmx/select-from-structure-cases.md)<br /><br /> [Consultas de obtención de detalles &#40;minería de datos&#41;](/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [Volver a Tipos SELECT](#Select_Types)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
