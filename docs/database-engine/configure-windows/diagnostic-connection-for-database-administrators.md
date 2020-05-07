---
title: Conexión de diagnóstico para administradores de bases de datos | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6123b5259f6927c41281fb99264432062fc252bd
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588163"
---
# <a name="diagnostic-connection-for-database-administrators"></a>Conexión de diagnóstico para administradores de bases de datos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una conexión de diagnóstico especial para los administradores cuando no son posibles las conexiones estándar con el servidor. La conexión de diagnóstico permite a un administrador tener acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar consultas de diagnóstico y solucionar problemas, incluso cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no responde a las solicitudes de conexión estándar.  
  
 Esta conexión de administrador dedicada (DAC) admite la característica de cifrado y otras características de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La DAC solo permite cambiar el contexto de usuario a otro usuario de administración.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hace lo posible para que la conexión de administrador dedicada (DAC) sea correcta, pero, en situaciones extremas, es posible que no lo logre.  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]  
  
## <a name="connecting-with-dac"></a>Conectar con DAC  
 De forma predeterminada, solo se permite la conexión desde un cliente que se ejecute en el servidor. Las conexiones de red no están permitidas, a menos que se configuren con el procedimiento almacenado sp_configure con la opción [remote admin connections](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md).  
  
 Solo los miembros del rol sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden conectarse utilizando la DAC.  
  
 La DAC está disponible y permitida a través de la utilidad del símbolo del sistema `sqlcmd` con un modificador de administrador especial (`-A`). Para obtener más información sobre el uso de `sqlcmd`, vea [Usar sqlcmd con variables de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md). También se puede conectar agregando el prefijo `admin:` al nombre de la instancia en formato `sqlcmd -S admin:<*instance_name*>`. También puede iniciar una DAC desde un Editor de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conectándose a `admin:\<*instance_name*>`.

> [!Note]  
> Para establecer una DAC desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
> - Desconecte todas las conexiones a la instancia de SQL Server relacionada, incluido el Explorador de objetos y todas las ventanas de consulta abiertas.
> - En el menú, seleccione **Archivo** > **Nuevo** > **Consulta de motor de base de datos**.
> - En el cuadro de diálogo de conexión, escriba `admin:<server_name>` en el campo Nombre del servidor si usa la instancia predeterminada o `admin:<server_name>\<instance_name>` si usa una instancia con nombre.

## <a name="restrictions"></a>Restricciones  
 Dado que la DAC existe únicamente para el diagnóstico de problemas de servidor en raras circunstancias, hay algunas restricciones en la conexión:  
  
- Para asegurarse de que haya recursos disponibles para la conexión, solo se permite una DAC por cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si ya hay una conexión DAC activa, cualquier solicitud nueva de conexión a través de la DAC se denegará con el error 17810.  
  
- Para ahorrar recursos, [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] no escucha en el puerto DAC a menos que se inicie con la marca de seguimiento 7806.  
  
- Inicialmente la DAC intenta conectarse a la base de datos predeterminada asociada al inicio de sesión. Una vez conectada correctamente, el usuario podrá conectarse a la base de datos maestra. Si la base de datos predeterminada está sin conexión o no disponible por la razón que sea, la conexión devolverá el error 4060. Con todo, se realizará correctamente si invalida la base de datos predeterminada para conectarse a la base de datos maestra utilizando el comando siguiente:  

   ```powershell
   sqlcmd -A -d master 
   ```

   Se recomienda conectarse a la base de datos maestra con la DAC porque su disponibilidad está garantizada si se ha iniciado la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] prohíbe la ejecución de comandos o consultas paralelas con la DAC. Por ejemplo, se genera el error 3637 si se ejecuta una de las instrucciones siguientes con la DAC:  
  
  - `RESTORE...`
  
  - `BACKUP...`

