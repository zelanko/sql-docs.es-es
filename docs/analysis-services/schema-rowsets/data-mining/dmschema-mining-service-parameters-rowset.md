---
title: Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_SERVICE_PARAMETERS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e867952dac5e49b5f563ba7a9aed29eef3564d1a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingserviceparameters-rowset"></a>Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS
  Describe los parámetros para los algoritmos en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DMSCHEMA_MINING_SERVICE_PARAMETERS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Nombre del algoritmo.|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|Nombre del parámetro.|  
|**TIPO_PARÁMETRO**|**DBTYPE_WSTR**|Tipo de parámetro.|  
|**IS_REQUIRED**|**DBTYPE_BOOL**|Valor booleano que devuelve **TRUE** si el parámetro es necesario.|  
|**PARAMETER_FLAGS**|**DBTYPE_UI4**|Máscara de bits que describe las características del parámetro:<br /><br /> **DM_PARAMETER_TRAINING** (**0x0000001**) indica que el parámetro se utiliza para el entrenamiento.<br /><br /> **DM_PARAMETER_PREDICTION** (**0x00000002**) indica que el parámetro se utiliza para la predicción.<br /><br /> **DM_PARAMETER_CONTENT** (**0x00000003**) indica que el parámetro se utiliza para la restricción de contenido.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Descripción del parámetro fácil de comprender.|  
|**VALOR PREDETERMINADO**|**DBTYPE_WSTR**|Valor predeterminado del parámetro. Devuelve **NULL** si el valor predeterminado no es un tipo de datos simple.|  
|**VALUE_ENUMERATION**|**DBTYPE_WSTR**|Enumerador de los valores posibles para el parámetro.|  
|**HELP_FILE**|**DBTYPE_WSTR**|Nombre del archivo que contiene la documentación de este parámetro.|  
|**HELP_CONTEXT**|**DBTYPE_I4**|Id. del contexto de Ayuda para esta función.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DMSCHEMA_MINING_SERVICE_PARAMETERS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**PARAMETER_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
