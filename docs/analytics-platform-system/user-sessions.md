---
title: Sesiones de usuario
description: Sesiones de usuario en el almacenamiento de datos paralelos de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399405"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sesiones de usuario en Analytics Platform System
Un inicio de sesión con los permisos adecuados puede administrar las sesiones de todos los inicios de sesión en un PDW de SQL Server dispositivo, incluida la realización de estas acciones:  
  
-   Vea las sesiones actuales en el dispositivo, incluidas las sesiones activas e inactivas.  
  
-   Vea las consultas activas y recientes para una sesión.  
  
-   Finalizar sesiones activas.  
  
Estas acciones se pueden realizar mediante el [monitor del dispositivo mediante la consola de administración](monitor-the-appliance-by-using-the-admin-console.md) o las [vistas del sistema](tsql-system-views.md) a través de comandos SQL, como se muestra a continuación.  
  
Los permisos necesarios para administrar sesiones con cualquiera de los métodos son los mismos y se describen en [conceder permisos para administrar inicios de sesión, usuarios y roles de base de datos](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Administrar sesiones mediante la consola de administración  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Para ver las sesiones actuales mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  La lista resultante muestra todas las sesiones recientes. Para ver solo las sesiones ' Active ' o ' IDLE ', haga clic en el encabezado de columna **status** para ordenar los resultados por estado.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Para ver consultas activas y recientes de una sesión mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  En la lista de resultados, haga clic en el ID. de sesión de la sesión deseada.  
  
3.  La lista consultas resultantes muestra las consultas recientes de la sesión. Para obtener información sobre cómo ver los detalles de la consulta, vea [supervisar consultas activas](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Para finalizar las sesiones mediante la consola de administración  
  
1.  En el menú superior, haga clic en **sesiones**.  
  
2.  Busque el ID. de sesión de la sesión que se va a cancelar.  
  
3.  Haga clic en la **X** roja a la izquierda del ID. de sesión para finalizar la sesión. Solo las sesiones con el estado ' Active ' o ' IDLE ' tendrán una **X**roja; solo se pueden finalizar estas sesiones.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Administrar sesiones mediante vistas del sistema y comandos SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Para ver las sesiones actuales mediante vistas del sistema  
Use [Sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para generar una lista de sesiones actuales.  
  
Este ejemplo devuelve el session_id, el login_name y el estado de todas las sesiones con el estado ' Active ' o ' IDLE '.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Para ver consultas activas y recientes de una sesión mediante las vistas del sistema  
Para ver las consultas activas y completadas recientemente asociadas a una sesión, use las vistas [Sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) y [Sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) . Esta consulta devuelve una lista de todas las sesiones activas o inactivas, además de las consultas activas o recientes asociadas a cada identificador de sesión.  
  
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
Use el comando [Kill](../t-sql/language-elements/kill-transact-sql.md) para finalizar una sesión actual. Necesitará el identificador de sesión para que finalice el proceso, que se puede obtener mediante la vista [Sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) .  
  
En este ejemplo, seleccione los valores de login_name, session_id y status para buscar una sesión basada en el nombre de inicio de sesión.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
Las sesiones con el estado "activo" o "inactivo" se pueden finalizar mediante el comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
