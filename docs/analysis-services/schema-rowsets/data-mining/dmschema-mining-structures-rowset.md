---
title: Conjunto de filas DMSCHEMA_MINING_STRUCTURES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5a40c44722108d8377eb98d050f3af528c23c0e5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingstructures-rowset"></a>Conjunto de filas DMSCHEMA_MINING_STRUCTURES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Enumera información sobre las estructuras de minería de datos del catálogo actual.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DMSCHEMA_MINING_STRUCTURES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema sin certificar. Si el proveedor no admite los esquemas, el valor es**NULL** .|  
|**NOMBRE_ESTRUCTURA**|**DBTYPE_WSTR**||Nombre de la estructura. Esta columna no puede contener valores **NULL**.|  
|**STRUCTURE_GUID**|**DBTYPE_GUID**||GUID que identifica la estructura de forma única. Si el proveedor no lo admite, su valor es**NULL** .|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción concisa de la estructura. Si no hay ninguna descripción asociada a la estructura, su valor es**NULL** .|  
|**STRUCTURE_PROPID**|**DBTYPE_UI4**||Identificador de propiedad de la estructura. Si el proveedor no lo admite, su valor es**NULL** .|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||Fecha en la que se creó la estructura. Si no está disponible por parte del proveedor, su valor es**NULL** .|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Fecha en la que se modificó la estructura por última vez. Si no está disponible por parte del proveedor, su valor es**NULL** .|  
|**CREATION_STATEMENT**|**DBTYPE_WSTR**||(Opcional) Instrucción que se utilizó para crear el modelo de minería de datos original.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||Valor booleano que indica si se ha rellenado la estructura.<br /><br /> **VARIANT_TRUE** si la estructura se ha rellenado; de lo contrario, **VARIANT_FALSE** .|  
|**LAST_PROCESSED**|**DBTYPE_DBTIMESTAMP**||Fecha en la que se procesó la estructura por última vez. Si no está disponible por parte del proveedor, su valor es**NULL** .|  
|**HOLDOUT_MAXPERCENT**|**DBTYPE_ UI1**||Valor especificado por el usuario que indica el porcentaje máximo de casos de entrada que se pueden considerar como el conjunto de prueba.<br /><br /> 0 o **NULL** indica que no existe límite.|  
|**HOLDOUT_MAXCASES**|**DBTYPE_UI8**||Valor especificado por el usuario que indica el número máximo de casos de entrada que se pueden considerar como el conjunto de prueba.<br /><br /> 0 o **NULL** indica que no existe límite.|  
|**HOLDOUT_SEED**|**DBTYPE_UI8**||Valor especificado por el usuario que se utiliza como inicialización del particionamiento reiterativo.<br /><br /> 0 indica que se utiliza como valor de inicialización un hash del id. de la estructura de minería de datos.|  
|**HOLDOUT_ACTUAL_SIZE**|**DBTYPE_UI8**||Si se procesa la estructura de minería de datos, indica el tamaño real del conjunto de datos de prueba, expresado en número de casos.<br /><br /> **NULL** indica que no se procesa la estructura de minería de datos.|  
  
 El conjunto de filas se ordena en **STRUCTURE_CATALOG**, **STRUCTURE_SCHEMA**, **STRUCTURE_NAME**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DMSCHEMA_MINING_STRUCTURES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**NOMBRE_ESTRUCTURA**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
