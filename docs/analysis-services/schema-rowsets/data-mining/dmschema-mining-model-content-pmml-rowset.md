---
title: Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_MODEL_CONTENT_PMML
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_MODEL_CONTENT_PMML rowset
ms.assetid: fa05bb08-a955-4c8d-b57f-ffcd82470220
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 771ce7da7719b186dffef3ae0f3095a215c71e48
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingmodelcontentpmml-rowset"></a>Conjunto de filas DMSCHEMA_MINING_MODEL_CONTENT_PMML
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Devuelve la estructura XML del modelo de minería de datos. El formato de las cadenas XML sigue el estándar PMML 2.1 (Lenguaje de marcado de modelos de predicción).  
  
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
  
  
