---
title: Tareas de administración de cargas de trabajo - Analytics Platform System | Microsoft Docs
description: Tareas de administración de cargas de trabajo de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ea6b3785914781e73a8570c1282741f7c4b56298
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959755"
---
# <a name="workload-management-tasks-in-analytics-platform-system"></a>Tareas de administración de cargas de trabajo de Analytics Platform System
Tareas de administración de cargas de trabajo de Analytics Platform System.

## <a name="view-login-members-of-each-resource-class"></a>Ver miembros del inicio de sesión de cada clase de recursos
Describe cómo mostrar a los miembros de inicio de sesión de cada rol de servidor de la clase de recurso en PDW de SQL Server. Use esta consulta para averiguar la clase de recursos permitidos para las solicitudes enviadas por cada inicio de sesión.  
  
Para obtener descripciones de clase de recursos, consulte [administración de cargas de trabajo](workload-management.md).  
  
Esta consulta muestra la lista de pertenencia de cada clase de recurso. Hay tres clases de recursos, mediumrc, largerc y xlargerc.  
  
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
  
Si un inicio de sesión no está en la lista, sus solicitudes recibirán los recursos predeterminados. Si un inicio de sesión es miembro de más de una clase de recursos, la clase más grande tiene prioridad.  
  
Se muestran las asignaciones de recursos en [administración de cargas de trabajo](workload-management.md).  
  
## <a name="change-the-system-resources-allocated-to-a-request"></a>Los recursos de sistema asignados a una solicitud de cambio
Describe cómo averiguar qué recursos de clase de una solicitud de PDW de SQL Server se está ejecutando en y, a continuación, cómo cambiar los recursos del sistema para esa solicitud. Cambiar los recursos para una solicitud requiere cambiar la pertenencia de clase de recurso del inicio de sesión enviando la solicitud, utilizando el [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) instrucción.  
  
### <a name="step-1-determine-the-resource-class-for-the-login-running-the-request"></a>Paso 1: Determinar la clase de recurso para el inicio de sesión ejecutando la solicitud.  
Esta consulta muestra los inicios de sesión que son miembros de las pertenencias a roles de servidor clase de recurso. Existen tres clases de recursos, **mediumrc**, **largerc**, y **xlargerc**.  
  
> [!IMPORTANT]  
> Esta consulta debe ser ejecutada por un inicio de sesión que tiene **CONTROL SERVER** permiso. Si ejecuta un inicio de sesión sin **CONTROL SERVER** permiso, esta consulta solo devuelve las pertenencias a roles para el inicio de sesión actual.  
  
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
  
Si no hay ningún inicio de sesión que son miembros de un rol de servidor de la clase de recurso, la tabla resultante estará vacía. En este caso, si la consulta devuelve un inicio de sesión denominado Ching, a continuación, cuando Ching envía una solicitud, la solicitud recibirá los recursos del sistema de forma predeterminada, que son menores que los recursos del sistema de clase de recurso. Si un inicio de sesión es miembro de más de una clase de recursos, la clase más grande tiene prioridad.  
  
Para obtener una lista de asignaciones de recursos para cada clase de recursos, consulte [administración de cargas de trabajo](workload-management.md).  
  
### <a name="step-2-run-the-request-under-a-login-with-different-resource-class-membership"></a>Paso 2: Ejecutar la solicitud en un inicio de sesión con la pertenencia a la clase de recursos diferente  
Hay dos maneras de ejecutar una solicitud con ambos recursos del sistema mayor o menor:  
  
-   Ejecute la solicitud en otro inicio de sesión que sea miembro de una clase de recurso mayor o menor.  
  
-   Agregue el inicio de sesión necesario para uno de los roles de la clase de recurso. Elija esta opción con precaución; cambiar la clase de recurso para el inicio de sesión, se cambiará el nivel de recursos del sistema para todas las solicitudes enviadas por el inicio de sesión.  
  
