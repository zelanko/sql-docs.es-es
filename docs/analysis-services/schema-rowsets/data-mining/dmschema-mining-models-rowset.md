---
title: Conjunto de filas DMSCHEMA_MINING_MODELS | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODELS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODELS rowset
ms.assetid: 1636f4cf-b342-4e2e-93b4-04136e2d41ef
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f857cf206932ad8048768c2c65f047670ec9d1e4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingmodels-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODELS
  Enumera los modelos de minería de datos del catálogo actual. El **DMSCHEMA_MINING_MODELS** conjunto de filas incluye información como nombres de modelo y fecha de procesamiento, el algoritmo de minería de datos asociados a cada modelo de minería de datos.  
  
 . El **DMSCHEMA_MINING_MODELS** de filas de esquema es muy similar a la [DBSCHEMA_TABLES](../../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md) de filas de esquema y se puede usar la misma manera.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DMSCHEMA_MINING_MODELS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Nombre del catálogo. Se rellena con el nombre de la base de datos de la que es miembro el modelo.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|El nombre del modelo de minería de datos. Esta columna contiene el nombre del modelo de minería de datos y nunca está vacía.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Tipo del modelo.|  
|**MODEL_GUID**|**DBTYPE_GUID**|GUID del modelo.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Descripción del modelo fácil de comprender.|  
|**MODEL_PROPID**|**DBTYPE_UI4**|Id. de propiedad del modelo. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**|Fecha en la que se creó el modelo.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**|Fecha en la que se modificó por última vez la definición del modelo.|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|Enumeración que identifica el tipo de algoritmo de minería de datos que utiliza el modelo. Este tipo puede tener uno de los siguientes valores:<br /><br /> **DM_SERVICETYPE_CLASSIFICATION** (1)<br /><br /> **DM_SERVICETYPE_SEGMENTATION**(2)<br /><br /> **ASOCIACIÓN DE DM_SERVICETYPE_**(4)<br /><br /> **DM_SERVICETYPE_ DENSITY_ESTIMATE**(8)<br /><br /> **DM_SERVICETYPE_SEQUENCE**(16)|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Nombre específico del proveedor para el algoritmo de minería de datos que utiliza el modelo.|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**|Instrucción que se utilizó para crear el modelo de minería de datos.|  
|**PREDICTION_ENTITY**|**DBTYPE_WSTR**|Lista delimitada por comas que indica las columnas de minería de datos que se pueden predecir.|  
|**IS_POPULATED**|**DBTYPE_BOOL**|Marca booleana que indica si el modelo se ha rellenado.<br /><br /> **TRUE** si el modelo se ha rellenado; en caso contrario, **FALSE**.|  
|**MINING_PARAMETERS**|**DBTYPE_WSTR**|Lista separada por comas de los parámetros que se usaron cuando se creó el modelo.|  
|**MINING_STRUCTURE**|**DBTYPE_WSTR**|Id. de la estructura de minería de datos en la que se basa el modelo.|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**|Fecha en la que se procesó el modelo por última vez.|  
|**MSOLAP_IS_DRILLTHROUGH_ENABLED**|**DBTYPE_BOOL**|Marca booleana que indica si el modelo admite la obtención de detalles.|  
|**FILTRO**|**DBTYPE_WSTR**|Expresión de filtro asociada al modelo de minería de datos.<br /><br /> Una cadena NULL o vacía indica que no se aplica ningún filtro.|  
|**TRAINING_SET_SIZE**|**DBTYPE_UIS**|El número de casos que se encuentran en el entrenamiento del modelo de minería de datos establece después de que se ha procesado la estructura y una vez aplicados los filtros para el modelo.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **DMSCHEMA_MINING_MODELS** se puede restringir el conjunto de filas en las columnas de la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Opcional.|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SERVICE_TYPE_ID**|**DBTYPE_UI4**|Opcional.|  
|**MINING_STRUCTURE**|**DBTYPE_WSTR**|Opcional.|  
  
 Para obtener ejemplos de cómo consultar este conjunto de filas, vea [consultar los parámetros que se usan para crear un modelo de minería de datos](../../../analysis-services/data-mining/query-the-parameters-used-to-create-a-mining-model.md).  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  

