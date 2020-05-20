---
title: sys.dm_xe_database_session_event_actions
titleSuffix: Azure SQL Database
ms.custom: seo-lt-2019
ms.date: 06/10/2016
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 48519fd9-c7c2-434b-848d-ccbf41133fdd
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a8b072fe9b2d81782941f88eb739c5dcbadc13c8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82818818"
---
# <a name="sysdm_xe_database_session_event_actions-azure-sql-database"></a>sys.dm_xe_database_session_event_actions (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre las acciones de la sesión de eventos. Se ejecutan las acciones cuando se activan los eventos. Esta vista de administración agrega estadísticas del número de veces que se ha ejecutado una acción y el tiempo de ejecución total de la acción.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y a las versiones futuras.|  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8**|La dirección de memoria de la sesión de eventos. No admite valores NULL.|  
|action_name|**nvarchar(60)**|Nombre de la acción. No admite valores NULL.|  
|action_package_guid|**uniqueidentifier**|El GUID del paquete que contiene la acción. No admite valores NULL.|  
|event_name|**nvarchar(60)**|Nombre del evento al que se enlaza la acción. No admite valores NULL.|  
|event_package_guid|**uniqueidentifier**|GUID del paquete que contiene el evento. No admite valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|Sys. dm_xe_database_session_event_actions. event_session_address|Sys. dm_xe_database_sessions. Address|Varios a uno|  
|Sys. dm_xe_database_session_event_actions. action_name<br /><br /> sys.dm_xe_session_event_actions.action_package_guid|sys.dm_xe_objects.name<br /><br /> Sys. dm_xe_database_session_events. event_package_guid|Varios a uno|  
|Sys. dm_xe_database_session_event_actions. event_name<br /><br /> Sys. dm_xe_database_session_event_actions. event_package_guid|sys.dm_xe_objects.name<br /><br /> sys.dm_xe_objects.package_guid|Varios a uno|  
  
## <a name="see-also"></a>Consulte también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
