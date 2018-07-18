---
title: Sys.database_event_session_fields (Azure SQL Database) | Microsoft Docs
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
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0a7c7ee610ae5eb3a56a46c5b8c7ba1645b64532
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981857"
---
# <a name="sysdatabaseeventsessionfields-azure-sql-database"></a>Sys.database_event_session_fields (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada columna personalizable que se estableció explícitamente en los eventos y destinos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y cualquier versión posterior.|  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|object_id|**int**|Id. del objeto al que está asociado este campo. No admite valores NULL.|  
|NAME|**sysname**|Nombre del campo. No admite valores NULL.|  
|value|**sql_variant**|Valor del campo. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  
  
## <a name="remarks"></a>Notas  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
||||  
|-|-|-|  
|De|En|Relación|  
|sys.database_event_session_actions.event_session_id|sys.database_event_sessions.event_session_id|Varios a uno|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.object_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|Varios a uno|  
|sys.database_event_session_actions.event_session_id<br /><br /> sys.database_event_session_actions.object_id|sys.database_event_session_targets.event_session_id<br /><br /> sys.database_event_session_targets.target_id|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
