---
title: Las sesiones de usuario de Analytics Platform System | Microsoft Docs"
description: Sesiones de usuario en almacenamiento del Analytics Platform System de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 33bf052e27640ee08784927351579378bffbec2b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419226"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sesiones de usuario de Analytics Platform System
Un inicio de sesión con los permisos adecuados puede administrar las sesiones de todos los inicios de sesión en un dispositivo PDW de SQL Server, incluida la realización de estas acciones:  
  
-   Ver las sesiones actuales en el dispositivo, incluidas las sesiones activas e inactivas.  
  
-   Ver las consultas activas y recientes de una sesión.  
  
-   Terminar sesiones activas.  
  
Estas acciones pueden realizarse mediante el uso del [supervisar el dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) o [vistas del sistema](tsql-system-views.md) mediante comandos de SQL, como se muestra a continuación.  
  
Los permisos necesarios para administrar sesiones mediante el uso de cualquiera de estos métodos son los mismos y se describen en [conceder permisos para administrar inicios de sesión, usuarios y Roles de base de datos](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Administrar sesiones mediante el uso de la consola de administración  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Para ver las sesiones actuales mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  La lista resultante muestra todas las sesiones recientes. Para ver solo las sesiones 'Active' o 'Idle', haga clic en el **estado** encabezado de columna para ordenar los resultados por estado.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Para ver las consultas activas y recientes de una sesión mediante el uso de la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  En la lista de resultados, haga clic en el identificador de sesión de la sesión deseado.  
  
3.  La lista de consultas resultante muestra las consultas recientes para la sesión. Para obtener información sobre cómo ver los detalles de la consulta, vea [supervisión de consultas activas](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Para finalizar sesiones mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  Busque el identificador de sesión para la sesión para cancelar.  
  
3.  Haga clic en el color rojo **X** a la izquierda de la Id. de sesión para finalizar la sesión. Solo las sesiones con el estado 'Active' o 'Inactivo' tendrán una roja **X**; solo se pueden finalizar estas sesiones.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Administrar sesiones mediante el uso de vistas del sistema y los comandos SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Para ver las sesiones actuales mediante el uso de vistas del sistema  
Use [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para generar una lista de las sesiones actuales.  
  
Este ejemplo devuelve el session_id, login_name y el estado de todas las sesiones con el estado 'Active' o 'Idle'.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Para ver las consultas activas y recientes de una sesión mediante el uso de vistas del sistema  
Para ver las consultas activas y completadas recientemente asociadas a una sesión, utilice el [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) y [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) vistas. Esta consulta devuelve una lista de todas las sesiones activas o inactivas, además de las consultas activas o recientes asociadas con cada identificador de sesión.  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>Para finalizar sesiones mediante comandos SQL  
Use la [KILL](../t-sql/language-elements/kill-transact-sql.md) comando para finalizar la sesión actual. Necesitará el identificador de sesión para la terminación del proceso, que puede obtenerse mediante la [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) vista.  
  
En este ejemplo, seleccione el login_name, session_id y valores de estado para buscar una sesión según el nombre de inicio de sesión.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
Pueden finalizar las sesiones con el estado 'Active' o 'Idle' mediante el comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
