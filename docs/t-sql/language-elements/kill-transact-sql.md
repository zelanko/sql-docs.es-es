---
title: KILL (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/31/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- KILL_TSQL
- KILL
dev_langs:
- TSQL
helpviewer_keywords:
- WITH STATUSONLY option
- terminating distributed transactions
- distributed transactions [SQL Server], terminating
- in-doubt transactions
- IDs [SQL Server], user processes
- ending distributed transactions [SQL Server]
- stopping distributed transactions
- session IDs [SQL Server]
- system process termination [SQL Server]
- stopping processes
- ending processes [SQL Server]
- UOW [SQL Server]
- orphaned transactions [SQL Server]
- unit of work [SQL Server]
- process termination [SQL Server]
- KILL statement
- terminating process
ms.assetid: 071cf260-c794-4b45-adc0-0e64097938c0
caps.latest.revision: 61
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 978e780dd19e34c27ceef49ff8388f6ae1f155ed
ms.openlocfilehash: 5a67eb7c7f3686dcb0735f6e1c4a1255ab8b59bd
ms.contentlocale: es-es
ms.lasthandoff: 09/02/2017

---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Termina un proceso de usuario basado en el identificador de sesión o la unidad de trabajo (UOW). Si la sesión especificada Id. o UOW tiene mucho trabajo para deshacer, la instrucción KILL puede tardar algún tiempo en completarse, especialmente cuando implique revertir una transacción larga.  
  
 KILL se puede usar para terminar una conexión normal, que termina internamente las transacciones asociadas al identificador de sesión especificado. La instrucción también puede usarse para terminar las transacciones distribuidas dudosas o huérfanas cuando se use el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server  
  
KILL { session ID | UOW } [ WITH STATUSONLY ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
KILL 'session_id'  
[;]   
```  
  
## <a name="arguments"></a>Argumentos  
 *Id. de sesión*  
 Es el Id. de sesión del proceso que se va a terminar. *Id. de sesión* es un entero único (**int**) que se asigna a cada conexión de usuario cuando se realiza la conexión. El valor del Id. de sesión asociado con la conexión mientras ésta dure. Cuando la conexión finaliza, el valor entero se libera y se puede volver a asignar a una nueva conexión.  
La consulta siguiente puede ayudarle a identificar el `session_id` que desea eliminar:  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**Se aplica a**: ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Identifica el identificador de unidad de trabajo (UOW) de las transacciones distribuidas. *UOW* es un GUID que puede obtenerse a partir de la columna request_owner_guid de la vista de administración dinámica sys.dm_tran_locks. *UOW* también puede obtenerse desde el registro de errores o a través del monitor MS DTC. Para obtener más información sobre cómo supervisar transacciones distribuidas, consulte la documentación de MS DTC.  
  
 Utilice KILL *UOW* para terminar las transacciones distribuidas huérfanas. Estas transacciones no están asociadas a ningún Id. de sesión real, sino que se asocian artificialmente al Id. de sesión = '-2'. Este Id. de sesión facilita la identificación de las transacciones huérfanas al consultar la columna de Id. de sesión en las vistas de administración dinámica sys.dm_tran_locks, sys.dm_exec_sessions o sys.dm_exec_requests.  
  
 WITH STATUSONLY  
 Genera un informe de progreso sobre un determinado *Id. de sesión* o *UOW* que se está revirtiendo debido a una instrucción KILL anterior. KILL WITH STATUSONLY no termina ni revierte el *Id. de sesión* o *UOW*; el comando solo muestra el progreso actual de la reversión.  
  
## <a name="remarks"></a>Comentarios  
 KILL se utiliza normalmente para terminar un proceso que está impidiendo la ejecución de otros procesos mediante bloqueos, o un proceso que está ejecutando una consulta que utiliza recursos necesarios del sistema. No se pueden terminar los procesos del sistema ni los procesos que ejecutan un procedimiento almacenado extendido.  
  
 Utilice KILL con cuidado, especialmente cuando se estén ejecutando procesos críticos. Los procesos propios no se pueden eliminar. Otros procesos que no debería detener son los siguientes:  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
Utilice @@SPID para mostrar el valor de identificador de sesión para la sesión actual.  
  
 Para obtener un informe de los valores de los Id. de sesión activos, puede consultar la columna session_id de las vistas de administración dinámica sys.dm_tran_locks, sys.dm_exec_sessions y sys.dm_exec_requests. También puede ver la columna SPID devuelta por el procedimiento almacenado del sistema sp_who. Si es una reversión en curso de un SPID determinado, la columna cmd del resultado sp_who establecido para que el SPID indica KILLED/ROLLBACK.  
  
 Cuando una conexión específica tiene un bloqueo aplicado a un recurso de base de datos y bloquea el progreso de otra conexión, el identificador de sesión de la conexión que bloquea se muestra en la columna `blocking_session_id` de `sys.dm_exec_requests` o en la columna `blk` devuelta por `sp_who`.  
  
 El comando KILL puede utilizarse para resolver transacciones distribuidas dudosas. Estas transacciones son transacciones distribuidas sin resolver que se producen a causa de reinicios no planeados del servidor de la base de datos o del coordinador de MS DTC. Para obtener más información acerca de las transacciones dudosas, vea la sección "Confirmación en dos fases" en [usar transacciones marcadas para recuperar las bases de datos relacionadas sistemáticamente &#40; Modelo de recuperación completa &#41; ](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>Usar WITH STATUSONLY  
 KILL WITH STATUSONLY genera un informe solo si el Id. de sesión o UOW está revirtiendo actualmente debido a una instrucción KILL *Id. de sesión*|*UOW* instrucción. El informe de progreso indica la cantidad de operaciones de reversión completadas, expresada en porcentaje, y la estimación de tiempo restante, expresada en segundos, de esta forma:  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 Si la reversión del Id. de sesión o UOW ha finalizado cuando ejecute la instrucción KILL *Id. de sesión*|*UOW* se ejecuta la instrucción WITH STATUSONLY, o si ningún Id. de sesión o UOW se está revirtiendo, KILL *Id. de sesión*|*UOW* WITH STATUSONLY devolverá el siguiente error:  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 Puede obtener el mismo informe de estado si se repite la misma instrucción KILL *Id. de sesión*|*UOW* instrucción sin la opción WITH STATUSONLY; sin embargo, no se recomienda hacerlo. Repetir una KILL *Id. de sesión* instrucción podría terminar un proceso nuevo si la reversión había finalizado y se vuelve a asignar el identificador de sesión a una nueva tarea antes de ejecuta la nueva instrucción KILL. Si se especifica WITH STATUSONLY se evita que suceda esto.  
  
## <a name="permissions"></a>Permissions  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** Requiere el permiso ALTER ANY CONNECTION. ALTER ANY CONNECTION se incluye con la pertenencia los roles fijos de servidor sysadmin o processadmin.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:** Requiere el permiso KILL DATABASE CONNECTION. El inicio de sesión de entidad de seguridad de nivel de servidor tiene la conexión de base de datos KILL.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-kill-to-terminate-a-session"></a>A. Usar KILL para terminar una sesión  
 En el siguiente ejemplo se muestra cómo terminar el Id. de sesión `53`.  
  
```sql  
KILL 53;  
GO  
```  
  
### <a name="b-using-kill-session-id-with-statusonly-to-obtain-a-progress-report"></a>B. Usar KILL Id. de sesión WITH STATUSONLY para obtener un informe de progreso  
 En el siguiente ejemplo se genera un estado del proceso de revertir para el Id. de sesión específico.  
  
```sql  
KILL 54;  
KILL 54 WITH STATUSONLY;  
GO  
  
--This is the progress report.  
spid 54: Transaction rollback in progress. Estimated rollback completion: 80% Estimated time left: 10 seconds.  
```  
  
### <a name="c-using-kill-to-terminate-an-orphaned-distributed-transaction"></a>C. Usar KILL para terminar una transacción distribuida huérfana  
 En el ejemplo siguiente se muestra cómo terminar una transacción distribuida huérfana (Id. de sesión = -2) con un *UOW* de `D5499C66-E398-45CA-BF7E-DC9C194B48CF`.  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>Vea también  
 [KILL STATS JOB &#40; Transact-SQL &#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [Eliminar suscripción de notificación de consulta &#40; Transact-SQL &#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [Cierre &#40; Transact-SQL &#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [Sys.dm_exec_requests &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [Sys.dm_exec_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [Sys.dm_tran_locks &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  

