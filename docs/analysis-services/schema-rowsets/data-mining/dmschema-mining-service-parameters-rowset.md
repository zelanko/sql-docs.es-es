---
title: Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
apiname: DMSCHEMA_MINING_SERVICE_PARAMETERS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c84d263a312318be40c65c37a168bf11fdc97cfc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
  
  
