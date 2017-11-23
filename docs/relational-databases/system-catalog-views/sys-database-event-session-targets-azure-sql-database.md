---
title: Sys.database_event_session_targets (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: 
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: Azure SQL Database
ms.assetid: 38d775ee-1fe1-4820-88c6-02b2f875a66b
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0e06bf788cb8d5b2b66a1470fff431015d2df0ec
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysdatabaseeventsessiontargets-azure-sql-database"></a>Sys.database_event_session_targets (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada destino de evento de una sesión de eventos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y las versiones posteriores.|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|target_id|**int**|Id. del destino. El Id. es único dentro del objeto de sesión de evento. No admite valores NULL.|  
|name|**sysname**|Nombre del destino del evento. No admite valores NULL.|  
|paquete|**sysname**|Nombre del paquete de eventos que contiene el destino de evento. No admite valores NULL.|  
|Módulo|**sysname**|Nombre del módulo que contiene el destino de evento. No admite valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
||||  
|-|-|-|  
|De|En|Relación|  
|Sys.database_event_session_targets.event_session_id|Sys.database_event_sessions.event_session_id|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
