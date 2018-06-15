---
title: KILL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d2cf23ffc6cceaf92f80eb75dbe9da1179e9e4a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064172"
---
# <a name="kill-transact-sql"></a>KILL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Termina un proceso de usuario basado en el identificador de sesión o la unidad de trabajo (UOW). Si el identificador de sesión o UOW especificado tiene que deshacer muchas operaciones, puede que la instrucción KILL tarde en completarse, especialmente cuando implique revertir una transacción larga.  
  
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
 *session ID*  
 Es el Id. de sesión del proceso que se va a terminar. *session ID* es un entero único (**int**) asignado a cada conexión de usuario en el momento de realizarla. El valor del Id. de sesión asociado con la conexión mientras ésta dure. Cuando la conexión finaliza, el valor entero se libera y se puede volver a asignar a una nueva conexión.  
La consulta siguiente puede ayudarle a identificar el valor `session_id` que quiere terminar:  
 ```sql  
 SELECT conn.session_id, host_name, program_name,
     nt_domain, login_name, connect_time, last_request_end_time 
FROM sys.dm_exec_sessions AS sess
JOIN sys.dm_exec_connections AS conn
    ON sess.session_id = conn.session_id;
```  
  
*UOW*  
**Se aplica a:** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Identifica el identificador de unidad de trabajo (UOW) de las transacciones distribuidas. *UOW* es un GUID que puede obtenerse desde la columna request_owner_guid de la vista de administración dinámica sys.dm_tran_locks. *UOW* también puede obtenerse desde el registro de errores o a través del monitor MS DTC. Para obtener más información sobre cómo supervisar transacciones distribuidas, consulte la documentación de MS DTC.  
  
 Use KILL *UOW* para terminar transacciones distribuidas huérfanas. Estas transacciones no están asociadas a ningún Id. de sesión real, sino que se asocian artificialmente al Id. de sesión = '-2'. Este Id. de sesión facilita la identificación de las transacciones huérfanas al consultar la columna de Id. de sesión en las vistas de administración dinámica sys.dm_tran_locks, sys.dm_exec_sessions o sys.dm_exec_requests.  
  
 WITH STATUSONLY  
 Genera un informe de progreso sobre un parámetro *session ID* o *UOW* especificado que se está revirtiendo a causa de una instrucción KILL anterior. KILL WITH STATUSONLY no termina ni revierte *session ID* o *UOW*; el comando solo muestra el progreso actual de la reversión.  
  
## <a name="remarks"></a>Notas  
 KILL se utiliza normalmente para terminar un proceso que está impidiendo la ejecución de otros procesos mediante bloqueos, o un proceso que está ejecutando una consulta que utiliza recursos necesarios del sistema. No se pueden terminar los procesos del sistema ni los procesos que ejecutan un procedimiento almacenado extendido.  
  
 Use KILL con cuidado, especialmente cuando se estén ejecutando procesos críticos. Los procesos propios no se pueden eliminar. Otros procesos que no se deben eliminar son:  
  
-   AWAITING COMMAND  
-   CHECKPOINT SLEEP  
-   LAZY WRITER  
-   LOCK MONITOR  
-   SIGNAL HANDLER  
  
Use @@SPID para mostrar el valor session ID de la sesión actual.  
  
 Para obtener un informe de los valores de los Id. de sesión activos, puede consultar la columna session_id de las vistas de administración dinámica sys.dm_tran_locks, sys.dm_exec_sessions y sys.dm_exec_requests. También puede ver la columna SPID devuelta por el procedimiento almacenado del sistema sp_who. Si se está realizando la reversión de un SPID determinado, la columna cmd del conjunto de resultados sp_who para ese SPID indica KILLED/ROLLBACK.  
  
 Cuando una conexión específica tiene un bloqueo aplicado a un recurso de base de datos y bloquea el progreso de otra conexión, el identificador de sesión de la conexión que bloquea se muestra en la columna `blocking_session_id` de `sys.dm_exec_requests` o en la columna `blk` devuelta por `sp_who`.  
  
 El comando KILL puede utilizarse para resolver transacciones distribuidas dudosas. Estas transacciones son transacciones distribuidas sin resolver que se producen a causa de reinicios no planeados del servidor de la base de datos o del coordinador de MS DTC. Para obtener más información sobre transacciones dudosas, vea la sección "Confirmación en dos fases" de [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="using-with-statusonly"></a>Usar WITH STATUSONLY  
 KILL WITH STATUSONLY solo genera un informe si el parámetro session ID o UOW se está revirtiendo actualmente a causa de una instrucción KILL *session ID*|*UOW* anterior. El informe de progreso indica la cantidad de operaciones de reversión completadas, expresada en porcentaje, y la estimación de tiempo restante, expresada en segundos, de esta forma:  
  
 `Spid|UOW <xxx>: Transaction rollback in progress. Estimated rollback completion: <yy>% Estimated time left: <zz> seconds`  
  
 Si la reversión de session ID o UOW ha finalizado cuando se ejecuta la instrucción KILL *session ID*|*UOW* WITH STATUSONLY, o si no se está revirtiendo session ID o UOW, KILL *session ID*|*UOW* WITH STATUSONLY devuelve el siguiente error:  
  
 ```
"Msg 6120, Level 16, State 1, Line 1"  
"Status report cannot be obtained. Rollback operation for Process ID <session ID> is not in progress."
```  
  
 Se puede obtener el mismo informe de estado si se repite la misma instrucción KILL *session ID*|*UOW* sin la opción WITH STATUSONLY, aunque no se recomienda hacerlo. Repetir una instrucción KILL *session ID* puede terminar un proceso nuevo si la operación de revertir había finalizado y session ID se volvió a asignar a una nueva tarea antes de ejecutar la nueva instrucción KILL. Si se especifica WITH STATUSONLY se evita que suceda esto.  
  
## <a name="permissions"></a>Permisos  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:** Requiere el permiso ALTER ANY CONNECTION. ALTER ANY CONNECTION se incluye con la pertenencia los roles fijos de servidor sysadmin o processadmin.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)]:** Requiere el permiso KILL DATABASE CONNECTION. El inicio de sesión de entidad de seguridad a nivel de servidor tiene KILL DATABASE CONNECTION.  
  
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
 En el siguiente ejemplo se muestra cómo terminar una transacción distribuida huérfana (session ID = -2) con un valor *UOW* de `D5499C66-E398-45CA-BF7E-DC9C194B48CF`.  
  
```sql  
KILL 'D5499C66-E398-45CA-BF7E-DC9C194B48CF';  
```  

  
## <a name="see-also"></a>Ver también  
 [KILL STATS JOB &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-stats-job-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)   
 [@@SPID &#40;Transact-SQL&#41;](../../t-sql/functions/spid-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
  
  
