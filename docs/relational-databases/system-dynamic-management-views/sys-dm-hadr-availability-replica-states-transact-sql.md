---
title: sys.dm_hadr_availability_replica_states (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_hadr_availability_replica_states
- sys.dm_hadr_availability_replica_states_TSQL
- sys.dm_hadr_availability_replica_states
- dm_hadr_availability_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_availability_replica_states dynamic management view
ms.assetid: d2e678bb-51e8-4a61-b223-5c0b8d08b8b1
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9adddf8b74848948bfdd45fdf93813ed7489d40a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmhadravailabilityreplicastates-transact-sql"></a>sys.dm_hadr_availability_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada réplica local y una fila para cada réplica remota en el mismo grupo de disponibilidad AlwaysOn que una réplica local. Cada fila contiene información sobre el estado de una réplica dada.  
  
> [!IMPORTANT]  
>  Para obtener información acerca de todas las réplicas de un grupo de disponibilidad determinado, consulte **sys.dm_hadr_availability_replica_states** en la instancia del servidor que hospeda la réplica principal. Cuando se consulta en una instancia de servidor que hospeda una réplica secundaria de un grupo de disponibilidad, esta vista de administración dinámica devuelve solo información local para el grupo de disponibilidad.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador único de la réplica.|  
|**group_id**|**uniqueidentifier**|Identificador único del grupo de disponibilidad.|  
|**is_local**|**bit**|Si la réplica es local, uno de:<br /><br /> 0 = Indica una réplica secundaria remota en un grupo de disponibilidad cuya réplica principal está hospedada en la instancia del servidor local. Este valor solo se produce en la ubicación de la réplica principal.<br /><br /> 1 = indica una réplica local. En las réplicas secundarias, es el único valor disponible para el grupo de disponibilidad al que pertenece la réplica.|  
|**rol**|**tinyint**|Actual [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] rol de una réplica local o una réplica remota conectada, uno de:<br /><br /> 0 = Resolver<br /><br /> 1 = Principal<br /><br /> 2 = Secundario<br /><br /> Para obtener más información sobre los roles de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)], vea [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).|  
|**role_desc**|**nvarchar(60)**|Descripción de **rol**, uno de:<br /><br /> RESOLVING<br /><br /> PRIMARY<br /><br /> SECONDARY|  
|**operational_state**|**tinyint**|Estado operativo actual de la réplica, uno de:<br /><br /> 0 = pendiente de conmutación por error<br /><br /> 1 = pendiente<br /><br /> 2 = en línea<br /><br /> 3 = sin conexión<br /><br /> 4 = Error<br /><br /> 5 = No se pudo establecer quórum<br /><br /> NULL = La réplica no es local.<br /><br /> Para obtener más información, consulte [Roles y estados operativos](#RolesAndOperationalStates), más adelante en este tema.|  
|**operational\_state\_desc**|**nvarchar(60)**|Descripción de **operativa\_estado**, uno de:<br /><br /> PENDING_FAILOVER<br /><br /> PENDING<br /><br /> ONLINE<br /><br /> OFFLINE<br /><br /> FAILED<br /><br /> FAILED_NO_QUORUM<br /><br /> NULL|  
|**recovery\_health**|**tinyint**|Paquete acumulativo de actualizaciones de la **base de datos\_estado** columna de la [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) vista de administración dinámica. Éstos son los valores posibles y sus descripciones.<br /><br /> 0: en curso.  Al menos una base de datos combinada y tiene un estado de la base de datos que no sea en línea (**base de datos\_estado** es no 0).<br /><br /> 1: en línea. Todas las bases de datos combinadas tienen un estado de la base de datos de en línea (**database_state** es 0).<br /><br /> NULL : **is_local** = 0|  
|**recovery_health_desc**|**nvarchar(60)**|Descripción de **recovery_health**, uno de:<br /><br /> ONLINE_IN_PROGRESS<br /><br /> ONLINE<br /><br /> NULL|  
|**synchronization\_health**|**tinyint**|Refleja un resumen del estado de sincronización de base de datos (**synchronization_state**) de todos los unido las bases de datos de disponibilidad (también conocido como *réplicas*) y el modo de disponibilidad de la réplica ( modo confirmación sincrónica o asincrónica). La acumulación reflejará el estado acumulado menos correcto las bases de datos en la réplica. A continuación se muestran los valores posibles y sus descripciones.<br /><br /> 0: no funciona correctamente.   El estado de al menos una de las bases de datos unidas es NOT SYNCHRONIZING.<br /><br /> 1: parcialmente correcto. Algunas réplicas no están en el estado de sincronización del destino: las réplicas de confirmación sincrónica deben ser sincronizadas y las réplicas de confirmación asincrónica deberían estar sincronizándose.<br /><br /> 2: correcto. Todas las réplicas están en el estado de sincronización del destino: las réplicas de confirmación sincrónica se sincronizan y las réplicas de confirmación asincrónica se están sincronizando.|  
|**synchronization_health_desc**|**nvarchar(60)**|Descripción de **synchronization_health**, uno de:<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**connected_state**|**tinyint**|Si una réplica secundaria está actualmente conectado a la réplica principal. Los valores posibles se muestran a continuación con sus descripciones.<br /><br /> 0: desconectado. La respuesta de una réplica de disponibilidad al estado desconectado depende de su función: en la réplica principal, si una réplica secundaria está desconectada, sus bases de datos secundarias se marcan como NOT SYNCHRONIZED en la réplica principal, que espera a que la base de datos secundaria a volver a conectar; En una réplica secundaria, cuando detecta que está desconectada, la réplica secundaria intenta volver a conectarse a la réplica principal.<br /><br /> 1: conectado.<br /><br /> Cada réplica principal realiza un seguimiento del estado de conexión de cada réplica secundaria en el mismo grupo de disponibilidad. Las réplicas secundarias realizan un seguimiento del estado de solo la réplica principal.|  
|**connected_state_desc**|**nvarchar(60)**|Descripción de **connection_state**, uno de:<br /><br /> DISCONNECTED<br /><br /> CONNECTED|  
|**last_connect_error_number**|**int**|Número del último error de conexión.|  
|**last_connect_error_description**|**nvarchar(1024)**|Texto de la **last_connect_error_number** mensaje.|  
|**last_connect_error_timestamp**|**datetime**|Marca de tiempo de fecha y hora que indica cuándo el **last_connect_error_number** se produjo el error.|  
  
##  <a name="RolesAndOperationalStates"></a>Roles y estados operativos  
 El rol, **rol**, refleja el estado de una réplica de disponibilidad determinado y el estado operativo, **operational_state**, describe si la réplica está preparada para procesar las solicitudes de cliente para todos los base de datos de la réplica de disponibilidad. El siguiente es un resumen de los Estados operativos que son posibles para cada rol: RESOLVING, principal y secundario.  
  
 **RESOLUCIÓN:** cuando una réplica de disponibilidad está en el rol RESOLVING, los Estados operativos posibles son como se muestra en la tabla siguiente.  
  
|Estado operativo|Description|  
|-----------------------|-----------------|  
|PENDING_FAILOVER|Se procesa un comando de conmutación por error para el grupo de disponibilidad.|  
|OFFLINE|Todos los datos de configuración para la réplica de disponibilidad se han actualizado en el clúster de WSFC y, además, en los metadatos locales, pero el grupo de disponibilidad no tiene actualmente una réplica principal.|  
|FAILED|Se ha producido un error de lectura al intentar recuperar información del clúster de WSFC.|  
|FAILED_NO_QUORUM|El nodo WSFC local no tiene quórum. Es un estado deducido.|  
  
 **PRINCIPAL:** cuando una réplica de disponibilidad está realizando el rol principal, es actualmente la réplica principal. Los posibles estados operativos son como se muestra en la tabla siguiente.  
  
|Estado operativo|Description|  
|-----------------------|-----------------|  
|PENDING|Es un estado transitorio, pero una réplica principal se puede bloquear en este estado si los subprocesos de trabajo no están disponibles para procesar las solicitudes.|  
|ONLINE|El recurso de grupo de disponibilidad está en línea, y todos los subprocesos de trabajo de la base de datos se han seleccionado.|  
|FAILED|La réplica de disponibilidad no puede leer ni escribir en el clúster de WSFC.|  
  
 **Base de datos secundaria:** cuando una réplica de disponibilidad está realizando el rol secundario, es actualmente una réplica secundaria. Los Estados operativos posibles son como se muestra en la tabla siguiente.  
  
|Estado operativo|Description|  
|-----------------------|-----------------|  
|ONLINE|La réplica secundaria local no está conectada a la réplica principal.|  
|FAILED|La réplica secundaria local no puede leer ni escribir en el clúster de WSFC.|  
|NULL|En una réplica principal, se devuelve este valor cuando la fila está relacionada con una réplica secundaria.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
