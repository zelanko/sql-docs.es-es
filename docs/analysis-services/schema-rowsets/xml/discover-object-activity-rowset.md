---
title: Conjunto de filas DISCOVER_OBJECT_ACTIVITY | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_OBJECT_ACTIVITY rowset
ms.assetid: 100f7de1-ad5c-4973-b863-3c10df1245c4
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 573b41cb848ee7a8e93bfdc4625b8a05857f2d61
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY, conjunto de filas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Proporciona el uso de recursos por objeto desde el inicio del servicio.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_OBJECT_ACTIVITY** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_AGGREGATION_HIT**|**DBTYPE_I8**||Número de veces que se ha alcanzado una agregación del objeto desde el inicio del servicio.|  
|**OBJECT_AGGREGATION_MISS**|**DBTYPE_I8**||Número de veces que no se ha perdido (es decir, no se ha utilizado) una agregación existente del objeto desde el inicio del servicio.|  
|**OBJECT_CPU_TIME_MS**|**DBTYPE_I8**||Tiempo de CPU, en milisegundos, consumido por el objeto desde el inicio del servicio.|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||Número de linaje de los datos del objeto; este número se incrementa cada vez que se procesa el objeto.|  
|**OBJECT_HIT**|**DBTYPE_I8**||Número de veces que se ha alcanzado el objeto en la memoria caché desde el inicio del servicio.|  
|**OBJECT_ID**|**DBTYPE_WSTR**||Id. del objeto tal y como se define en el momento de su creación.|  
|**OBJECT_MISS**|**DBTYPE_I8**||Número de veces que se ha perdido el objeto en la memoria caché desde el inicio del servicio.|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||Ruta de acceso al elemento primario del objeto actual.|  
|**OBJECT_READ_KB**|**DBTYPE_I8**||Valor acumulado de los datos leídos por el objeto desde el inicio del servicio, en kilobytes.|  
|**OBJECT_READS**|**DBTYPE_I8**||Número acumulado de operaciones de lectura realizadas por el objeto desde el inicio del servicio.|  
|**OBJECT_ROWS_RETURNED**|**DBTYPE_I8**||Número de filas devueltas por el objeto al autor de las llamadas desde el inicio del servicio.|  
|**OBJECT_ROWS_SCANNED**|**DBTYPE_I8**||Número de filas examinadas por el objeto desde el inicio del servicio.|  
|**OBJECT_VERSION**|**DBTYPE_I4**||Número de versión de metadatos del objeto; este número cambia cada vez que se modifica el objeto.|  
|**OBJECT_WRITE_KB**|**DBTYPE_I8**||Valor acumulado de los datos escritos por el objeto desde el inicio del servicio, en kilobytes.|  
|**OBJECT_WRITES**|**DBTYPE_I8**||Número acumulado de operaciones de escritura realizadas por el objeto desde el inicio del servicio.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_OBJECT_ACTIVTY** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|Opcional.|  
|OBJECT_ID|DBTYPE_WSTR|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
