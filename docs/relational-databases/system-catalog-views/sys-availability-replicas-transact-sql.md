---
title: Sys.availability_replicas (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- availability_replicas_TSQL
- availability_replicas
- sys.availability_replicas
- sys.availability_replicas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.availability_replicas catalog view
ms.assetid: 0a06e9b6-a1e4-4293-867b-5c3f5a8ff62c
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c519483b311a7556e1c4309f494144a2c0d19751
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysavailabilityreplicas-transact-sql"></a>sys.availability_replicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Devuelve una fila para cada una de las réplicas de disponibilidad que pertenecen a cualquier grupo de disponibilidad AlwaysOn del clúster de conmutación por error WSFC.  
  
Si la instancia del servidor local no puede comunicar con el clúster de conmutación por error de WSFC, debido por ejemplo a que el clúster está inactivo o se ha perdido el quorum, solo se devuelven las filas de las réplicas de disponibilidad locales. Estas filas contendrán solamente las columnas de datos que están almacenadas localmente en caché en metadatos.  
  
 
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador único de la réplica.|  
|**group_id**|**uniqueidentifier**|Identificador único del grupo de disponibilidad al que pertenece la réplica.|  
|**replica_metadata_id**|**int**|Identificador del objeto de metadatos local correspondiente a las réplicas de disponibilidad en el motor de base de datos.|  
|**replica_server_name**|**nvarchar(256)**|Nombre de servidor de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda esta réplica y, para una instancia no predeterminada, su nombre de instancia.|  
|**owner_sid**|**varbinary(85)**|Identificador de seguridad (SID) registrado en esta instancia de servidor para el propietario externo de esta réplica de disponibilidad.<br /><br /> NULL para las réplicas de disponibilidad no locales.|  
|**endpoint_url**|**nvarchar(128)**|Representación en forma de cadena de la base de datos definida por el usuario que crea un reflejo del extremo usado por las conexiones entre las réplicas principal y secundaria para la sincronización de datos. Para obtener más información sobre la sintaxis de las direcciones URL del punto de conexión, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).<br /><br /> NULL = No se puede comunicar con el clúster de conmutación por error de WSFC.<br /><br /> Para cambiar este punto de conexión, utilice la opción de ENDPOINT_URL de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**availability_mode**|**tinyint**|Modo de disponibilidad de la réplica, que puede ser alguno de los siguientes:<br /><br /> 0 &#124; Confirmación asincrónica. La réplica principal puede confirmar transacciones sin esperar a que la réplica secundaria escriba el registro en disco.<br /><br /> 1 &#124; Confirmación sincrónica. La réplica principal espera para confirmar una determinada transacción hasta que la réplica secundaria escribe la transacción en el disco.<br /><br />4 &#124; Solo la configuración. La réplica principal envía los metadatos de configuración del grupo de disponibilidad a la réplica de forma sincrónica. Datos de usuario no se transmiten a la réplica. Está disponible en SQL Server de 2017 CU1 y versiones posteriores.<br /><br /> Para obtener más información, vea [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).|  
|**availability_mode_desc**|**nvarchar(60)**|Descripción de **disponibilidad\_modo**, uno de:<br /><br /> ASINCRÓNICA\_CONFIRMAR<br /><br /> SINCRÓNICO\_CONFIRMAR<br /><br /> CONFIGURACIÓN\_SÓLO<br /><br /> Para cambiar este modo de disponibilidad de una réplica de disponibilidad, utilice la opción AVAILABILITY_MODE de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.<br/><br>No se puede cambiar el modo de disponibilidad de una réplica a configuración\_sólo. No se puede cambiar una configuración\_réplica sólo en una réplica principal o secundaria. |  
|**conmutación por error\_modo**|**tinyint**|El [modo de conmutación por error](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) de la réplica de disponibilidad, uno de:<br /><br /> 0 &#124; Conmutación por error manual. La conmutación por error a una réplica secundaria establecida en conmutación por error manual la debe iniciar manualmente el administrador de la base de datos. El tipo de conmutación por error que se realice dependerá de si se ha sincronizado la réplica secundaria, del modo siguiente:<br /><br /> Si la réplica de disponibilidad no se ha sincronizado o se está sincronizando todavía, solo se puede realizar una conmutación por error forzada (con la posibilidad de que se pierdan datos).<br /><br /> Si el modo de disponibilidad se establece en confirmación sincrónica (**disponibilidad\_modo** = 1) y la réplica de disponibilidad está actualmente conmutación por error manual y sincronizada sin puede producir una pérdida de datos.<br /><br /> 1 &#124; Conmutación automática por error. La réplica es un posible objetivo de las conmutaciones por error automáticas.  Conmutación automática por error solo se admite si el modo de disponibilidad se establece en confirmación sincrónica (**disponibilidad\_modo** = 1) y la réplica de disponibilidad está sincronizada actualmente.<br /><br /> Para ver un resumen del estado de sincronización de base de datos de cada base de datos de disponibilidad en una réplica de disponibilidad, use la **sincronización\_estado** y **sincronización\_estado\_desc** columnas de la [sys.dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) vista de administración dinámica. El resumen tiene en cuenta el estado de sincronización de todas las bases de datos de disponibilidad y el modo de disponibilidad de sus réplicas de disponibilidad.<br /><br /> **Nota:** para ver el estado de sincronización de una base de datos de disponibilidad determinado, consulte la **sincronización\_estado** y **sincronización\_estado** columnas de la [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) vista de administración dinámica.|  
|**failover\_mode\_desc**|**nvarchar(60)**|Descripción de **conmutación por error\_modo**, uno de:<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> Para cambiar el modo de conmutación por error, use la conmutación por error\_opción del modo de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**session\_timeout**|**int**|Período de tiempo de espera, en segundos. El período de tiempo de espera es el tiempo máximo que la réplica espera hasta recibir un mensaje de otra réplica antes de considerar que se ha producido un error en la conexión entre la réplica principal y secundaria. El tiempo de espera de la sesión detecta si las réplicas secundarias están conectadas a la réplica principal.<br /><br /> Al detectar un error en la conexión con una réplica secundaria, la réplica principal considera que la réplica secundaria que no son\_SYNCHRONIZED. Al detectar un error en la conexión con la réplica principal, la réplica secundaria intenta volver a conectarse.<br /><br /> **Nota:** los tiempos de espera de sesión no hacen que las conmutaciones por error automáticas.<br /><br /> Para cambiar este valor, utilice la opción SESSION_TIMEOUT de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**principal\_rol\_permitir\_conexiones**|**tinyint**|Si la disponibilidad permite todas las conexiones o solamente conexiones de lectura/escritura, que puede tener uno de los siguientes valores:<br /><br /> 2 = Todas (predeterminado)<br /><br /> 3 = Lectura/escritura|  
|**primary\_role\_allow\_connections\_desc**|**nvarchar(60)**|Descripción de **principal\_rol\_permitir\_conexiones**, uno de:<br /><br /> ALL<br /><br /> LEER\_ESCRIBIR|  
|**secundaria\_rol\_permitir\_conexiones**|**tinyint**|Si una réplica de disponibilidad que está realizando el rol secundario (es decir, una réplica secundaria) puede aceptar conexiones de clientes; puede tener uno de los valores siguientes:<br /><br /> 0 = No. No se permiten conexiones directas con las bases de datos de la réplica secundaria y las bases de datos no están disponible para acceso de lectura. Esta es la configuración predeterminada.<br /><br /> 1 = Solo lectura. Solo se permiten conexiones de solo lectura a las bases de datos de la réplica secundaria. Todas las bases de datos de la réplica están disponibles para acceso de lectura.<br /><br /> 2 = Todas. Se permiten todas las conexiones con las bases de datos de la réplica secundaria para acceso de solo lectura.<br /><br /> Para obtener más información, vea [Secundarias activas: réplicas secundarias legibles &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|Descripción de **secondary_role_allow_connections**, uno de:<br /><br /> No<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|Fecha en que se creó la réplica.<br /><br /> NULL = La réplica no está en esta instancia de servidor.|  
|**modify_date**|**datetime**|Fecha de la última modificación de la réplica.<br /><br /> NULL = La réplica no está en esta instancia de servidor.|  
|**backup_priority**|**int**|Representa la prioridad definida por el usuario para realizar copias de seguridad en esta réplica en relación con las otras réplicas del mismo grupo de disponibilidad. El valor es un número entero en el intervalo de 0..100.<br /><br /> Para obtener más información, vea [Secundarias activas: copia de seguridad en las réplicas secundarias &#40;Grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**read_only_routing_url**|**nvarchar(256)**|Extremo de conectividad (URL) de la réplica de disponibilidad de solo lectura. Para obtener más información, vea [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW ANY DEFINITION en la instancia de servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad &#40; Transact-SQL &#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
