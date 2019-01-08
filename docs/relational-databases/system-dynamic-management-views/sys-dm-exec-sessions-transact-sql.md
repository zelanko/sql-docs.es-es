---
title: Sys.dm_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_sessions_TSQL
- sys.dm_exec_sessions
- dm_exec_sessions
- sys.dm_exec_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sessions dynamic management view
ms.assetid: 2b7e8e0c-eea0-431e-819f-8ccd12ec8cfa
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0b2a01f7c8ffa3616deb0c7f1ebcec1ea94e65dd
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52535189"
---
# <a name="sysdmexecsessions-transact-sql"></a>sys.dm_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada sesión autenticada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sys.dm_exec_sessions es una vista de ámbito de servidor que muestra información acerca de todas las conexiones de usuario activas y las tareas internas. Esta información incluye la versión del cliente, el nombre del programa cliente, la hora de inicio de sesión del cliente, el usuario de inicio de sesión, la configuración de la sesión actual, etcétera. Use sys.dm_exec_sessions para ver, primero, la carga del sistema actual e identificar una sesión de interés y, después, obtener más información acerca de esa sesión con otras vistas o funciones de administración dinámica.  
  
 Las vistas de administración dinámica sys.dm_exec_connections, sys.dm_exec_sessions y sys.dm_exec_requests se asignan a la [sys.sysprocesses](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md) tabla del sistema.  
  
> **NOTA:** Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_exec_sessions**.  
  
