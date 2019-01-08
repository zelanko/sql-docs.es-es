---
title: Sys.dm_xe_session_event_actions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xe_session_event_actions_TSQL
- sys.dm_xe_session_event_actions_TSQL
- dm_xe_session_event_actions
- sys.dm_xe_session_event_actions
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_xe_session_event_actions dynamic management view
ms.assetid: 0c22a546-683e-4c84-ab97-1e9e95304b03
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6725ebaf9aa90e8ab3ae768ad30199a3a8b9b2aa
ms.sourcegitcommit: f46fd79fd32a894c8174a5cb246d9d34db75e5df
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/26/2018
ms.locfileid: "53785836"
---
# <a name="sysdmxesessioneventactions-transact-sql"></a>sys.dm_xe_session_event_actions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre las acciones de la sesión de eventos. Se ejecutan las acciones cuando se activan los eventos. Esta vista de administración agrega estadísticas del número de veces que se ha ejecutado una acción y el tiempo de ejecución total de la acción.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|La dirección de memoria de la sesión de eventos. No admite valores NULL.|  
|action_name|**nvarchar(256)**|El nombre de la acción. No admite valores NULL.|  
|action_package_guid|**uniqueidentifier**|El GUID del paquete que contiene la acción. No admite valores NULL.|  
|event_name|**nvarchar(256)**|Nombre del evento al que se enlaza la acción. No admite valores NULL.|  
|event_package_guid|**uniqueidentifier**|El GUID del paquete que contiene el evento. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|sys.dm_xe_session_event_actions.event_session_address|sys.dm_xe_sessions.address|Varios a uno|  
|Sys.dm_xe_session_event_actions.action_name,<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_session_events.event_package_guid|Varios a uno|  
|Sys.dm_xe_session_event_actions.event_name,<br /><br /> sys.dm_xe_session_event_actions.event_package_guid|sys.dm_xe_objects.name,<br /><br /> sys.dm_xe_objects.package_guid|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

