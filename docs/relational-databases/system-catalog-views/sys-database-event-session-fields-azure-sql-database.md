---
description: sys.database_event_session_fields (Azure SQL Database)
title: sys.database_event_session_fields (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 729e24203a471cf3bdea3a18ee510cf2cced9987
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97458537"
---
# <a name="sysdatabase_event_session_fields-azure-sql-database"></a>sys.database_event_session_fields (Azure SQL Database)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Devuelve una fila para cada columna personalizable que se estableció explícitamente en los eventos y destinos.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y a las versiones posteriores.|  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|Identificador de la sesión de eventos. No admite valores NULL.|  
|object_id|**int**|Id. del objeto al que está asociado este campo. No admite valores NULL.|  
|name|**sysname**|Nombre del campo. No admite valores NULL.|  
|value|**sql_variant**|Valor del campo. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 Esta vista tiene las siguientes cardinalidades de relación.  
  
| From | En | Relación |
| ---- | -- | ------------ |
|Sys.database_event_session_actions sys.database_event_session_actions.event_session_id|Sys.database_event_sessions sys.database_event_sessions.event_session_id|Varios a uno|  
|Sys.database_event_session_actions sys.database_event_session_actions.event_id<br /><br /> Sys.database_event_session_actions sys.database_event_session_actions.object_id<br /><br /> Sys.database_event_session_actions sys.database_event_session_actions.event_session_id|Sys.database_event_session_events sys.database_event_session_events.event_session_id<br /><br /> Sys.database_event_session_events sys.database_event_session_events.event_id|Varios a uno|  
|Sys.database_event_session_actions sys.database_event_session_actions.event_session_id<br /><br /> Sys.database_event_session_actions sys.database_event_session_actions.object_id|Sys.database_event_session_targets sys.database_event_session_targets.event_session_id<br /><br /> Sys.database_event_session_targets sys.database_event_session_targets.target_id|Varios a uno|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
