---
title: Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML | Documentos de Microsoft
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
- DMSCHEMA_MINING_MODEL_CONTENT_PMML
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML rowset
ms.assetid: fa05bb08-a955-4c8d-b57f-ffcd82470220
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3c90e4dd752726b59e68ad6fb03c9d29327006e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103636"
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML
  Devuelve la estructura XML del modelo de minería de datos. El formato de las cadenas XML sigue el estándar PMML 2.1 (Lenguaje de marcado de modelos de predicción).  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_MODEL_CONTENT_PMML` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo que se rellena con el nombre de la base de datos de la que el modelo es miembro.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene `NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||Nombre del modelo. Esta columna no puede contener valores `NULL`.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`||Tipo del modelo. Es una cadena específica del proveedor. Puede ser `NULL`:|  
|`MODEL_GUID`|`DBTYPE_GUID`||GUID que identifica el modelo. Los proveedores que no utilizan GUID para identificar las tablas devuelven `NULL`.|  
|`MODEL_PMML`|`DBTYPE_WSTR`||Representación XML del contenido del modelo en formato PMML.|  
|`SIZE`|`DBTYPE_UI4`||Número de bytes de la secuencia de XML.|  
|`LOCATION`|`DBTYPE_WSTR`||Ubicación del archivo XML. Es `NULL` si no hay ninguna ubicación disponible.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_MODEL_CONTENT_PMML` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_TYPE`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  