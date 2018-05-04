---
title: Sys.availability_groups (Transact-SQL) | Documentos de Microsoft
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
- sys.availability_groups_TSQL
- availability_groups_TSQL
- sys.availability_groups
- availability_groups
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_groups catalog view
ms.assetid: da7fa55f-c008-45d9-bcfc-3513b02d9e71
caps.latest.revision: 42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3874bde2c43ddcba3e0ef365ff371a54ffcb8ad
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysavailabilitygroups-transact-sql"></a>sys.availability_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada grupo de disponibilidad para los que la instancia local de SQL Server hospeda una réplica de disponibilidad. Cada fila contiene una copia almacenada en caché de los metadatos del grupo de disponibilidad.  
   
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador único (GUID) del grupo de disponibilidad.|  
|**Nombre**|**sysname**|Nombre del grupo de disponibilidad. Es un nombre definido por el usuario que debe ser único dentro del clúster de conmutación por error de Windows Server (WSFC).|  
|**resource_id**|**nvarchar(40)**|Id. del recurso del clúster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|Id. del grupo de recursos del clúster WSFC del grupo de disponibilidad.|  
|**failure_condition_level**|**int**|Error definido por el usuario nivel de condición en la que debe desencadenar una conmutación automática por error, uno de los valores enteros que se muestran en la tabla inmediatamente por debajo de esta tabla.<br /><br /> Los niveles de condición de error (1-5) abarcan desde el nivel menos restrictivo (1) al más restrictivo (5). Un nivel de condición dado abarca todos los niveles menos restrictivos. Así pues, el nivel de condición más estricto (el nivel 5) incluye los cuatro niveles de condición menos restrictivos (1-4), el nivel 4 incluye los niveles 1-3, y así sucesivamente.<br /><br /> Para cambiar este valor, utilice la opción FAILURE_CONDITION_LEVEL de la [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**health_check_timeout**|**int**|Tiempo de espera (en milisegundos) para la [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) sistema procedimiento almacenado para devolver información de estado del servidor, antes de que la instancia del servidor se supone que es lento o se ha bloqueado. El valor predeterminado es 30000 milisegundos (30 segundos).<br /><br /> Para cambiar este valor, utilice la opción HEALTH_CHECK_TIMEOUT de la [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**automated_backup_preference**|**tinyint**|Ubicación preferida para realizar copias de seguridad en las bases de datos de disponibilidad en este grupo de disponibilidad. Éstos son los valores posibles y sus descripciones.<br /><br /> <br /><br /> 0: principal. Las copias de seguridad deben realizarse siempre en la réplica principal.<br /><br /> 1: solo secundaria. Es preferible realizar copias de seguridad en una réplica secundaria.<br /><br /> 2: preferir secundaria. Es preferible realizar copias de seguridad en una réplica secundaria, pero se pueden realizar en la réplica principal si no hay ninguna réplica secundaria disponible a tal efecto. Éste es el comportamiento predeterminado.<br /><br /> 3: todas las réplicas. No se establecen preferencias sobre si las copias de seguridad se deben realizar en la réplica principal o en una secundaria.<br /><br /> <br /><br /> Para obtener más información, vea [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Descripción de **automated_backup_preference**, uno de:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Ninguno|  
|**version**|**smallint**|La versión de los metadatos del grupo de disponibilidad almacenada en el clúster de conmutación por error de Windows. Este número de versión se incrementa cuando se agregan nuevas características.|  
|**basic_features**|**bit**|Especifica si se trata de un grupo de disponibilidad básica. Para obtener más información, vea [Grupos de disponibilidad básica &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).|  
|**dtc_support**|**bit**|Especifica si se ha habilitado la compatibilidad con DTC para este grupo de disponibilidad. El **DTC_SUPPORT** opción de **CREATE AVAILABILITY GROUP** controla esta configuración.|  
|**db_failover**|**bit**|Especifica si el grupo de disponibilidad admite la conmutación por error para condiciones de mantenimiento de base de datos. El **DB_FAILOVER** opción de **CREATE AVAILABILITY GROUP** controla esta configuración.|  
|**is_distributed**|**bit**|Especifica si se trata de un grupo de disponibilidad distribuido. Para obtener más información, vea [Distributed Availability Groups &#40;Always On Availability Groups&#41; (Grupos de disponibilidad distribuida &#40;grupos de disponibilidad AlwaysOn&#41;)](../../database-engine/availability-groups/windows/distributed-availability-groups-always-on-availability-groups.md).|  
  
## <a name="failure-condition-level--values"></a>Valores de nivel de condición de error  
 La tabla siguiente describen los niveles de condición de error posibles para la **failure_condition_level** columna.  
  
|Value|Condición de error|  
|-----------|-----------------------|  
|1|Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:<br /><br /> <br /><br /> -El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio no está funcionando.<br /><br /> -La concesión del grupo de disponibilidad para conectarse al clúster de conmutación por error WSFC expira porque no se ha recibido ninguna confirmación de la instancia del servidor. Para obtener más información, vea [Cómo funciona: tiempo de espera de concesión de AlwaysOn de SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).|  
|2|Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:<br /><br /> <br /><br /> -La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se conecta al clúster y el especificado por el usuario **health_check_timeout** se superó el umbral del grupo de disponibilidad.<br /><br /> -La réplica de disponibilidad está en estado de error.|  
|3|Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] graves, como bloqueos por subproceso huérfanos, infracciones graves de acceso de escritura o un volcado excesivo.<br /><br /> Es el valor predeterminado.|  
|4|Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] moderados, tales como una condición persistente de memoria insuficiente en el grupo de recursos de servidor interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|5|Especifica que se debe iniciar una conmutación por error automática en el caso de condiciones de error designadas, incluidas las siguientes:<br /><br /> <br /><br /> -Agotamiento de subprocesos de trabajo del motor de SQL.<br /><br /> -La detección de un interbloqueo irresoluble.|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW ANY DEFINITION en la instancia de servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad & #40; Transact-SQL & #41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
