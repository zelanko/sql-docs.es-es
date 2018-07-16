---
title: Conjunto de filas DMSCHEMA_MINING_STRUCTURES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DMSCHEMA_MINING_STRUCTURES
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURES rowset
ms.assetid: 6224556b-08a0-496e-bd7c-632c3e833e26
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab600b39e4a8347e470153cf21510554605d1c71
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323075"
---
# <a name="dmschemaminingstructures-rowset"></a>Conjunto de filas DMSCHEMA_MINING_STRUCTURES
  Enumera información sobre las estructuras de minería de datos del catálogo actual.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_STRUCTURES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar. Si el proveedor no admite los esquemas, el valor es `NULL`.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||Nombre de la estructura. Esta columna no puede contener valores `NULL`.|  
|`STRUCTURE_GUID`|`DBTYPE_GUID`||GUID que identifica la estructura de forma única. Si el proveedor no lo admite, su valor es `NULL`.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción concisa de la estructura. Si no hay ninguna descripción asociada a la estructura, su valor es `NULL`.|  
|`STRUCTURE_PROPID`|`DBTYPE_UI4`||Identificador de propiedad de la estructura. Si el proveedor no lo admite, su valor es `NULL`.|  
|`DATE_CREATED`|`DBTYPE_DBTIMESTAMP`||Fecha en la que se creó la estructura. Si no está disponible por parte del proveedor, su valor es `NULL`.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||Fecha en la que se modificó la estructura por última vez. Si no está disponible por parte del proveedor, su valor es `NULL`.|  
|`CREATION_STATEMENT`|`DBTYPE_WSTR`||(Opcional) Instrucción que se utilizó para crear el modelo de minería de datos original.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||Valor booleano que indica si se ha rellenado la estructura.<br /><br /> `VARIANT_TRUE` si la estructura se ha rellenado; de lo contrario, `VARIANT_FALSE`.|  
|`LAST_PROCESSED`|`DBTYPE_DBTIMESTAMP`||Fecha en la que se procesó la estructura por última vez. Si no está disponible por parte del proveedor, su valor es `NULL`.|  
|`HOLDOUT_MAXPERCENT`|`DBTYPE_ UI1`||Valor especificado por el usuario que indica el porcentaje máximo de casos de entrada que se pueden considerar como el conjunto de prueba.<br /><br /> 0 o `NULL` indica que no existe límite.|  
|`HOLDOUT_MAXCASES`|`DBTYPE_UI8`||Valor especificado por el usuario que indica el número máximo de casos de entrada que se pueden considerar como el conjunto de prueba.<br /><br /> 0 o `NULL` indica que no existe límite.|  
|`HOLDOUT_SEED`|`DBTYPE_UI8`||Valor especificado por el usuario que se utiliza como inicialización del particionamiento reiterativo.<br /><br /> 0 indica que se utiliza como valor de inicialización un hash del id. de la estructura de minería de datos.|  
|`HOLDOUT_ACTUAL_SIZE`|`DBTYPE_UI8`||Si se procesa la estructura de minería de datos, indica el tamaño real del conjunto de datos de prueba, expresado en número de casos.<br /><br /> `NULL` indica que no se procesa la estructura de minería de datos.|  
  
 El conjunto de filas se ordena en `STRUCTURE_CATALOG`, `STRUCTURE_SCHEMA`, `STRUCTURE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_STRUCTURES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
