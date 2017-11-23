---
title: MSmerge_articlehistory (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSmerge_articlehistory
- MSmerge_articlehistory_TSQL
dev_langs: TSQL
helpviewer_keywords: MSmerge_articlehistory system table
ms.assetid: 2870e7ea-dbec-4636-9171-c2cee96018ac
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dbd2fef95a478eebc6526fc888fa621c1ec198ab
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="msmergearticlehistory-transact-sql"></a>MSmerge_articlehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSmerge_articlehistory** controla los cambios realizados en los artículos durante una sesión de sincronización del agente de mezcla, con una fila por cada artículo en el que se realizaron cambios de tabla. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|El identificador de una sesión de trabajo del agente de mezcla en el [MSmerge_sessions](../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) tabla del sistema.|  
|**phase_id**|**int**|Fase de la sesión de sincronización, que puede ser una de las siguientes:<br /><br /> **1** = cargar.<br /><br /> **2** = descarga.<br /><br /> **4** = limpiar.<br /><br /> **5** = apagado.<br /><br /> **6** = cambios del esquema.<br /><br /> **7** = BCP.|  
|**article_name**|**sysname**|Nombre del artículo en el que se realizaron cambios.|  
|**start_time**|**datetime**|Hora a la que el agente empezó a procesar el artículo.|  
|**duration**|**int**|Tiempo, en segundos, que el agente tardó en procesar un artículo.|  
|**Inserta**|**int**|Número de inserciones aplicadas a un artículo específico durante la sincronización. Este valor aumenta durante el proceso de sincronización y el valor final representa el número total.|  
|**actualizaciones**|**int**|Número de actualizaciones aplicadas a un artículo específico durante la sincronización. Este valor aumenta durante el proceso de sincronización y el valor final representa el número total.|  
|**eliminaciones**|**int**|Número de eliminaciones aplicadas a un artículo específico durante la sincronización. Este valor aumenta durante el proceso de sincronización y el valor final representa el número total.|  
|**conflictos**|**int**|Número de conflictos que se han producido durante la sincronización. Este valor aumenta durante el proceso de sincronización y el valor final representa el número total.|  
|**conflicts_resolved**|**int**|Número de conflictos que se han producido durante la sincronización y se han resuelto. Este valor aumenta durante el proceso de sincronización y el valor final representa el número total.|  
|**rows_retried**|**int**|Número de filas con errores que se han reintentado durante la sincronización. Este valor aumenta durante el proceso de sincronización y el valor final representa el número total.|  
|**percent_complete**|**decimal**|Porcentaje del tiempo total de sincronización que el Agente de mezcla ha invertido en el artículo durante una sesión. Este valor es NULL hasta que finaliza la sesión.|  
|**estimated_changes**|**int**|Estimación del número de cambios de fila que deben aplicarse al artículo.|  
|**relative_cost**|**decimal**|Tiempo empleado en aplicar los cambios para este artículo respecto al tiempo total de la sesión completa.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
