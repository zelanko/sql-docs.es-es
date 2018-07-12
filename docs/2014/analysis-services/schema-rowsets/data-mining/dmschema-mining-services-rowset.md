---
title: Conjunto de filas DMSCHEMA_MINING_SERVICES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_SERVICES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICES rowset
ms.assetid: 4a672f2f-d637-4def-a572-c18556f83d34
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6ccfdba24d7bc23b97eb15e61321f82e5ab1d9b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278255"
---
# <a name="dmschemaminingservices-rowset"></a>Conjunto de filas DMSCHEMA_MINING_SERVICES
  Proporciona una descripción de cada algoritmo de minería de datos admitido por el proveedor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_SERVICES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||Nombre del algoritmo. Esta columna es específica del proveedor.|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||Esta columna contiene un mapa de bits que describe el servicio de minería de datos. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] rellena esta columna con uno de los valores siguientes:<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (`1`)<br />-   `DM_SERVICETYPE_CLUSTERING` (`2`)|  
|`SERVICE_DISPLAY_NAME`|`DBTYPE_WSTR`||Nombre para mostrar localizable para el algoritmo.|  
|`SERVICE_GUID`|`DBTYPE_GUID`||GUID para el algoritmo.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción del algoritmo fácil de comprender.|  
|`PREDICTION_LIMIT`|`DBTYPE_UI4`||Número máximo de predicciones que pueden proporcionar el modelo y el algoritmo.|  
|`SUPPORTED_DISTRIBUTION_FLAGS`|`DBTYPE_WSTR`||Lista delimitada por comas de las marcas que describen las distribuciones estadísticas admitidas por el algoritmo. Esta columna contiene uno o más de los siguientes valores:<br /><br /> -   "`NORMAL`"<br />-   "`LOG NORMAL`"<br />-   "`UNIFORM`"|  
|`SUPPORTED_INPUT_CONTENT_TYPES`|`DBTYPE_WSTR`||Lista delimitada por comas de las marcas que describen los tipos de contenido de entrada admitidos por el algoritmo. Esta columna contiene uno o más de los siguientes valores:<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-"CLAVE `SEQUENCE`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-   "`KEY TIME`"|  
|`SUPPORTED_PREDICTION_CONTENT_TYPES`|`DBTYPE_WSTR`||Lista delimitada por comas de las marcas que describen los tipos de contenido de predicción admitidos por el algoritmo. Esta columna contiene uno o más de los siguientes valores:<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-   "`DISCRETIZED`"<br />-   "`ORDERED`"<br />-"CLAVE `SEQUENCE` "<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY VARIANCE`"<br />-   "`PROBABILITY STDEV`"<br />-"KEY TIME"|  
|`SUPPORTED_MODELING_FLAGS`|`DBTYPE_WSTR`||Lista delimitada por comas de las marcas de modelado admitidas por el algoritmo. Esta columna contiene uno o más de los siguientes valores:<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> También se pueden definir marcas específicas del proveedor.|  
|`SUPPORTED_SOURCE_QUERY`|`DBTYPE_WSTR`||: Esta columna se admite por compatibilidad con versiones anteriores.|  
|`TRAINING_COMPLEXITY`|`DBTYPE_I4`||Duración esperada del entrenamiento:<br /><br /> -   `DM_TRAINING_COMPLEXITY_LOW` indica que el tiempo de ejecución es relativamente corto y es proporcional a la entrada.<br />-   **DM_TRAINING_COMPLEXITY_MEDIUM** indica que el tiempo de ejecución puede ser largo, pero suele ser proporcional a la entrada.<br />-   **DM_TRAINING_COMPLEXITY_HIGH** indica que el tiempo de ejecución es largo y puede aumentar exponencialmente en relación al número de casos de entrenamiento.|  
|`PREDICTION_COMPLEXITY`|`DBTYPE_I4`||Duración esperada de la predicción:<br /><br /> -   **DM_PREDICTION_COMPLEXITY_LOW** indica que el tiempo de ejecución es relativamente corto y es proporcional a la entrada.<br />-   **DM_PREDICTION_COMPLEXITY_MEDIUM** indica que el tiempo de ejecución puede ser largo, pero suele ser proporcional a la entrada.<br />-   **DM_PREDICTION_COMPLEXITY_HIGH** indica que el tiempo de ejecución es largo y puede aumentar exponencialmente en relación al número de casos de entrenamiento.|  
|`EXPECTED_QUALITY`|`DBTYPE_I4`||Calidad esperada del modelo generado con este algoritmo:<br /><br /> -   `DM_EXPECTED_QUALITY_LOW`<br />-   `DM_EXPECTED_QUALITY_MEDIUM`<br />-   **DM_EXPECTED_QUALITY_HIGH**|  
|`SCALING`|`DBTYPE_I4`||Escalabilidad del algoritmo:<br /><br /> -   **DM_SCALING_LOW**<br />-   `DM_SCALING_MEDIUM`<br />-   **DM_SCALING_HIGH**|  
|`ALLOW_INCREMENTAL_INSERT`|`DBTYPE_BOOL`||Valor booleano que indica si el algoritmo admite el entrenamiento incremental, es decir, actualizar los patrones detectados en función de nuevos datos objetivos, en lugar de volver a detectar los patrones totalmente.|  
|`ALLOW_PMML_INITIALIZATION`|`DBTYPE_BOOL`||Valor booleano que indica si se pueden crear modelos de minería de datos en función de una cadena de PMML 2.1.<br /><br /> Si su valor es `TRUE`, el algoritmo de minería de datos admite la inicialización a partir de contenido de PMML 2.1.|  
|`CONTROL`|`DBTYPE_I4`||Compatibilidad proporcionada por el servicio si se interrumpe el entrenamiento:<br /><br /> -   `DM_CONTROL_NONE` indica que el algoritmo no se puede cancelar después de iniciarse entrenar el modelo.<br />-   `DM_CONTROL_CANCEL` indica que el algoritmo puede cancelarse una vez que se inicia entrenar el modelo, pero debe reiniciarse para reanudar el entrenamiento.<br />-   `DM_CONTROL_SUSPENDRESUME` indica que el algoritmo puede cancelarse y reanudarse en cualquier momento, pero los resultados no están disponibles hasta que se complete la formación.<br />-   `DM_CONTROL_SUSPENDWITHRESULT` indica que el algoritmo puede cancelarse y reanudarse en cualquier momento, y pueden obtenerse resultados incrementales.|  
|`ALLOW_DUPLICATE_KEY`|`DBTYPE_BOOL`||Valor booleano que indica si los casos pueden contener claves duplicadas.<br /><br /> Si su valor es `VARIANT_TRUE`, se permite que los casos contengan claves duplicadas.|  
|`VIEWER_TYPE`|`DBTYPE_WSTR`||Visor recomendado para este modelo.|  
|`HELP_FILE`|`DBTYPE_WSTR`||(Opcional) Nombre del archivo que contiene la documentación de este servicio.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||(Opcional) Id. del contexto de Ayuda para este servicio.|  
|`MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL`|`DBTYPE_WSTR`||Versión admitida del DDL. 0 indica que no se admite DDL.|  
|`MSOLAP_SUPPORTS_OLAP_MINING_MODELS`|`DBTYPE_BOOL`||Valor booleano que indica si se pueden crear modelos de minería de datos OLAP.<br /><br /> Si su valor es `TRUE`, pueden crearse modelos de minería de datos OLAP. Requiere que `MSOLAP_SUPPORTS_ANALYSIS_SERVICES_DDL` sea distinto de cero.|  
|`MSOLAP_SUPPORTS_DATA_MINING_DIMENSIONS`|`DBTYPE_BOOL`||Valor booleano que indica si se pueden crear dimensiones de minería de datos.<br /><br /> Si su valor es `TRUE`, pueden crearse dimensiones de minería de datos.|  
|`MSOLAP_SUPPORTS_DRILLTHROUGH`|`DBTYPE_BOOL`||Valor booleano que indica si el servicio admite las funciones de obtención de detalles.<br /><br /> Si su valor es `TRUE`, el servicio admite las funciones de obtención de detalles.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_SERVICES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
