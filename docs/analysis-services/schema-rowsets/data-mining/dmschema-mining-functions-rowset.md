---
title: Conjunto de filas DMSCHEMA_MINING_FUNCTIONS | Documentos de Microsoft
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
- DMSCHEMA_MINING_FUNCTIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d7e0224cb46a481150fe97f0e247f3cd8f8aa11e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de filas DMSCHEMA_MINING_FUNCTIONS
  Describe las funciones de minería de datos que son compatibles con los algoritmos de minería de datos disponibles en un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DMSCHEMA_MINING_FUNCTIONS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**||Nombre del algoritmo.|  
|**NOMBRE_FUNCIÓN**|**DBTYPE_WSTR**||Nombre de la función.|  
|**SIGNATURA_DE_FUNCIÓN**|**DBTYPE_WSTR**||Firma de la función.|  
|**RETURNS_TABLE**|**DBTYPE_BOOL**||**FALSE** si la función devuelve contenido escalar (como la longitud del argumento de carácter); **TRUE** si la función devuelve una tabla (como una tabla de histograma).|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción de la función fácil de comprender.|  
|**HELP_FILE**|**DBTYPE_WSTR**||Nombre del archivo que contiene la documentación de esta función.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||Id. del contexto de Ayuda para esta función.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DMSCHEMA_MINING_FUNCTIONS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NOMBRE_FUNCIÓN**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
