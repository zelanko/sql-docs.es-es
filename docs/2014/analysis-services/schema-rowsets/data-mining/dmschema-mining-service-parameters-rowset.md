---
title: Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS | Documentos de Microsoft
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
- DMSCHEMA_MINING_SERVICE_PARAMETERS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_SERVICE_PARAMETERS rowset
ms.assetid: 5994e66b-84d0-4279-9f50-d92fd829dd83
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9079be52d50da3a400496dc602166c857f2b1691
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198539"
---
# <a name="dmschemaminingserviceparameters-rowset"></a>Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS
  Describe los parámetros para los algoritmos en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_SERVICE_PARAMETERS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||Nombre del algoritmo.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`||Nombre del parámetro.|  
|`PARAMETER_TYPE`|`DBTYPE_WSTR`||Tipo de parámetro.|  
|`IS_REQUIRED`|`DBTYPE_BOOL`||Valor booleano que devuelve `TRUE` si el parámetro es necesario.|  
|`PARAMETER_FLAGS`|`DBTYPE_UI4`||Máscara de bits que describe las características del parámetro:<br /><br /> -   `DM_PARAMETER_TRAINING` (`0x0000001`) indica que el parámetro se utiliza para el entrenamiento<br />-   `DM_PARAMETER_PREDICTION` (`0x00000002`) indica que el parámetro se utiliza para la predicción<br />-   `DM_PARAMETER_CONTENT` (`0x00000003`) indica que el parámetro se utiliza para la restricción de contenido.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción del parámetro fácil de comprender.|  
|`DEFAULT_VALUE`|`DBTYPE_WSTR`||Valor predeterminado del parámetro. Devuelve `NULL` si el valor predeterminado no es un tipo de datos simple.|  
|`VALUE_ENUMERATION`|`DBTYPE_WSTR`||Enumerador de los valores posibles para el parámetro.|  
|`HELP_FILE`|`DBTYPE_WSTR`||Nombre del archivo que contiene la documentación de este parámetro.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||Id. del contexto de Ayuda para esta función.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_SERVICE_PARAMETERS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  