Suponga que Ching es un miembro del rol de servidor largerc. El ejemplo siguiente muestra cómo agregar Ching de inicio de sesión al rol de servidor xlargerc.  
  
```sql  
ALTER SERVER ROLE xlargerc ADD MEMBER Ching;  
```  
  
Ching ahora es un miembro de la largerc y los roles de servidor xlargerc. Cuando Ching envía las solicitudes, las solicitudes reciben los recursos del sistema xlargerc.  
  
El siguiente ejemplo mueve Ching volver a la función de servidor mediumrc.  Para cambiar a la nueva función, el inicio de sesión debe quitarse xlargerc y roles de servidor largerc y agregado al rol de servidor mediumrc.  
  
```sql  
-- Move login Ching back to using medium system resources for requests.  
ALTER SERVER ROLE xlargerc DROP MEMBER Ching;  
ALTER SERVER ROLE largerc DROP MEMBER Ching;  
ALTER SERVER ROLE mediumrc ADD MEMBER Ching;  
```  
  
Ching ahora es un miembro del rol de servidor mediumrc.  El ejemplo siguiente cambia Ching tenga los recursos del sistema predeterminada para las solicitudes.  
  
```sql  
-- Move login Ching to use the default system resources for requests.  
ALTER SERVER ROLE mediumrc DROP MEMBER Ching;  
```  
  
Para obtener más información acerca de cómo cambiar la pertenencia al rol de clase de recursos, consulte [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md).  

## <a name="change-a-login-to-the-default-system-resources-for-its-requests"></a>Cambiar un inicio de sesión a los recursos del sistema predeterminada para sus solicitudes
Describe cómo cambiar las asignaciones de recursos del sistema asignadas a un inicio de sesión de SQL Server PDW para las cantidades de forma predeterminada. 
  
Para obtener descripciones de clase de recursos, consulte [administración de cargas de trabajo](workload-management.md)  
  
Cuando un inicio de sesión no es un miembro de cualquier rol de servidor de la clase de recursos, las solicitudes enviadas por el inicio de sesión recibirá la cantidad predeterminada de los recursos del sistema.  
  
Supongamos que el inicio de sesión Matt actualmente es un miembro de todos los roles de servidor de clase de recursos y desea volver a tener solicitudes recibir solo los recursos predeterminados.  El ejemplo siguiente asigna los recursos predeterminados a las solicitudes de Matt colocando su pertenencia de todos los roles de servidor de clase tres recursos.  
  
```sql  
--Give the requests submitted by Matt the default system resources   
--by dropping Matt from all resource class server roles.  
ALTER SERVER ROLE XLargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE LargeRC DROP MEMBER Matt;  
ALTER SERVER ROLE MediumRC DROP MEMBER Matt;  
```  
  
## <a name="display-the-number-of-concurrency-slots-needed-for-a-waiting-request"></a>Mostrar que el número de ranuras de simultaneidad es necesario para una espera de solicitud
Describe cómo averiguar el número de simultaneidad ranuras son necesarios para una solicitud que está esperando para ejecutarse en PDW de SQL Server.  
  
Para obtener más información, consulte [administración de cargas de trabajo](workload-management.md).  
  
Una solicitud podría estar esperando demasiado tiempo sin ejecuta. Una de las formas de solucionar problemas de la solicitud es mirar el número de ranuras de simultaneidad que necesita la solicitud.  El ejemplo siguiente muestra el número de espacios de simultaneidad necesarios para cada solicitud en espera.  
  
```sql  
--Display the number of concurrency slots required   
--for each request that is waiting to run.  
SELECT request_id, concurrency_slots_used AS [Slots Needed], resource_class AS [Resource Class]  
FROM sys.dm_pdw_resource_waits;  
```  
  
  
## <a name="see-also"></a>Vea también  
[Administración de cargas de trabajo](workload-management.md)  
  
