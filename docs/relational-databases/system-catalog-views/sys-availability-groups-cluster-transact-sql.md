---
title: Sys.availability_groups_cluster (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.availability_groups_cluster
- availability_groups_cluster
- availability_groups_cluster_TSQL
- sys.availability_groups_cluster_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups_cluster catalog view
- Availability Groups [SQL Server], WSFC clusters
ms.assetid: d0f4683f-cdf0-4227-8b68-720ffe58f158
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e552a4deb02e676905eefc470f220c6d54cdc5f2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysavailabilitygroupscluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada grupo de disponibilidad AlwaysOn en el Windows Server conmutación por error de agrupación en clústeres (WSFC). Cada fila contiene los metadatos del grupo de disponibilidad del clúster de WSFC.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador único (GUID) del grupo de disponibilidad.|  
|**Nombre**|**sysname**|Nombre del grupo de disponibilidad. Es un nombre definido por el usuario que debe ser único dentro del clúster de conmutación por error de Windows Server (WSFC).|  
|**resource_id**|**nvarchar(40)**|Id. del recurso del clúster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|Id. del grupo de recursos del clúster WSFC del grupo de disponibilidad.|  
|**failure_condition_level**|**int**|Nivel de condición de error definido por el usuario bajo el cual debe activarse una conmutación por error automática; puede tener uno de los valores enteros siguientes:<br /><br /> 1: Especifica que se debe iniciar una conmutación por error automática cuando se produce alguna de las siguientes acciones: <br />-El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio no está funcionando.<br />-La concesión del grupo de disponibilidad para conectarse al clúster de conmutación por error WSFC expira porque no se ha recibido ninguna confirmación de la instancia del servidor. Para obtener más información, vea [Cómo funciona: tiempo de espera de concesión de AlwaysOn de SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> 2: Especifica que se debe iniciar una conmutación por error automática cuando se produce alguna de las siguientes acciones:  <br />-La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se conecta al clúster y el especificado por el usuario **health_check_timeout** se superó el umbral del grupo de disponibilidad. <br />-La réplica de disponibilidad está en estado de error. <br />3: Especifica que se debe iniciar una conmutación por error automática en caso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errores internos, como bloqueos por subproceso huérfanos, infracciones graves de acceso de escritura o volcado excesivo. Es el valor predeterminado. <br />4: Especifica que se debe iniciar una conmutación por error automática en moderados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] errores internos, como una condición de falta de memoria persistente en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grupo de recursos internos.<br />5: Especifica que se debe iniciar una conmutación por error automática en condiciones de error aptas, incluidas:<br />-Agotamiento de subprocesos de trabajo del motor de SQL. <br />-La detección de un interbloqueo irresoluble.<br /><br /> Los niveles de condición de error (1-5) abarcan desde el nivel menos restrictivo (1) al más restrictivo (5). Un nivel de condición dado abarca todos los niveles menos restrictivos. Así pues, el nivel de condición más estricto (el nivel 5) incluye los cuatro niveles de condición menos restrictivos (1-4), el nivel 4 incluye los niveles 1-3, y así sucesivamente.<br /><br /> Para cambiar este valor, utilice la opción FAILURE_CONDITION_LEVEL de la [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**health_check_timeout**|**int**|Tiempo de espera (en milisegundos) para la [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema procedimiento almacenado para devolver información de estado del servidor, antes de que la instancia del servidor se supone que es lento o se ha bloqueado. El valor predeterminado es 30000 milisegundos (30 segundos).<br /><br /> Para cambiar este valor, utilice la opción HEALTH_CHECK_TIMEOUT de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**automated_backup_preference**|**tinyint**|Ubicación preferida para realizar copias de seguridad en las bases de datos de disponibilidad en este grupo de disponibilidad. Los valores pueden ser los siguientes:<br /><br /> 0: principal. Las copias de seguridad deben realizarse siempre en la réplica principal.<br />1: solo secundaria. Es preferible realizar copias de seguridad en una réplica secundaria.<br />2: preferir secundaria. Es preferible realizar copias de seguridad en una réplica secundaria, pero se pueden realizar en la réplica principal si no hay ninguna réplica secundaria disponible a tal efecto. Éste es el comportamiento predeterminado.<br />3: todas las réplicas. No se establecen preferencias sobre si las copias de seguridad se deben realizar en la réplica principal o en una secundaria.<br /><br /> Para obtener más información, vea [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Descripción de **automated_backup_preference**, uno de:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Ninguno|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW ANY DEFINITION en la instancia de servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
