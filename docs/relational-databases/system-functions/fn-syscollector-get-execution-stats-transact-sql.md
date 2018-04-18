---
title: fn_syscollector_get_execution_stats (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_stats
- fn_syscollector_get_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_stats function
ms.assetid: 793ad72c-a992-4a8d-8584-bcb6b3b476f1
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c2621c2a723d0bb693b0672134fa02d75f48cea
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="fnsyscollectorgetexecutionstats-transact-sql"></a>fn_syscollector_get_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve estadísticas detalladas del paquete o conjunto de recopilación, incluido el número de filas de error registradas por una tarea Flujo de datos del paquete. Una tarea de flujo de datos es un componente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que procesa los datos. Estos datos están en formato relacional, de modo que tienen un conjunto de datos de entrada y otro de salida compuestos por filas.  
  
 Las estadísticas se calculan a partir de las entradas en la vista syscollector_execution_stats.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_syscollector_get_execution_stats ( log_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *log_id*  
 Identificador único local para el registro de ejecución. *log_id* es **int**.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|avg_row_count_in|**int**|Promedio del número de filas que entraron en las tareas Flujo de datos del paquete.<br /><br /> Nota: Una tarea de flujo de datos es un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] componente que procesa los datos. Estos datos están en formato relacional, de modo que tienen un conjunto de datos de entrada formado por filas. Este es el número de filas que entraron en la tarea. Una vez transformados los datos, la salida es un conjunto de resultados formado por filas. La tarea de flujo de datos transforma los datos y genera un conjunto de resultados que está compuesto por filas. Esta salida es el número de filas que salieron de la tarea.|  
|min_row_count_in|**int**|Mínimo número de filas que entraron en las tareas Flujo de datos del paquete.|  
|max_row_count_in|**int**|Máximo número de filas que entraron en las tareas Flujo de datos del paquete.|  
|avg_row_count_out|**int**|Promedio del número de filas que salieron de las tareas Flujo de datos del paquete.|  
|min_row_count_out|**int**|Mínimo número de filas que salieron de las tareas Flujo de datos del paquete.|  
|max_row_count_out|**int**|Máximo número de filas que salieron de las tareas Flujo de datos del paquete.|  
|avg_duration|**int**|Tiempo promedio, en milisegundos, empleado en el componente de flujo de datos del paquete.|  
|min_duration|**int**|Tiempo mínimo, en milisegundos, empleado en el componente de flujo de datos del paquete.|  
|max_duration|**int**|Tiempo máximo, en milisegundos, empleado en el componente de flujo de datos del paquete.|  
  
## <a name="permissions"></a>Permissions  
 Requiere SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Vea también  
 [syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
