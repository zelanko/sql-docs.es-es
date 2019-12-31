---
title: Tareas de administración de cargas de trabajo
description: Tareas de administración de cargas de trabajo en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 88d95eb0a2e0805930cb5f01f5af05b8fc6b3f2e
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399413"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Tareas de administración de cargas de trabajo en Analytics Platform System
Tareas de administración de cargas de trabajo en Analytics Platform System.

## <a name="view-login-members-of-each-resource-class"></a>Ver los miembros de inicio de sesión de cada clase de recurso
Describe cómo mostrar los miembros de inicio de sesión de cada rol de servidor de clase de recurso en PDW de SQL Server. Utilice esta consulta para averiguar la clase de recursos permitidos para las solicitudes enviadas por cada inicio de sesión.  
  
Para obtener descripciones de clases de recursos, consulte [Administración de cargas de trabajo](workload-management.md).  
  
Esta consulta muestra la lista de miembros de cada clase de recurso. Hay tres clases de recursos, mediumrc, largerc y xlargerc.  
  
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
  
Las asignaciones de recursos se enumeran en [Administración de cargas de trabajo](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Cambiar los recursos del sistema asignados a una solicitud
Describe cómo averiguar en qué clase de recursos se está ejecutando una solicitud de PDW de SQL Server y, a continuación, cómo cambiar los recursos del sistema para esa solicitud. Para cambiar los recursos de una solicitud, es necesario cambiar la pertenencia a la clase de recurso del inicio de sesión que envía la solicitud mediante la instrucción [ALTER Server role](../t-sql/statements/alter-server-role-transact-sql.md) .  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Paso 1: determinar la clase de recursos para el inicio de sesión que ejecuta la solicitud.  
Esta consulta muestra los inicios de sesión que son miembros de las pertenencias a roles de servidor de clase de recurso. Hay tres clases de recursos, **mediumrc**, **largerc**y **xlargerc**.  
  
> [!IMPORTANT]  
> Esta consulta debe ejecutarse mediante un inicio de sesión que tenga el permiso **Control Server** . Si la ejecuta un inicio de sesión sin el permiso **Control Server** , esta consulta solo devuelve las pertenencias a roles del inicio de sesión actual.  
  
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
  
Si no hay inicios de sesión que sean miembros de un rol de servidor de clase de recurso, la tabla resultante estará vacía. En este caso, si la consulta devuelve un inicio de sesión denominado Ching, cuando Ching envíe una solicitud, la solicitud recibirá los recursos del sistema predeterminados, que son más pequeños que los recursos del sistema de la clase de recursos. Si un inicio de sesión es miembro de más de una clase de recurso, la clase más grande tiene prioridad.  
  
Para obtener una lista de las asignaciones de recursos para cada clase de recurso, consulte [Administración de cargas de trabajo](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Paso 2: ejecutar la solicitud en un inicio de sesión con una pertenencia a clase de recurso diferente  
Hay dos maneras de ejecutar una solicitud con recursos del sistema más grandes o más pequeños:  
  
-   Ejecute la solicitud en un inicio de sesión diferente que sea miembro de una clase de recursos mayor o menor.  
  
-   Agregue el inicio de sesión necesario a uno de los roles de clase de recurso. Elija esta opción con precaución; al cambiar la clase de recursos para el inicio de sesión, se cambiará el nivel de recursos del sistema para todas las solicitudes enviadas por el inicio de sesión.  
  
Supongamos que Ching es un miembro del rol de servidor largerc. En el ejemplo siguiente se muestra cómo agregar el inicio de sesión Ching al rol de servidor xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching es ahora miembro de los roles de servidor largerc y xlargerc. Cuando Ching envía solicitudes, las solicitudes recibirán los recursos del sistema de xlargerc.  
  
En el ejemplo siguiente se mueve Ching al rol de servidor mediumrc.  Para cambiar al nuevo rol, el inicio de sesión se debe quitar de xlargerc y de los roles de servidor largerc, y se puede Agregar al rol de servidor mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching es ahora miembro del rol de servidor mediumrc.  En el ejemplo siguiente se cambia Ching para que tenga los recursos del sistema predeterminados para las solicitudes.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Para obtener más información sobre cómo cambiar la pertenencia al rol de clase de recurso, consulte [ALTER Server role](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Cambiar un inicio de sesión a los recursos del sistema predeterminados para sus solicitudes
Describe cómo cambiar las asignaciones de recursos del sistema asignadas a un inicio de sesión de PDW de SQL Server a los importes predeterminados. 
  
Para obtener descripciones de clases de recursos, consulte [Administración de cargas de trabajo](workload-management.md)  
  
Cuando un inicio de sesión no es miembro de ningún rol de servidor de clase de recurso, las solicitudes enviadas por el inicio de sesión recibirán la cantidad predeterminada de recursos del sistema.  
  
Supongamos que el inicio de sesión Matt es actualmente miembro de todos los roles de servidor de clase de recurso y desea revertir a que las solicitudes reciban solo los recursos predeterminados.  En el ejemplo siguiente se asignan los recursos predeterminados a las solicitudes de Matt quitando su pertenencia de los tres roles de servidor de clase de recurso.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Mostrar el número de espacios de simultaneidad necesarios para una solicitud en espera
Describe cómo averiguar el número de espacios de simultaneidad que necesita una solicitud que está a la espera de ejecutarse en PDW de SQL Server.  
  
Para obtener más información, consulte [Administración de cargas de trabajo](workload-management.md).  
  
Una solicitud puede estar esperando demasiado tiempo sin ejecutarse. Una de las formas de solucionar problemas de la solicitud es examinar el número de ranuras de simultaneidad que necesita la solicitud.  En el ejemplo siguiente se muestra el número de espacios de simultaneidad necesarios para cada solicitud en espera.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Véase también  
[Administración de cargas de trabajo](workload-management.md)  
  
