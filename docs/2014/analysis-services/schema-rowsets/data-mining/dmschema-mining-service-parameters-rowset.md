---
title: Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7203b2f717ec7605fcc52c1387472779488ae4c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224475"
---
# <a name="dmschemaminingserviceparameters-rowset"></a>Conjunto de filas DMSCHEMA_MINING_SERVICE_PARAMETERS
  Describe los parámetros para los algoritmos en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_SERVICE_PARAMETERS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||Nombre del algoritmo.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`||Nombre del parámetro.|  
|`PARAMETER_TYPE`|`DBTYPE_WSTR`||Tipo de parámetro.|  
|`IS_REQUIRED`|`DBTYPE_BOOL`||Valor booleano que devuelve `TRUE` si el parámetro es necesario.|  
|`PARAMETER_FLAGS`|`DBTYPE_UI4`||Máscara de bits que describe las características del parámetro:<br /><br /> -   `DM_PARAMETER_TRAINING` (`0x0000001`) indica que el parámetro se usa para el entrenamiento<br />-   `DM_PARAMETER_PREDICTION` (`0x00000002`) indica que el parámetro se usa para la predicción<br />-   `DM_PARAMETER_CONTENT` (`0x00000003`) indica el parámetro se utiliza para la restricción de contenido|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción del parámetro fácil de comprender.|  
|`DEFAULT_VALUE`|`DBTYPE_WSTR`||Valor predeterminado del parámetro. Devuelve `NULL` si el valor predeterminado no es un tipo de datos simple.|  
|`VALUE_ENUMERATION`|`DBTYPE_WSTR`||Enumerador de los valores posibles para el parámetro.|  
|`HELP_FILE`|`DBTYPE_WSTR`||Nombre del archivo que contiene la documentación de este parámetro.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||Id. del contexto de Ayuda para esta función.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_SERVICE_PARAMETERS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`PARAMETER_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
