---
title: Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_MODEL_CONTENT_PMML rowset
ms.assetid: fa05bb08-a955-4c8d-b57f-ffcd82470220
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 960abf852fb3cf548b5f00203521e8440b04cae2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML
  Devuelve la estructura XML del modelo de minería de datos. El formato de las cadenas XML sigue el estándar PMML 2.1 (Lenguaje de marcado de modelos de predicción).  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DMSCHEMA_MINING_MODEL_CONTENT_PMML** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo que se rellena con el nombre de la base de datos de la que el modelo es miembro.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**||Nombre del modelo. Esta columna no puede contener valores **NULL**.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**||Tipo del modelo. Es una cadena específica del proveedor. Puede ser **NULL**:|  
|**MODEL_GUID**|**DBTYPE_GUID**||GUID que identifica el modelo. Los proveedores que no utilizan GUID para identificar las tablas devuelven **NULL**.|  
|**MODEL_PMML**|**DBTYPE_WSTR**||Representación XML del contenido del modelo en formato PMML.|  
|**TAMAÑO**|**DBTYPE_UI4**||Número de bytes de la secuencia de XML.|  
|**UBICACIÓN**|**DBTYPE_WSTR**||Ubicación del archivo XML. Es **NULL** si no hay ninguna ubicación disponible.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DMSCHEMA_MINING_MODEL_CONTENT_PMML** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_TYPE**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
