---
title: Sys.database_event_session_actions (Azure SQL Database) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
ms.assetid: 32494df1-7ab7-4b88-a858-6b1021d67433
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a5f0a70cdf6f242b36c6cf9888d2bf9d0fc37d61
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39549955"
---
# <a name="sysdatabaseeventsessionactions-azure-sql-database"></a>sys.database_event_session_actions (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada acción en cada evento de una sesión de eventos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y cualquier versión posterior.|  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|event_id|**int**|Id. del evento. Este Id. es único dentro del objeto de sesión de eventos. No admite valores NULL.|  
|NAME|**sysname**|El nombre de la acción. Acepta valores NULL.|  
|paquete|**sysname**|Nombre del paquete de eventos que contiene el evento. Acepta valores NULL.|  
|módulo|**sysname**|Nombre del módulo que contiene el evento. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  
  
## <a name="remarks"></a>Notas  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
||||  
|-|-|-|  
|De|En|Relación|  
|sys.database_event_session_actions.event_session_id|sys.sys.database_event_sessions.event_session_id|Varios a uno|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|Varios a uno|  
  
  
