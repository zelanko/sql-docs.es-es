---
title: Sys.dm_exec_distributed_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_DISTRIBUTED_REQUESTS
- DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
- SYS.DM_EXEC_DISTRIBUTED_REQUESTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase,views
- sys.dm_exec_distributed_sql_requests management view
- PolyBase
- dm_exec_distributed_sql_requests management view
ms.assetid: c041d416-d8c6-435e-a563-6a310abd33e3
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7d61b26c1af6a588140cdf47308ee8f69ecd42b2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37982547"
---
# <a name="sysdmexecdistributedrequests-transact-sql"></a>Sys.dm_exec_distributed_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene información sobre todas las solicitudes activas actualmente o recientemente en las consultas de PolyBase. Muestra una fila por cada solicitud o consulta.  
  
 Basado en sesión y solicitar el identificador, un usuario, a continuación, puede recuperar las solicitudes de distribuida reales generadas para ejecutarse: a través de sys.dm_exec_distributed_requests. Por ejemplo, una consulta que implican SQL regular y las tablas externas de SQL se se descompone en diversas instrucciones/solicitudes ejecutadas a través de los diversos nodos de proceso. Para realizar un seguimiento de los pasos distribuidos en todos los nodos de proceso, presentamos un identificador de ejecución 'global' que se puede usar para realizar un seguimiento de todas las operaciones en los nodos de proceso asociados a una solicitud determinada y el operador, respectivamente.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|sql_handle|**varbinary (64)**|Clave para esta vista. Identificador numérico único asociado a la solicitud.|Es único en todas las solicitudes en el sistema.|  
|execution_id|**nvarchar (32**|Identificador numérico único asociado con la sesión en el que se ejecutó esta consulta.||  
|status|**nvarchar (32**|Estado actual de la solicitud.|'Pendiente', 'Autorizar', 'AcquireSystemResources', 'Initializing', 'Planear', 'Análisis', 'AquireResources', 'Ejecutando', 'Cancelar', 'Completa', 'Error', 'Cancelar'.|  
|error_id|**nvarchar(36)**|Identificador único del error asociado a la solicitud, si existe.|Se establece en NULL si se ha producido ningún error.|  
|start_time|**datetime**|Hora a la que se inició la ejecución de la solicitud.|0 para las solicitudes en cola; datetime válido de lo contrario, menor o igual que la hora actual.|  
|end_time|**datetime**|Hora en que completó el motor de compilación de la solicitud.|NULL para las solicitudes en cola o activas; en caso contrario, un valor datetime válido menor o igual que la hora actual.|  
|total_elapsed_time|**int**|Tiempo transcurrido en ejecución desde que se inició la solicitud, en milisegundos.|Entre 0 y la diferencia entre start_time y end_time. Si total_elapsed_time supera el valor máximo de un entero, continuará total_elapsed_time sea el valor máximo. Esta condición generará la advertencia "se superó el valor máximo." El valor máximo en milisegundos equivale a 24,8 días.|  
  
## <a name="see-also"></a>Vea también  
 [Solución de problemas con las vistas de administración dinámica de PolyBase](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
