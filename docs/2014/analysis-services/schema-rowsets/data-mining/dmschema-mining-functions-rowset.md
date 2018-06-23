---
title: Conjunto de filas DMSCHEMA_MINING_FUNCTIONS | Documentos de Microsoft
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5a60e18a57c15976e7a7bd5d5e31729e255869a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201245"
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de filas DMSCHEMA_MINING_FUNCTIONS
  Describe las funciones de minería de datos que son compatibles con los algoritmos de minería de datos disponibles en un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_FUNCTIONS` filas contiene las columnas siguientes.  
  
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
 El `DMSCHEMA_MINING_FUNCTIONS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  