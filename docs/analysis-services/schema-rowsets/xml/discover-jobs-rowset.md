---
title: Conjunto de filas DISCOVER_JOBS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9d0d836d8fe44041aa541d71d86be327647dab9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036326"
---
# <a name="discoverjobs-rowset"></a>DISCOVER_JOBS, conjunto de filas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
