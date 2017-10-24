---
title: Conjunto de filas DISCOVER_OBJECT_ACTIVITY | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_OBJECT_ACTIVITY rowset
ms.assetid: 100f7de1-ad5c-4973-b863-3c10df1245c4
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f42115f46be220580d42d54f5cab62c7c12492ec
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY, conjunto de filas
  Proporciona el uso de recursos por objeto desde el inicio del servicio.  
  
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
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