- Con la DAC solo está garantizada la disponibilidad de recursos limitados. No use la DAC para ejecutar consultas que consuman muchos recursos (por ejemplo, una combinación compleja en una tabla grande) o consultas que se puedan bloquear. Así se evita que la DAC agrave cualquier problema de servidor ya existente. Para evitar posibles escenarios de bloqueo, si debe ejecutar consultas que se pueden bloquear, ejecútelas con niveles de aislamiento basado en instantáneas siempre que sea posible; de lo contrario, establezca el nivel de aislamiento de transacción en READ UNCOMMITTED y establezca un valor pequeño, como 2000 milisegundos, para LOCK_TIMEOUT, o ambos. Esto evitará que la sesión de la DAC se bloquee. Sin embargo, dependiendo del estado en el que esté [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede ser que la sesión de la DAC se bloquee en un bloqueo temporal. Es posible que pueda finalizar la sesión de la DAC mediante CTRL+C, pero esto no está garantizado. En tal caso, la única alternativa puede ser reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- Para asegurarse de la conectividad y la solución de problemas con la DAC, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reserva recursos limitados para procesar los comandos ejecutados en la DAC. Estos recursos solo suelen ser suficientes para funciones sencillas de diagnóstico y solución de problemas, como las que se mencionan más adelante.  
  
 Aunque teóricamente es posible ejecutar cualquier instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que no se tenga que ejecutar en paralelo en la DAC, se recomienda encarecidamente limitar el uso a los siguientes comandos de diagnóstico y solución de problemas:  
  
- Consultas en vistas de administración dinámica para diagnósticos básicos, como [sys.dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md) para el estado de bloqueo, [sys.dm_os_memory_cache_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md) para comprobar el estado de las cachés, y [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) y [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) para solicitudes y sesiones activas. Evite las vistas de administración dinámica que consumen muchos recursos (por ejemplo, [sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md) examina el almacén de versiones completo y puede causar numerosas E/S) o que usan combinaciones complejas. Para obtener información acerca de las implicaciones para el rendimiento, vea la documentación específica para la [vista de administración dinámica](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
- Consultas en vistas de catálogo.  
  
- Comandos DBCC básicos como [DBCC FREEPROCCACHE](../..//t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md), [DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md), [DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md) y [DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md). No ejecute comandos que consumen muchos recursos, como [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md), [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md) o [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
- Comando KILL *\<spid>* de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Dependiendo del estado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible que el comando KILL no siempre se ejecute correctamente; en tal caso, la única opción puede ser reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Éstas son algunas directrices generales:  
  
    - Compruebe que realmente se ha eliminado el SPID con la consulta `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`. Si no devuelve ninguna fila, significa que la sesión se ha eliminado.  
  
    - Si la sesión todavía existe, compruebe si hay tareas asignadas a esta sesión ejecutando la consulta `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`. Si ve la tarea, lo más probable es que se esté eliminando la sesión ahora. Tenga en cuenta que es posible que esto tarde bastante tiempo y que no salga correctamente.  
  
    - Si no hay ninguna tarea en sys.dm_os_tasks asociada a esta sesión, pero la sesión permanece en sys.dm_exec_sessions tras ejecutar el comando KILL, significa que no tiene ningún trabajo disponible. Seleccione una de las tareas que se están ejecutando (una tarea que aparece en la vista sys.dm_os_tasks con `sessions_id <> NULL`), y elimine la sesión que tiene asociada para liberar el trabajo. Tenga en cuenta que es posible que no sea suficiente eliminar una sola sesión: posiblemente tendrá que eliminar varias.  
  
## <a name="dac-port"></a>Puerto de la DAC  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha la DAC en el puerto TCP 1434 si está disponible o en un puerto asignado dinámicamente en el inicio de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. El [registro de errores](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md) contiene el número de puerto en el que escucha la DAC. De forma predeterminada, la escucha de la DAC solo acepta la conexión en el puerto local. Para ver un ejemplo de código en el que se activan conexiones de administración remota, vea [remote admin connections (opción de configuración del servidor)](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md).  
  
 Una vez configurada la conexión de administración remota, la escucha de la DAC se habilita sin necesidad de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se puede conectar un cliente a la DAC de forma remota. Puede habilitar la escucha de la DAC para que acepte las conexiones remotamente incluso si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no responde conectándose primero a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la DAC de forma local y, a continuación, ejecutando el procedimiento almacenado sp_configure para aceptar la conexión desde conexiones remotas.  
  
 En las configuraciones de clúster, la DAC estará desactivada de forma predeterminada. Los usuarios pueden ejecutar la opción remote admin connection de sp_configure para habilitar la escucha de la DAC para tener acceso a una conexión remota. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no responde y la escucha de la DAC no está habilitada, es posible que tenga que reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse a la DAC. Por esta razón, es recomendable que habilite la opción de configuración remote admin connections en los sistemas en clúster.  
  
 Durante el inicio, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna dinámicamente el puerto de la DAC. Mientras se establece la conexión a la instancia predeterminada, la DAC evita el uso de una solicitud del protocolo de resolución de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SSRP) al servicio SQL Server Browser. Primero se conecta a través del puerto TCP 1434. Si se produce un error, realiza una llamada SSRP para obtener el puerto. Si el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no escucha las solicitudes SSRP, la solicitud de conexión devolverá un error. Consulte el registro de errores para ver en qué número de puerto escucha la DAC. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceptar conexiones de administración remotas, la DAC debe iniciarse con un número de puerto explícito:  
  
 **sqlcmd -S tcp:** _\<servidor>,\<puerto>_  
  
 El registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra el número de puerto de la DAC, que es 1434 de forma predeterminada. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurado para aceptar solo conexiones DAC locales, conéctese mediante el adaptador de bucles invertidos con el comando siguiente:  
  
 **sqlcmd -S 127.0.0.1,1434**  
  
> [!TIP]  
>  Al conectarse a la [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] con la DAC, también debe especificar el nombre de la base de datos en la cadena de conexión por medio de la opción -d.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo, un administrador observa que el servidor `URAN123` no responde y desea diagnosticar el problema. Para ello, el usuario activa la utilidad del símbolo del sistema `sqlcmd` y se conecta al servidor `URAN123` mediante `-A` para indicar la DAC.  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 Ahora el administrador puede ejecutar consultas para diagnosticar el problema y posiblemente finalizar las sesiones que no responden.  
  
 En un ejemplo similar de conexión a la [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usaría el comando siguiente, incluido el parámetro -d para especificar la base de datos:  
  
 `sqlcmd -S serverName.database.windows.net,1434 -U sa -P <xxx> -d AdventureWorks`  
  
## <a name="related-content"></a>Contenido relacionado  
 [Usar sqlcmd con variables de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
 [Utilidad sqlcmd](../../tools/sqlcmd-utility.md)  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)  
 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
 [DBCC OPENTRAN &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
 [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  

