---
title: sys.availability_replicas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d6babc4d32782e6bf7321deb0a1778fff644bd14
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/14/2019
ms.locfileid: "54257080"
---
# <a name="sysavailabilityreplicas-transact-sql"></a>sys.availability_replicas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Devuelve una fila para cada una de las réplicas de disponibilidad que pertenecen a ningún grupo de disponibilidad Always On en el clúster de conmutación por error WSFC.  
  
Si la instancia del servidor local no puede comunicar con el clúster de conmutación por error de WSFC, debido por ejemplo a que el clúster está inactivo o se ha perdido el quorum, solo se devuelven las filas de las réplicas de disponibilidad locales. Estas filas contendrán solamente las columnas de datos que están almacenadas localmente en caché en metadatos.  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**replica_id**|**uniqueidentifier**|Identificador único de la réplica.|  
|**group_id**|**uniqueidentifier**|Identificador único del grupo de disponibilidad al que pertenece la réplica.|  
|**replica_metadata_id**|**int**|Identificador del objeto de metadatos local correspondiente a las réplicas de disponibilidad en el motor de base de datos.|  
|**replica_server_name**|**nvarchar(256)**|Nombre de servidor de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda esta réplica y, para una instancia no predeterminada, su nombre de instancia.|  
|**owner_sid**|**varbinary(85)**|Identificador de seguridad (SID) registrado en esta instancia de servidor para el propietario externo de esta réplica de disponibilidad.<br /><br /> NULL para las réplicas de disponibilidad no locales.|  
|**endpoint_url**|**nvarchar(128)**|Representación en forma de cadena de la base de datos definida por el usuario que crea un reflejo del extremo usado por las conexiones entre las réplicas principal y secundaria para la sincronización de datos. Para obtener más información sobre la sintaxis de las direcciones URL del punto de conexión, vea [Especificar la dirección URL del punto de conexión al agregar o modificar una réplica de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md).<br /><br /> NULL = No se puede comunicar con el clúster de conmutación por error de WSFC.<br /><br /> Para cambiar este punto de conexión, utilice la opción ENDPOINT_URL de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**availability_mode**|**tinyint**|Modo de disponibilidad de la réplica, que puede ser alguno de los siguientes:<br /><br /> 0 &#124; confirmación asincrónica. La réplica principal puede confirmar transacciones sin esperar a que la réplica secundaria escriba el registro en disco.<br /><br /> 1 &#124; confirmación sincrónica. La réplica principal espera para confirmar una determinada transacción hasta que la réplica secundaria escribe la transacción en el disco.<br /><br />4 &#124; solo la configuración. La réplica principal envía los metadatos de configuración del grupo de disponibilidad a la réplica de forma sincrónica. Datos de usuario no se transmiten a la réplica. Disponible en SQL Server 2017 CU1 y versiones posteriores.<br /><br /> Para obtener más información, vea [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md).|  
|**availability_mode_desc**|**nvarchar(60)**|Descripción de **disponibilidad\_modo**, uno de:<br /><br /> ASINCRÓNICA\_CONFIRMAR<br /><br /> SINCRÓNICO\_CONFIRMAR<br /><br /> CONFIGURACIÓN\_SOLO<br /><br /> Para cambiar esto en el modo de disponibilidad de una réplica de disponibilidad, utilice la opción AVAILABILITY_MODE de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.<br/><br>No se puede cambiar el modo de disponibilidad de una réplica a configuración\_solo. No se puede cambiar una configuración\_réplica solo a una réplica secundaria o principal. |  
|**failover\_mode**|**tinyint**|El [modo de conmutación por error](../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) de la réplica de disponibilidad, uno de:<br /><br /> 0 &#124; conmutación automática por error. La réplica es un posible objetivo de las conmutaciones por error automáticas.  Conmutación automática por error solo se admite si se establece el modo de disponibilidad en confirmación sincrónica (**disponibilidad\_modo** = 1) y la réplica de disponibilidad está sincronizada actualmente.<br /><br /> 1 &#124; conmutación por error manual. La conmutación por error a una réplica secundaria establecida en conmutación por error manual la debe iniciar manualmente el administrador de la base de datos. El tipo de conmutación por error que se realice dependerá de si se ha sincronizado la réplica secundaria, del modo siguiente:<br /><br /> Si la réplica de disponibilidad no se ha sincronizado o se está sincronizando todavía, solo se puede realizar una conmutación por error forzada (con la posibilidad de que se pierdan datos).<br /><br /> Si se establece el modo de disponibilidad en confirmación sincrónica (**disponibilidad\_modo** = 1) y la réplica de disponibilidad está actualmente conmutación por error manual y sincronizada sin puede producirse una pérdida de datos.<br /><br /> Para ver un resumen del estado de sincronización de base de datos de cada base de datos de disponibilidad en una réplica de disponibilidad, use el **sincronización\_mantenimiento** y **sincronización\_mantenimiento\_desc** columnas de la [sys.dm_hadr_availability_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql.md) vista de administración dinámica. El resumen tiene en cuenta el estado de sincronización de todas las bases de datos de disponibilidad y el modo de disponibilidad de sus réplicas de disponibilidad.<br /><br /> **Nota:** Para ver el estado de sincronización de una base de datos de disponibilidad determinado, consulte el **sincronización\_estado** y **sincronización\_mantenimiento** columnas de la [sys.dm_hadr_database_replica_states](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) vista de administración dinámica.|  
|**failover\_mode\_desc**|**nvarchar(60)**|Descripción de **conmutación por error\_modo**, uno de:<br /><br /> MANUAL<br /><br /> AUTOMATIC<br /><br /> Para cambiar el modo de conmutación por error, utilice la conmutación por error\_opción modo de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**session\_timeout**|**int**|Período de tiempo de espera, en segundos. El período de tiempo de espera es el tiempo máximo que la réplica espera hasta recibir un mensaje de otra réplica antes de considerar que se ha producido un error en la conexión entre la réplica principal y secundaria. El tiempo de espera de la sesión detecta si las réplicas secundarias están conectadas a la réplica principal.<br /><br /> Al detectar un error en la conexión con una réplica secundaria, la réplica principal considera que la réplica secundaria no\_SYNCHRONIZED. Al detectar un error en la conexión con la réplica principal, la réplica secundaria intenta volver a conectarse.<br /><br /> **Nota:** Cuando se agota el tiempo de espera de la sesión, no se realiza una conmutación por error automática.<br /><br /> Para cambiar este valor, use la opción SESSION_TIMEOUT de [ALTER AVAILABILITY GROUP](../../t-sql/statements/alter-availability-group-transact-sql.md) [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción.|  
|**principal\_rol\_permitir\_conexiones**|**tinyint**|Si la disponibilidad permite todas las conexiones o solamente conexiones de lectura/escritura, que puede tener uno de los siguientes valores:<br /><br /> 2 = Todas (predeterminado)<br /><br /> 3 = Lectura/escritura|  
|**principal\_rol\_permitir\_conexiones\_desc**|**nvarchar(60)**|Descripción de **principal\_rol\_permitir\_conexiones**, uno de:<br /><br /> ALL<br /><br /> LEER\_ESCRIBIR|  
|**secundaria\_rol\_permitir\_conexiones**|**tinyint**|Si una réplica de disponibilidad que está realizando el rol secundario (es decir, una réplica secundaria) puede aceptar conexiones de clientes; puede tener uno de los valores siguientes:<br /><br /> 0 = No. No se permiten conexiones directas con las bases de datos de la réplica secundaria y las bases de datos no están disponible para acceso de lectura. Esta es la configuración predeterminada.<br /><br /> 1 = Solo lectura. Solo se permiten conexiones de solo lectura a las bases de datos de la réplica secundaria. Todas las bases de datos de la réplica están disponibles para acceso de lectura.<br /><br /> 2 = Todas. Se permiten todas las conexiones con las bases de datos de la réplica secundaria para acceso de solo lectura.<br /><br /> Para obtener más información, consulte [secundarias activas: Las réplicas secundarias legibles &#40;grupos de disponibilidad Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).|  
|**secondary_role_allow_connections_desc**|**nvarchar(60)**|Descripción de **secondary_role_allow_connections**, uno de:<br /><br /> No<br /><br /> READ_ONLY<br /><br /> ALL|  
|**create_date**|**datetime**|Fecha en que se creó la réplica.<br /><br /> NULL = La réplica no está en esta instancia de servidor.|  
|**modify_date**|**datetime**|Fecha de la última modificación de la réplica.<br /><br /> NULL = La réplica no está en esta instancia de servidor.|  
|**backup_priority**|**int**|Representa la prioridad definida por el usuario para realizar copias de seguridad en esta réplica en relación con las otras réplicas del mismo grupo de disponibilidad. El valor es un número entero en el intervalo de 0..100.<br /><br /> Para obtener más información, consulte [secundarias activas: Copia de seguridad en réplicas secundarias &#40;grupos de disponibilidad Always On&#41;](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).|  
|**read_only_routing_url**|**nvarchar(256)**|Extremo de conectividad (URL) de la réplica de disponibilidad de solo lectura. Para obtener más información, vea [Configurar el enrutamiento de solo lectura para un grupo de disponibilidad &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md).|  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW ANY DEFINITION en la instancia de servidor.  
  
## <a name="see-also"></a>Vea también  
 [sys.availability_groups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-groups-transact-sql.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Supervisar grupos de disponibilidad &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
