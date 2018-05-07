---
title: Sys.dm_tcp_listener_states (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tcp_listener_states
- dm_tcp_listener_states
- sys.dm_tcp_listener_states_TSQL
- dm_tcp_listener_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Availability Groups [SQL Server], listeners
- sys.dm_tcp_listener_states dynamic management view
ms.assetid: 9997ffed-a4c1-428f-8bac-3b9e4b16d7cf
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b8c2c2ea711d2c7950fb4b1e2f67da2ab23b29b5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmtcplistenerstates-transact-sql"></a>sys.dm_tcp_listener_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila que contiene la información de estado dinámico para cada agente de escucha TCP.  
  
> [!NOTE]
> El agente de escucha del grupo de disponibilidad podría escuchar en el mismo puerto que el agente de escucha de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este caso, los agentes de escucha se enumeran por separado, como en el caso de un agente de escucha de Service Broker.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**listener_id**|**int**|Identificador interno del agente de escucha. No admite valores NULL.<br /><br /> Clave principal.|  
|**ip_address**|**nvarchar48**|La dirección IP del agente de escucha que está en línea y que está siendo objeto de escucha actualmente. Se permite IPv4 e IPv6. Si un agente de escucha posee ambos tipos de direcciones, se enumeran por separado. Un carácter comodín IPv4, se muestra como “0.0.0.0”. Un carácter comodín IPv6, se muestra como “::”.<br /><br /> No admite valores NULL.|  
|**is_ipv4**|**bit**|Tipo de dirección IP<br /><br /> 1 = IPv4<br /><br /> 0 = IPv6|  
|**port**|**int**|Número de puerto en el que escucha el agente de escucha. No admite valores NULL.|  
|**Tipo**|**tinyint**|Tipo de agente de escucha, uno de los siguientes:<br /><br /> 0 = [!INCLUDE[tsql](../../includes/tsql-md.md)]<br /><br /> 1 = Service Broker<br /><br /> 2 = Creación de reflejo de base de datos<br /><br /> No admite valores NULL.|  
|**type_desc**|**nvarchar (20)**|Descripción de la **tipo**, uno de:<br /><br /> TSQL<br /><br /> SERVICE_BROKER<br /><br /> DATABASE_MIRRORING<br /><br /> No admite valores NULL.|  
|**state**|**tinyint**|Estado del agente de escucha del grupo de disponibilidad, uno de los siguientes:<br /><br /> 1 = En línea. El agente de escucha está escuchando y procesando solicitudes.<br /><br /> 2 = Pendiente de reiniciarse. El agente de escucha está sin conexión, pendiente de un reinicio.<br /><br /> Si el agente de escucha del grupo de disponibilidad está escuchando en el mismo puerto que la instancia de servidor, estos dos agentes de escucha tienen siempre el mismo estado.<br /><br /> No admite valores NULL.<br /><br /> Nota: Los valores de esta columna proceden del objeto TSD_listener. La columna no es compatible con un estado sin conexión porque cuando el TDS_listener está sin conexión, no se puede consultar para estado.|  
|**state_desc**|**nvarchar(16)**|Descripción de **estado**, uno de:<br /><br /> ONLINE<br /><br /> PENDING_RESTART<br /><br /> No admite valores NULL.|  
|**start_time**|**datetime**|Marca de tiempo que indica cuándo se inició el agente de escucha. No admite valores NULL.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Consultar el catálogo de sistema SQL Server preguntas más frecuentes](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [Vistas de catálogo de grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Funciones y vistas de administración dinámica de los grupos de disponibilidad AlwaysOn &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)  
  
  
