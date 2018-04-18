---
title: Sys.database_event_session_actions (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
ms.assetid: 32494df1-7ab7-4b88-a858-6b1021d67433
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 72d1fd572adc64912c064bef9504b1126ccc72ff
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdatabaseeventsessionactions-azure-sql-database"></a>Sys.database_event_session_actions (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada acción en cada evento de una sesión de eventos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y las versiones posteriores.|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|event_id|**int**|Id. del evento. Este Id. es único dentro del objeto de sesión de eventos. No admite valores NULL.|  
|name|**sysname**|El nombre de la acción. Acepta valores NULL.|  
|paquete|**sysname**|Nombre del paquete de eventos que contiene el evento. Acepta valores NULL.|  
|Módulo|**sysname**|Nombre del módulo que contiene el evento. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
||||  
|-|-|-|  
|De|En|Relación|  
|sys.database_event_session_actions.event_session_id|sys.sys.database_event_sessions.event_session_id|Varios a uno|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|Varios a uno|  
  
  
