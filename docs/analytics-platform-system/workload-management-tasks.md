---
title: 'Tareas de administración de cargas de trabajo: Analytics Platform System | Documentos de Microsoft'
description: Tareas de administración de cargas de trabajo en el sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 16206cb5cefd68b19e1640592b903890808b5a31
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Tareas de administración de cargas de trabajo en el sistema de la plataforma de análisis
Tareas de administración de cargas de trabajo en el sistema de la plataforma de análisis.

## <a name="view-login-members-of-each-resource-class"></a>Ver los miembros de inicio de sesión de cada clase de recurso
Describe cómo mostrar a los miembros de inicio de sesión de cada rol de servidor de la clase de recurso en PDW de SQL Server. Utilice esta consulta para averiguar la clase de recursos permitido para las solicitudes enviadas por cada inicio de sesión.  
  
Para obtener descripciones de clase de recursos, consulte [administración de cargas de trabajo](workload-management.md).  
  
Esta consulta muestra la lista de miembros de cada clase de recursos. Hay tres clases de recursos, mediumrc, largerc y xlargerc.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  ( l.[type] = 'S' OR l.[type] = 'U' OR l.[type] = 'G' )  
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
```  
  
Si un inicio de sesión no está en esta lista, sus solicitudes recibirán los recursos predeterminados. Si un inicio de sesión es miembro de más de una clase de recurso, la clase más grande tiene prioridad.  
  
Las asignaciones de recursos se muestran en [administración de cargas de trabajo](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Los recursos de sistema asignados a una solicitud de cambio
Describe cómo averiguar qué recursos de clase de una solicitud de PDW de SQL Server se ejecuta en y, a continuación, cómo cambiar los recursos del sistema para esa solicitud. Cambiar los recursos para una solicitud, es necesario cambiar la pertenencia de la clase de recurso del inicio de sesión enviando la solicitud, mediante el uso de la [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) instrucción.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Paso 1: Determinar la clase de recurso para el inicio de sesión que ejecuta la solicitud.  
Esta consulta muestra los inicios de sesión que son miembros de las pertenencias a roles de servidor de recursos (clase). Hay tres clases de recursos, **mediumrc**, **largerc**, y **xlargerc**.  
  
> [!IMPORTANT]  
> Esta consulta debe ser ejecutada por un inicio de sesión que tiene **CONTROL SERVER** permiso. Si se ha ejecutado un inicio de sesión sin **CONTROL SERVER** permiso, esta consulta solo devuelve las pertenencias a roles para el inicio de sesión actual.  
  
```sql  
SELECT l.name AS [member], r.name AS [server role]  
FROM sys.server_role_members AS rm  
JOIN sys.server_principals AS l  
  ON l.principal_id = rm.member_principal_id  
JOIN  
  sys.server_principals AS r  
  ON r.principal_id = rm.role_principal_id  
WHERE  
  l.[type] = 'S'   
  AND r.[type] = 'R'  
  AND r.[name] in ('mediumrc', 'largerc', 'xlargerc');  
GO  
```  
  
Si no hay inicios de sesión que son miembros de un rol de servidor de la clase de recurso, la tabla resultante estará vacía. En este caso, si la consulta devuelve un inicio de sesión denominado Ching, a continuación, cuando Ching envía una solicitud, la solicitud recibirán los recursos del sistema de forma predeterminada, que son menores que los recursos del sistema de clase de recurso. Si un inicio de sesión es miembro de más de una clase de recurso, la clase más grande tiene prioridad.  
  
Para obtener una lista de asignaciones de recursos para cada clase de recursos, consulte [administración de cargas de trabajo](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Paso 2: Ejecutar la solicitud en un inicio de sesión con la pertenencia de la clase de recursos distinto  
Hay dos maneras de ejecutar una solicitud con cualquier recursos del sistema de mayor o menor:  
  
-   Ejecutar la solicitud en otro inicio de sesión que sea miembro de una clase de recursos mayor o menor.  
  
-   Agregar el inicio de sesión necesario a uno de los roles de la clase de recurso. Elija esta opción con precaución; cambiar la clase de recurso para el inicio de sesión, se cambiará el nivel de recursos del sistema para todas las solicitudes enviadas por el inicio de sesión.  
  
Suponga que Ching es un miembro del rol de servidor largerc. En el ejemplo siguiente se muestra cómo agregar Ching de inicio de sesión para el rol de servidor xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching ahora es un miembro de la largerc y los roles de servidor xlargerc. Cuando Ching envía las solicitudes, las solicitudes recibirán los recursos del sistema xlargerc.  
  
En el ejemplo siguiente, se retrocede Ching al rol de servidor mediumrc.  Para cambiar a la nueva función, el inicio de sesión debe quitarla xlargerc y roles de servidor largerc y agregado a la función de servidor mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching ahora es un miembro del rol de servidor mediumrc.  En el ejemplo siguiente se cambia Ching para que los recursos del sistema de forma predeterminada para las solicitudes.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Para obtener más información acerca de cómo cambiar la pertenencia al rol de clase de recursos, consulte [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Cambiar un inicio de sesión a los recursos del sistema predeterminado para sus solicitudes
Describe cómo cambiar las asignaciones de recursos de sistema asignadas a un inicio de sesión de SQL Server PDW para los importes de forma predeterminada. 
  
Para obtener descripciones de clase de recursos, consulte [administración de cargas de trabajo](workload-management.md)  
  
Cuando un inicio de sesión no es un miembro de cualquier rol de servidor de la clase de recurso, las solicitudes enviadas por el inicio de sesión recibirá la cantidad de recursos del sistema predeterminada.  
  
Suponga que el inicio de sesión Matt actualmente es un miembro de todos los roles de servidor de clase de recursos y desea volver a tener las solicitudes de recepción únicamente los recursos de forma predeterminada.  En el ejemplo siguiente se asigna los recursos predeterminados a las solicitudes de Matt colocando su pertenencia a todas las funciones de servidor de clase de recurso tres.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Mostrar que el número de ranuras de simultaneidad necesarios para una espera de solicitud
Describe cómo averiguar el número de ranuras necesarias para una solicitud que está esperando para ejecutarse en SQL Server PDW de simultaneidad.  
  
Para obtener más información, consulte [administración de cargas de trabajo](workload-management.md).  
  
Una solicitud podría estar esperando demasiado tiempo sin que ejecuta. Uno de los métodos para solucionar problemas de la solicitud consiste en buscar el número de ranuras de la simultaneidad que necesita de la solicitud.  En el ejemplo siguiente se muestra el número de ranuras de simultaneidad necesaria para cada solicitud en espera.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Vea también  
[Administración de cargas de trabajo](workload-management.md)  
  
