---
title: Sys. server_event_session_targets (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_targets_TSQL
- sys.server_event_session_targets_TSQL
- sys.server_event_session_targets
- server_event_session_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_targets catalog view
- xe
ms.assetid: dda4879d-57ae-4267-b410-1ef5c37404c7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 707060599513e765e702755251015899eb6732d7
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82821806"
---
# <a name="sysserver_event_session_targets-transact-sql"></a>sys.server_event_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada destino de evento de una sesión de eventos.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|target_id|**int**|Id. del destino. El Id. es único dentro del objeto de sesión de evento. No admite valores NULL.|  
|name|**sysname**|Nombre del destino del evento. No admite valores NULL.|  
|Paquete|**sysname**|Nombre del paquete de eventos que contiene el destino de evento. No admite valores NULL.|  
|module|**sysname**|Nombre del módulo que contiene el destino de evento. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="remarks"></a>Observaciones  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
||||  
|-|-|-|  
|De|En|Relación|  
|sys.server_event_session_targets.event_session_id|Sys. server_event_sessions. event_session_id|Varios a uno|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
