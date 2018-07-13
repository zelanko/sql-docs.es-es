---
title: Conjunto de filas DMSCHEMA_MINING_FUNCTIONS | Microsoft Docs
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
- DMSCHEMA_MINING_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b726c81df5a6085ee52b177d95b4917d7cb8be1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169655"
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de filas DMSCHEMA_MINING_FUNCTIONS
  Describe las funciones de minería de datos que son compatibles con los algoritmos de minería de datos disponibles en un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_FUNCTIONS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||Nombre del algoritmo.|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`||Nombre de la función.|  
|`FUNCTION_SIGNATURE`|`DBTYPE_WSTR`||Firma de la función.|  
|`RETURNS_TABLE`|`DBTYPE_BOOL`||`FALSE` si la función devuelve contenido escalar (como la longitud del argumento de carácter); `TRUE` si la función devuelve una tabla (como una tabla de histograma).|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción de la función fácil de comprender.|  
|`HELP_FILE`|`DBTYPE_WSTR`||Nombre del archivo que contiene la documentación de esta función.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||Id. del contexto de Ayuda para esta función.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_FUNCTIONS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  
