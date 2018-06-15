---
title: Las sesiones de usuario en el sistema de la plataforma de análisis | Documentos de Microsoft"
description: Sesiones de usuario en almacenamiento de datos paralelos del sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: fc2e759d77953f739d77f6ad4eb371cc9747efdc
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31544717"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sesiones de usuario en el sistema de la plataforma de análisis
Un inicio de sesión con los permisos adecuados puede administrar las sesiones de todos los inicios de sesión en un equipo de SQL Server PDW, incluidos realizar estas acciones:  
  
-   Ver las sesiones actuales en el dispositivo, incluidas las sesiones activas e inactivas.  
  
-   Ver las consultas activas y recientes de una sesión.  
  
-   Terminar sesiones activas.  
  
Estas acciones pueden realizarse utilizando el [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) o [vistas del sistema](tsql-system-views.md) a través de comandos SQL, tal y como se muestra a continuación.  
  
Los permisos necesarios para administrar sesiones mediante cualquiera de estos métodos son los mismos y se describen en [conceder permisos para administrar inicios de sesión, usuarios y Roles de base de datos](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Administrar sesiones mediante el uso de la consola de administración  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Para ver las sesiones actuales mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  La lista resultante muestra todas las sesiones recientes. Para ver solo las sesiones 'Active' o 'Inactivo', haga clic en el **estado** encabezado de columna para ordenar los resultados por estado.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Para ver las consultas activas y recientes para una sesión mediante el uso de la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  En la lista de resultados, haga clic en el identificador de sesión de la sesión deseado.  
  
3.  La lista de consultas resultante muestra las consultas recientes para la sesión. Para obtener información acerca de cómo ver detalles de la consulta, vea [supervisión consultas activas](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Para finalizar las sesiones mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  Buscar el identificador de sesión para la sesión para cancelar.  
  
3.  Haga clic en el área roja **X** a la izquierda del identificador de sesión para finalizar la sesión. Solo las sesiones con el estado 'Active' o 'Inactivo' tendrá una roja **X**; solo se pueden terminar estas sesiones.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Administrar sesiones mediante el uso de vistas del sistema y los comandos SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Para ver las sesiones actuales mediante el uso de vistas del sistema  
Use [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para generar una lista de las sesiones actuales.  
  
Este ejemplo devuelve el estado, login_name y session_id para todas las sesiones con el estado 'Active' o 'Inactivo'.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Para ver las consultas activas y recientes para una sesión mediante el uso de vistas del sistema  
Para ver las consultas activas y completadas recientemente asociadas a una sesión, utilice la [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) y [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) vistas. Esta consulta devuelve una lista de todas las sesiones activas o inactivas, además de las consultas activas o recientes asociadas a cada identificador de sesión.  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>Para finalizar las sesiones mediante comandos SQL  
Use la [KILL](../t-sql/language-elements/kill-transact-sql.md) comando para finalizar la sesión actual. Necesitará el identificador de sesión para la terminación del proceso, que puede obtenerse mediante la [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) vista.  
  
En este ejemplo, seleccione login_name, session_id y valores de estado para buscar una sesión basándose en el nombre de inicio de sesión.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
Pueden finalizar las sesiones que tienen un estado 'Active' o 'Inactivo' mediante el comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
