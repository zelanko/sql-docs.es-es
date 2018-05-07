---
title: Conjunto de filas DMSCHEMA_MINING_FUNCTIONS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f92a3028f9397283f8d5820c54d823e40b8fdc3d
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de filas DMSCHEMA_MINING_FUNCTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe las funciones de minería de datos admitidas por los algoritmos de minería de datos disponibles en un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
  
