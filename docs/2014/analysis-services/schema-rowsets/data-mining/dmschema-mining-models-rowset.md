---
title: Conjunto de filas DMSCHEMA_MINING_MODELS | Documentos de Microsoft
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
- DMSCHEMA_MINING_MODELS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODELS rowset
ms.assetid: 1636f4cf-b342-4e2e-93b4-04136e2d41ef
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d8296ddb800b7691936236aa0cdb6550c89c34c2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197030"
---
# <a name="dmschemaminingmodels-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODELS
  Enumera los modelos de minería de datos del catálogo actual. El conjunto de filas `DMSCHEMA_MINING_MODELS` incluye información como los nombres de modelo, la fecha de procesamiento y el algoritmo de minería de datos asociados a cada modelo de minería de datos.  
  
 . El `DMSCHEMA_MINING_MODELS` de filas de esquema es muy similar a la [DBSCHEMA_TABLES](../ole-db/dbschema-tables-rowset.md) de filas de esquema y se puede usar la misma manera.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_MODELS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo. Se rellena con el nombre de la base de datos de la que es miembro el modelo.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene `NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||El nombre del modelo de minería de datos. Esta columna contiene el nombre del modelo de minería de datos y nunca está vacía.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||Tipo del modelo.|  
|`MODEL_GUID`|`DBTYPE_GUID`||GUID del modelo.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción del modelo fácil de comprender.|  
|`MODEL_PROPID`|`DBTYPE_UI4`||Id. de propiedad del modelo. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||Fecha en la que se creó el modelo.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||Fecha en la que se modificó por última vez la definición del modelo.|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`||Enumeración que identifica el tipo de algoritmo de minería de datos que utiliza el modelo. Este tipo puede tener uno de los siguientes valores:<br /><br /> -   `DM_SERVICETYPE_CLASSIFICATION` (1)<br />-   `DM_SERVICETYPE_SEGMENTATION`(2)<br />-   `DM_SERVICETYPE_ ASSOCIATION`(4)<br />-   `DM_SERVICETYPE_ DENSITY_ESTIMATE`(8)<br />-   `DM_SERVICETYPE_SEQUENCE`(16)|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||Nombre específico del proveedor para el algoritmo de minería de datos que utiliza el modelo.|  
|`CREATION_STATEMENT`|`DBTYPE_WSTR`||Instrucción que se utilizó para crear el modelo de minería de datos.|  
|`PREDICTION_ENTITY`|`DBTYPE_WSTR`||Lista delimitada por comas que indica las columnas de minería de datos que se pueden predecir.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||Marca booleana que indica si el modelo se ha rellenado.<br /><br /> `TRUE` si el modelo se ha rellenado; de lo contrario, `FALSE`.|  
|`MINING_PARAMETERS`|`DBTYPE_WSTR`||Lista separada por comas de los parámetros que se usaron cuando se creó el modelo.|  
|`MINING_STRUCTURE`|`DBTYPE_WSTR`||Id. de la estructura de minería de datos en la que se basa el modelo.|  
|`LAST_PROCESSED`|`DBTYPE_DBTIMESTAMP`||Fecha en la que se procesó el modelo por última vez.|  
|`MSOLAP_IS_DRILLTHROUGH_ENABLED`|`DBTYPE_BOOL`||Marca booleana que indica si el modelo admite la obtención de detalles.|  
|`FILTER`|`DBTYPE_WSTR`||Expresión de filtro asociada al modelo de minería de datos.<br /><br /> Una cadena NULL o vacía indica que no se aplica ningún filtro.|  
|`TRAINING_SET_SIZE`|`DBTYPE_UIS`||El número de casos que se encuentran en el entrenamiento del modelo de minería de datos establece después de que se ha procesado la estructura y una vez aplicados los filtros para el modelo.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_MODELS` se puede restringir el conjunto de filas en las columnas de la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|Opcional.|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SERVICE_TYPE_ID`|`DBTYPE_UI4`|Opcional.|  
|`MINING_STRUCTURE`|`DBTYPE_WSTR`|Opcional.|  
  
 Para obtener ejemplos de cómo consultar este conjunto de filas, vea [consultar los parámetros que se usan para crear un modelo de minería de datos](../../data-mining/query-the-parameters-used-to-create-a-mining-model.md).  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  