|Nombre de columna|Tipo de datos|Descripción e información específica de la versión|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifica la sesión asociada a cada conexión principal activa. No admite valores NULL.|  
|login_time|**datetime**|Hora en que se estableció la sesión. No admite valores NULL.|  
|host_name|**nvarchar(128)**|Nombre de la estación de trabajo cliente específica de una sesión. El valor es NULL para las sesiones internas. Acepta valores NULL.<br /><br /> **Nota de seguridad:** La aplicación cliente proporciona el nombre de la estación de trabajo y puede proporcionar datos inexactos. No confíe en HOST_NAME como característica de seguridad.|  
|program_name|**nvarchar(128)**|Nombre del programa cliente que inició la sesión. El valor es NULL para las sesiones internas. Acepta valores NULL.|  
|host_process_id|**int**|Identificador de proceso del programa cliente que inició la sesión. El valor es NULL para las sesiones internas. Acepta valores NULL.|  
|client_version|**int**|Versión del protocolo TDS de la interfaz utilizada por el cliente para conectarse al servidor. El valor es NULL para las sesiones internas. Acepta valores NULL.|  
|client_interface_name|**nvarchar(32)**|Nombre de la biblioteca o controlador utilizada por el cliente para comunicarse con el servidor. El valor es NULL para las sesiones internas. Acepta valores NULL.|  
|security_id|**varbinary(85)**|Identificador de seguridad de Microsoft Windows asociado al inicio de sesión. No admite valores NULL.|  
|login_name|**nvarchar(128)**|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que se está ejecutando la sesión. Para saber qué nombre de inicio de sesión original ha creado la sesión, vea original_login_name. Puede ser un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autentica el nombre de inicio de sesión o un nombre de usuario de dominio autenticado de Windows. No admite valores NULL.|  
|nt_domain|**nvarchar(128)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Dominio de Windows para el cliente si la sesión utiliza la autenticación de Windows o una conexión de confianza. Este valor es NULL para las sesiones internas y los usuarios que no son del dominio. Acepta valores NULL.|  
|nt_user_name|**nvarchar(128)**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Nombre de usuario de Windows para el cliente si la sesión utiliza la autenticación de Windows o una conexión de confianza. Este valor es NULL para las sesiones internas y los usuarios que no son del dominio. Acepta valores NULL.|  
|status|**nvarchar(30)**|Estado de la sesión. Valores posibles:<br /><br /> **Ejecutando** -uno o más solicitudes en ejecución<br /><br /> **En modo de suspensión** -no hay solicitudes en ejecución actualmente<br /><br /> **Latente** -sesión se ha restablecido debido a la agrupación de conexiones y ahora está en estado de inicio.<br /><br /> **Preconnect** -sesión está en el clasificador del regulador de recursos.<br /><br /> No admite valores NULL.|  
|context_info|**varbinary(128)**|Valor CONTEXT_INFO para la sesión. La información de contexto se establece por el usuario mediante el [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) instrucción. Acepta valores NULL.|  
|cpu_time|**int**|Tiempo de CPU, en milisegundos, utilizado por esta sesión. No admite valores NULL.|  
|memory_usage|**int**|Número de páginas de memoria de 8 KB utilizadas por esta sesión. No admite valores NULL.|  
|total_scheduled_time|**int**|Tiempo total, en milisegundos, para el que se programó la ejecución de la sesión (sus solicitudes). No admite valores NULL.|  
|total_elapsed_time|**int**|Tiempo transcurrido, en milisegundos, desde que se estableció la sesión. No admite valores NULL.|  
|endpoint_id|**int**|Identificador del extremo asociado a la sesión. No admite valores NULL.|  
|last_request_start_time|**datetime**|Hora a la que comenzó la última solicitud de la sesión. Se incluye la solicitud que se ejecuta actualmente. No admite valores NULL.|  
|last_request_end_time|**datetime**|Hora a la que se realizó por última vez una solicitud de la sesión. Acepta valores NULL.|  
|reads|**bigint**|Número de lecturas realizadas, por solicitudes de esta sesión, durante esta sesión. No admite valores NULL.|  
|writes|**bigint**|Número de escrituras realizadas, por solicitudes de esta sesión, durante esta sesión. No admite valores NULL.|  
|logical_reads|**bigint**|Número de lecturas lógicas realizadas en la sesión. No admite valores NULL.|  
|is_user_process|**bit**|0 si es una sesión de sistema; En caso contrario, es 1. No admite valores NULL.|  
|text_size|**int**|Valor de TEXTSIZE para la sesión. No admite valores NULL.|  
|language|**nvarchar(128)**|Valor de LANGUAGE para la sesión. Acepta valores NULL.|  
|date_format|**nvarchar(3)**|Valor de DATEFORMAT para la sesión. Acepta valores NULL.|  
|date_first|**smallint**|Valor de DATEFIRST para la sesión. No admite valores NULL.|  
|quoted_identifier|**bit**|Valor de QUOTED_IDENTIFIER para la sesión. No admite valores NULL.|  
|arithabort|**bit**|Valor de ARITHABORT para la sesión. No admite valores NULL.|  
|ansi_null_dflt_on|**bit**|Valor de ANSI_NULL_DFLT_ON para la sesión. No admite valores NULL.|  
|ansi_defaults|**bit**|Valor de ANSI_DEFAULTS para la sesión. No admite valores NULL.|  
|ansi_warnings|**bit**|Valor de ANSI_WARNINGS para la sesión. No admite valores NULL.|  
|ansi_padding|**bit**|Valor de ANSI_PADDING para la sesión. No admite valores NULL.|  
|ansi_nulls|**bit**|Valor de ANSI_NULLS para la sesión. No admite valores NULL.|  
|concat_null_yields_null|**bit**|Valor de CONCAT_NULL_YIELDS_NULL para la sesión. No admite valores NULL.|  
|transaction_isolation_level|**smallint**|Nivel de aislamiento de transacción de la sesión.<br /><br /> 0 = Unspecified<br /><br /> 1 = ReadUncomitted<br /><br /> 2 = ReadCommitted<br /><br /> 3 = Repeatable<br /><br /> 4 = Serializable<br /><br /> 5 = Snapshot<br /><br /> No admite valores NULL.|  
|lock_timeout|**int**|Valor de LOCK_TIMEOUT para la sesión. El valor se expresa en milisegundos. No admite valores NULL.|  
|deadlock_priority|**int**|Valor de DEADLOCK_PRIORITY para la sesión. No admite valores NULL.|  
|row_count|**bigint**|Número de filas devueltas en la sesión hasta este momento. No admite valores NULL.|  
|prev_error|**int**|Identificador del último error devuelto en la sesión. No admite valores NULL.|  
|original_security_id|**varbinary(85)**|Identificador de seguridad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows asociado al original_login_name. No admite valores NULL.|  
|original_login_name|**nvarchar(128)**|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el cliente usó para crear esta sesión. Puede ser un nombre de inicio de sesión autenticado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un nombre de usuario de dominio autenticado en Windows o un usuario de base de datos independiente. Tenga en cuenta que, después de la conexión inicial, la sesión puede haber pasado por muchos cambios de contexto implícitos o explícitos. Por ejemplo, si [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md) se utiliza. No admite valores NULL.|  
|last_successful_logon|**datetime**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Hora del último inicio de sesión correcto para original_login_name con anterioridad al inicio de sesión actual.|  
|last_unsuccessful_logon|**datetime**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Hora del último intento de inicio de sesión incorrecto para original_login_name con anterioridad al inicio de sesión actual.|  
|unsuccessful_logons|**bigint**|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de intentos de inicio de sesión incorrectos para original_login_name entre last_successful_logon y login_time.|  
|group_id|**int**|Identificador del grupo de cargas de trabajo al que pertenece esta sesión. No admite valores NULL.|  
|database_id|**smallint**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador de la base de datos actual para cada sesión.|  
|authenticating_database_id|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Identificador de la base de datos que autentica la entidad de seguridad. Para los inicios de sesión, el valor será 0. Para los usuarios de base de datos independiente, el valor será el identificador de base de datos de la base de datos independiente.|  
|open_transaction_count|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de transacciones abiertas por sesión.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
## <a name="permissions"></a>Permisos  
Todos pueden ver su propia información de sesión.  
**[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]:** Requiere `VIEW SERVER STATE` permiso en [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para ver todas las sesiones en el servidor.  
**[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]:** Requiere `VIEW DATABASE STATE` para ver todas las conexiones a la base de datos actual. `VIEW DATABASE STATE` no se puede conceder en el `master` base de datos. 
  
  
## <a name="remarks"></a>Comentarios  
 Cuando el **compatibilidad con criterio común habilitada** está habilitada la opción de configuración del servidor, las estadísticas de inicio de sesión se muestran en las siguientes columnas.  
  
-   last_successful_logon  
  
-   last_unsuccessful_logon  
  
-   unsuccessful_logons  
  
 Si esta opción no está habilitada, estas columnas devuelven valores NULL. Para obtener más información sobre cómo establecer la opción de configuración de este servidor, consulte [compatibilidad con criterio común habilitada la opción de configuración del servidor](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md).  
 
 
 Las conexiones de administrador en Azure SQL Database verá una fila por cada sesión autenticada. Las sesiones de "sa" que aparecen en el conjunto de resultados, no tiene ningún impacto en la cuota de usuario para las sesiones. Las conexiones que no es administrador solo verán información relacionada con sus sesiones de usuario de base de datos.
 
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|En / Apply|Relación|  
|----------|--------|---------------|------------------|  
|sys.dm_exec_sessions|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|session_id|Uno a ninguno o uno a varios|  
|sys.dm_exec_sessions|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|session_id|Uno a ninguno o uno a varios|  
|sys.dm_exec_sessions|[sys.dm_tran_session_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)|session_id|Uno a ninguno o uno a varios|  
|sys.dm_exec_sessions|[Sys.dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)(session_id &#124; 0)|session_id CROSS APPLY<br /><br /> OUTER APPLY|Uno a ninguno o uno a varios|  
|sys.dm_exec_sessions|[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)|session_id|Uno a uno|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-finding-users-that-are-connected-to-the-server"></a>A. Buscar usuarios conectados al servidor  
 En el ejemplo siguiente se buscan los usuarios que están conectados al servidor y se devuelve el número de sesiones de cada usuario.  
  
```sql  
SELECT login_name ,COUNT(session_id) AS session_count   
FROM sys.dm_exec_sessions   
GROUP BY login_name;  
```  
  
### <a name="b-finding-long-running-cursors"></a>b. Buscar cursores de ejecución prolongada  
 En el ejemplo siguiente se buscan los cursores que se han abierto durante más de un período concreto, quién los creó y en qué sesión están.  
  
```sql  
USE master;  
GO  
SELECT creation_time ,cursor_id   
    ,name ,c.session_id ,login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s   
   ON c.session_id = s.session_id   
WHERE DATEDIFF(mi, c.creation_time, GETDATE()) > 5;  
```  
  
### <a name="c-finding-idle-sessions-that-have-open-transactions"></a>C. Buscar sesiones inactivas que tienen transacciones abiertas  
 En el ejemplo siguiente se buscan sesiones que tienen transacciones abiertas y están inactivas. Una sesión inactiva es aquélla que no tiene ninguna solicitud en ejecución.  
  
```sql  
SELECT s.*   
FROM sys.dm_exec_sessions AS s  
WHERE EXISTS   
    (  
    SELECT *   
    FROM sys.dm_tran_session_transactions AS t  
    WHERE t.session_id = s.session_id  
    )  
    AND NOT EXISTS   
    (  
    SELECT *   
    FROM sys.dm_exec_requests AS r  
    WHERE r.session_id = s.session_id  
    );  
```  
  
### <a name="d-finding-information-about-a-queries-own-connection"></a>D. Buscar información sobre una conexión propietaria de consultas  
 Consulta típica para recopilar información sobre una conexión solo para consultas.  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



