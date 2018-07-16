---
title: Conjunto de filas DISCOVER_JOBS | Microsoft Docs
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
helpviewer_keywords:
- DISCOVER_JOBS rowset
ms.assetid: b4d83bb6-aed3-4513-b516-cefadf95dad2
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a23a3e3dae0a03bf31a7b73b8cb505e834cff27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246065"
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS, conjunto de filas
  Proporciona información sobre los trabajos activos que se ejecutan en el servidor. Un trabajo forma una parte de un comando que ejecuta una tarea concreta en nombre del comando.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_JOBS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`JOB_CREATION_TIME`|`DBTYPE_DBTIMESTAMP`||Fecha y hora UTC del servidor cuando que se creó el trabajo.|  
|`JOB_DESCRIPTION`|`DBTYPE_WSTR`||Descripción del trabajo asignada por el servicio de servidor.|  
|`JOB_EXECUTION_TIME_MS`|`DBTYPE_I8`||Tiempo, en milisegundos, que el trabajo está activo.|  
|`JOB_ID`|`DBTYPE_I4`||Identificador único del trabajo.|  
|`JOB_START_TIME`|`DBTYPE_DBTIMESTAMP`||Fecha y hora UTC del servidor cuando se inició el trabajo.|  
|`JOB_THREADPOOL_ID`|`DBTYPE_I4`||Grupo de subprocesos a partir del que se inició el trabajo actual.|  
|`JOB_TOTAL_TIME_MS`|`DBTYPE_I8`||Tiempo, en milisegundos, desde que se inició el trabajo.|  
|`SPID`|`DBTYPE_I4`||Identificador de la sesión.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_JOBS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|SPID|DBTYPE_I4|Opcional.|  
|JOB_ID|DBTYPE_I4|Opcional.|  
|JOB_DESCRIPTION|DBTYPE_WSTR|Opcional.|  
|JOB_THREADPOOL_ID|DBTYPE_I4|Opcional.|  
|JOB_MIN TOTAL_TIME_MS|DBTYPE_I8|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
