---
title: Conjunto de filas DISCOVER_JOBS | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edf0125dff1f193106f5738aef99b8c830c29236
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS, conjunto de filas
  Proporciona información sobre los trabajos activos que se ejecutan en el servidor. Un trabajo forma una parte de un comando que ejecuta una tarea concreta en nombre del comando.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_JOBS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**JOB_CREATION_TIME**|**DBTYPE_DBTIMESTAMP**||Fecha y hora UTC del servidor cuando que se creó el trabajo.|  
|**JOB_DESCRIPTION**|**DBTYPE_WSTR**||Descripción del trabajo asignada por el servicio de servidor.|  
|**JOB_EXECUTION_TIME_MS**|**DBTYPE_I8**||Tiempo, en milisegundos, que el trabajo está activo.|  
|**JOB_ID**|**DBTYPE_I4**||Identificador único del trabajo.|  
|**JOB_START_TIME**|**DBTYPE_DBTIMESTAMP**||Fecha y hora UTC del servidor cuando se inició el trabajo.|  
|**JOB_THREADPOOL_ID**|**DBTYPE_I4**||Grupo de subprocesos a partir del que se inició el trabajo actual.|  
|**JOB_TOTAL_TIME_MS**|**DBTYPE_I8**||Tiempo, en milisegundos, desde que se inició el trabajo.|  
|**SPID**|**DBTYPE_I4**||Identificador de la sesión.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_JOBS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Opcional.|  
|JOB_ID|DBTYPE_I4|Opcional.|  
|JOB_DESCRIPTION|DBTYPE_WSTR|Opcional.|  
|JOB_THREADPOOL_ID|DBTYPE_I4|Opcional.|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
