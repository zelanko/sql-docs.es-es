---
title: Sys. availability_groups_cluster (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a9ca998a0b65fff44e71549d1dae879d73288dfb
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874273"
---
# <a name="sysavailability_groups_cluster-transact-sql"></a>sys.availability_groups_cluster (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada grupo de disponibilidad AlwaysOn en los clústeres de conmutación por error de Windows Server (WSFC). Cada fila contiene los metadatos del grupo de disponibilidad del clúster de WSFC.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identificador único (GUID) del grupo de disponibilidad.|  
|**name**|**sysname**|Nombre del grupo de disponibilidad. Es un nombre definido por el usuario que debe ser único dentro del clúster de conmutación por error de Windows Server (WSFC).|  
|**resource_id**|**nvarchar(40)**|Id. del recurso del clúster WSFC.|  
|**resource_group_id**|**nvarchar(40)**|Id. del grupo de recursos del clúster WSFC del grupo de disponibilidad.|  
|**failure_condition_level**|**int**|Nivel de condición de error definido por el usuario bajo el cual debe activarse una conmutación por error automática; puede tener uno de los valores enteros siguientes:<br /><br /> 1: Especifica que se debe iniciar una conmutación por error automática en los casos siguientes: <br />-El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio está inactivo.<br />-La concesión del grupo de disponibilidad para conectarse al clúster de conmutación por error de WSFC expira porque no se recibe ninguna confirmación de la instancia del servidor. Para más información, vea [Cómo funciona: tiempo de espera de concesión de Always On de SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> 2: Especifica que se debe iniciar una conmutación por error automática en los casos siguientes:  <br />-La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se conecta al clúster y se supera el umbral de **health_check_timeout** especificado por el usuario del grupo de disponibilidad. <br />-La réplica de disponibilidad tiene un estado de error. <br />3: Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] graves, como bloqueos por subproceso huérfanos, infracciones graves de acceso de escritura o un volcado excesivo. Este es el valor predeterminado. <br />4: Especifica que se debe iniciar una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] moderados, tales como una condición persistente de memoria insuficiente en el grupo de recursos de servidor interno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br />5: Especifica que se debe iniciar una conmutación por error automática en el caso de condiciones de error designadas, incluidas las siguientes:<br />-Agotamiento de los subprocesos de trabajo del motor de SQL. <br />-Detección de un interbloqueo no resuelto.<br /><br /> Los niveles de condición de error (1-5) abarcan desde el nivel menos restrictivo (1) al más restrictivo (5). Un nivel de condición dado abarca todos los niveles menos restrictivos. Así pues, el nivel de condición más estricto (el nivel 5) incluye los cuatro niveles de condición menos restrictivos (1-4), el nivel 4 incluye los niveles 1-3, y así sucesivamente.<br /><br /> Para cambiar este valor, use la opción FAILURE_CONDITION_LEVEL de la instrucción [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**health_check_timeout**|**int**|Tiempo de espera (en milisegundos) para que el procedimiento almacenado del sistema [sp_server_diagnostics](../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) devuelva información de estado del servidor, antes de que se asuma que la instancia del servidor es lenta o no responde. El valor predeterminado es 30000 milisegundos (30 segundos).<br /><br /> Para cambiar este valor, use la opción HEALTH_CHECK_TIMEOUT de la instrucción [ALTER Availability Group](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] .|  
|**automated_backup_preference**|**tinyint**|Ubicación preferida para realizar copias de seguridad en las bases de datos de disponibilidad en este grupo de disponibilidad. Uno de los siguientes valores:<br /><br /> 0: Principal. Las copias de seguridad deben realizarse siempre en la réplica principal.<br />1: Solo secundaria. Es preferible realizar copias de seguridad en una réplica secundaria.<br />2: Prefiere secundaria. Es preferible realizar copias de seguridad en una réplica secundaria, pero se pueden realizar en la réplica principal si no hay ninguna réplica secundaria disponible a tal efecto. Éste es el comportamiento predeterminado.<br />3: Cualquier réplica. No se establecen preferencias sobre si las copias de seguridad se deben realizar en la réplica principal o en una secundaria.<br /><br /> Para más información, consulte [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;grupos de disponibilidad Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**automated_backup_preference_desc**|**nvarchar(60)**|Descripción de **automated_backup_preference**, uno de los siguientes:<br /><br /> PRIMARY<br /><br /> SECONDARY_ONLY<br /><br /> SECONDARY<br /><br /> Ninguno|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW ANY DEFINITION en la instancia de servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
