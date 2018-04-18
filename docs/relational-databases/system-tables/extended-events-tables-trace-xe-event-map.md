---
title: trace_xe_event_map (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trace_xe_event_map_TSQL
- trace_xe_event_map
dev_langs:
- TSQL
helpviewer_keywords:
- trace_xe_event_map
- extended events [SQL Server], tables
ms.assetid: 537aa292-3540-47e8-be28-56dc01abc343
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fde0e497d6dbc79431309c296664e0e3db639561
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="extended-events-tables---tracexeeventmap"></a>Extended tablas de eventos - trace_xe_event_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada evento de eventos extendidos que está asignado a una clase de eventos de Seguimiento de SQL. Esta tabla se almacena en la base de datos maestra, en el esquema sys.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|trace_event_id|**smallint**|Identificador de la clase de eventos de Seguimiento de SQL que está asignando.|  
|package_name|**nvarchar(60)**|El nombre del paquete de eventos extendidos donde reside el evento asignado.|  
|xe_event_name|**nvarchar(60)**|El nombre del evento de eventos extendidos que está asignado a la clase de eventos de Seguimiento de SQL.|  
  
## <a name="remarks"></a>Comentarios  
 Puede utilizar la siguiente consulta para identificar las acciones de eventos de eventos extendidos que son equivalentes a las clases de eventos de Seguimiento de SQL:  
  
```  
SELECT te.name, xe.package_name, xe.xe_event_name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NOT NULL  
```  
  
 No todas las clases de eventos tienen eventos de eventos extendidos equivalentes. Puede utilizar la siguiente consulta para enumerar las clases de eventos que no tienen un equivalente de eventos extendidos:  
  
```  
SELECT te.trace_event_id, te.name  
FROM sys.trace_events AS te  
LEFT JOIN sys.trace_xe_event_map AS xe  
   ON te.trace_event_id = xe.trace_event_id  
WHERE xe.trace_event_id IS NULL  
```  
  
 En la consulta anterior, la mayoría de las clases de eventos devueltas están relacionadas con la auditoría. Recomendamos que use la Auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para auditar. Auditoría de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa eventos extendidos para facilitar la creación de auditorías. Para obtener más información, vea [SQL Server Audit &#40;motor de base de datos&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
## <a name="see-also"></a>Vea también  
 [trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)  
  
  
