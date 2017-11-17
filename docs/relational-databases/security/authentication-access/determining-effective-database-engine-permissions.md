---
title: Determinar los permisos efectivos del motor de base de datos | Microsoft Docs
ms.custom: 
ms.date: 01/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions, effective
- effective permissions
ms.assetid: 273ea09d-60ee-47f5-8828-8bdc7a3c3529
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d21efb4495f786b6000fe0b8675fa042b4d2ca6e
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="determining-effective-database-engine-permissions"></a>Determinar los permisos efectivos del motor de base de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este tema se describe cómo determinar quién tiene permisos para varios objetos en el motor de base de datos de SQL Server. SQL Server implementa dos sistemas de permisos para el motor de base de datos. Un sistema anterior de roles fijos tiene permisos preconfigurados. A partir de SQL Server 2005 está disponible un sistema más flexible y preciso. (La información de este tema también es aplicable a SQL Server, a partir de la versión 2005. Ciertos tipos de permisos no están disponibles en algunas versiones de SQL Server).

>  [!IMPORTANT] 
>  * Los permisos efectivos son la suma de ambos sistemas de permiso. 
>  * Una denegación de permisos invalida una concesión de permisos. 
>  * Si un usuario es miembro del rol fijo de servidor sysadmin, los permisos no se comprueban más, por lo que no se aplicarán las denegaciones. 
>  * El sistema antiguo y el nuevo sistema tienen similitudes. Por ejemplo, la pertenencia al rol fijo de servidor `sysadmin` es similar a tener el permiso `CONTROL SERVER`. Pero los sistemas no son idénticos. Por ejemplo, si un inicio de sesión solo tiene el permiso `CONTROL SERVER` y un procedimiento almacenado comprueba la pertenencia en el rol fijo de servidor `sysadmin`, se producirá un error en la comprobación del permiso. Lo contrario también es cierto. 


## <a name="summary"></a>Resumen   
* El permiso de nivel de servidor puede proceder de la pertenencia a roles fijos de servidor o roles de servidor definidos por el usuario. Todos pertenecen al rol fijo de servidor `public` y reciben cualquier permiso asignado allí.   
* Los permisos de nivel de servidor pueden proceder de concesiones de permisos a inicios de sesión o roles de servidor definidos por el usuario.   
* Los permisos de nivel de base de datos pueden proceder de la pertenencia a los roles de base de datos fijos o a roles de base de datos definidos por el usuario en cada base de datos. Todos pertenecen al rol fijo de base de datos `public` y reciben cualquier permiso asignado allí.   
* Los permisos de nivel de base de datos pueden proceder de concesiones de permisos a usuarios o a roles de base de datos definidos por el usuario en cada base de datos.   
* Los permisos se pueden recibir desde el inicio de sesión `guest` o el usuario de base de datos `guest` si están habilitados. El inicio de sesión y los usuarios `guest` están deshabilitados de forma predeterminada.   
* Los usuarios de Windows pueden ser miembros de grupos de Windows que pueden tener inicios de sesión. SQL Server detecta la pertenencia a grupos de Windows cuando un usuario de Windows se conecta y presenta un token de Windows con el identificador de seguridad de un grupo de Windows. Como SQL Server no administra ni recibe actualizaciones automáticas sobre la pertenencia a grupos de Windows, SQL Server no puede informar de forma confiable de los permisos de usuarios de Windows que se reciben de la pertenencia a grupos de Windows.   
* Los permisos se pueden adquirir cambiando a un rol de aplicación y proporcionando la contraseña.   
* Los permisos se pueden adquirir mediante la ejecución de un procedimiento almacenado que incluya la cláusula `EXECUTE AS`.   
* Los permisos se pueden adquirir por los inicios de sesión o los usuarios con el permiso `IMPERSONATE`.   
* Los miembros del grupo de administradores del equipo local siempre pueden elevar sus privilegios a `sysadmin`. (No se aplica a SQL Database).  
* Los miembros del rol fijo de servidor `securityadmin` pueden elevar muchos de sus privilegios y en algunos casos pueden elevar los privilegios a `sysadmin`. (No se aplica a SQL Database).   
* Los administradores de SQL Server pueden ver información sobre todos los inicios de sesión y usuarios. Los usuarios con menos privilegios normalmente solo ven información sobre sus propias identidades.

## <a name="older-fixed-role-permission-system"></a>Sistema anterior de permisos de rol fijo

Los roles fijos de servidor y los roles fijos de base de datos tienen permisos preconfigurados que no se pueden cambiar. Para determinar quién es miembro del rol fijo de servidor, ejecute la consulta siguiente.    
>  [!NOTE] 
>  No se aplica a SQL Database ni SQL Data Warehouse, donde los permisos de nivel de servidor no están disponibles. La columna `is_fixed_role` de `sys.server_principals` se agregó en SQL Server 2012. No es necesaria para las versiones anteriores de SQL Server.  
```tsql
SELECT SP1.name AS ServerRoleName, 
 isnull (SP2.name, 'No members') AS LoginName   
 FROM sys.server_role_members AS SRM
 RIGHT OUTER JOIN sys.server_principals AS SP1
   ON SRM.role_principal_id = SP1.principal_id
 LEFT OUTER JOIN sys.server_principals AS SP2
   ON SRM.member_principal_id = SP2.principal_id
 WHERE SP1.is_fixed_role = 1 -- Remove for SQL Server 2008
 ORDER BY SP1.name;
```
>  [!NOTE] 
>  * Todos los inicios de sesión son miembros del rol público y no se pueden quitar. 
>  * Esta consulta comprueba las tablas en la base de datos maestra, pero se puede ejecutar en cualquier base de datos para el producto local. 

Para determinar quién es miembro de un rol fijo de base de datos, ejecute la consulta siguiente en todas las bases de datos.
```tsql
SELECT DP1.name AS DatabaseRoleName, 
   isnull (DP2.name, 'No members') AS DatabaseUserName 
 FROM sys.database_role_members AS DRM
 RIGHT OUTER JOIN sys.database_principals AS DP1
   ON DRM.role_principal_id = DP1.principal_id
 LEFT OUTER JOIN sys.database_principals AS DP2
   ON DRM.member_principal_id = DP2.principal_id
 WHERE DP1.is_fixed_role = 1
 ORDER BY DP1.name;
```
Para comprender los permisos concedidos a cada rol, vea las descripciones de roles en las ilustraciones en Libros en pantalla ([Server-Level Roles](../../../relational-databases/security/authentication-access/server-level-roles.md) (Roles de nivel de servidor) y [Database-Level Roles](../../../relational-databases/security/authentication-access/database-level-roles.md) (Roles de nivel de base de datos)).

## <a name="newer-granular-permission-system"></a>Sistema de permisos granulares más reciente

Este sistema es muy flexible, lo que significa que puede ser complicado si los usuarios que lo configuran quieren que sea muy preciso. Eso no es necesariamente algo negativo; espero que mi entidad financiera sea precisa. Para simplificar las cosas, ayuda a crear roles, asignar permisos a roles y, después, agregar los grupos de usuarios a los roles. Y es más fácil si el equipo de desarrollo de base de datos separa la actividad por esquemas y, después, concede permisos de rol a un esquema completo en lugar de a procedimientos o tablas individuales. Pero la realidad es compleja y hay que asumir que las necesidades empresariales crean requisitos de seguridad inesperados.   

El gráfico siguiente muestra los permisos y las relaciones entre ellos. Algunos de los permisos de nivel superior (como `CONTROL SERVER`) se muestran varias veces. En este tema, el póster es demasiado pequeño para leerlo. Haga clic en la imagen para descargar el **Póster de permisos del motor de base de datos** en formato pdf.  
  
 [![Permisos de motor de base de datos](../../../relational-databases/security/media/database-engine-permissions.PNG)](http://go.microsoft.com/fwlink/?LinkId=229142)

### <a name="security-classes"></a>Clases Security

Los permisos se pueden conceder en el nivel de servidor, el nivel de base de datos, el nivel de esquema o el nivel de objeto, etc. Hay 26 niveles (denominados clases). La lista completa de clases en orden alfabético es: `APPLICATION ROLE`, `ASSEMBLY`, `ASYMMETRIC KEY`, `AVAILABILITY GROUP`, `CERTIFICATE`, `CONTRACT`, `DATABASE`, `DATABASE` `SCOPED CREDENTIAL`, `ENDPOINT`, `FULLTEXT CATALOG`, `FULLTEXT STOPLIST`, `LOGIN`, `MESSAGE TYPE`, `OBJECT`, `REMOTE SERVICE BINDING`, `ROLE`, `ROUTE`, `SCHEMA`, `SEARCH PROPERTY LIST`, `SERVER`, `SERVER ROLE`, `SERVICE`, `SYMMETRIC KEY`, `TYPE`, `USER`, `XML SCHEMA COLLECTION`. (Algunas clases no están disponibles en algunos tipos de servidores SQL Server). Para proporcionar información completa sobre cada clase se requiere una consulta diferente.

### <a name="principals"></a>Entidades de seguridad

Los permisos se conceden a entidades de seguridad. Las entidades de seguridad pueden ser roles de servidor, inicios de sesión, roles de base de datos o usuarios. Los inicios de sesión pueden representar grupos de Windows que incluyen muchos usuarios de Windows. Dado que los grupos de Windows no se mantienen por SQL Server, SQL Server no siempre sabe quién es miembro de un grupo de Windows. Cuando un usuario de Windows se conecta a SQL Server, el paquete de inicio de sesión contiene los tokens de pertenencia a grupos de Windows para el usuario.

Cuando un usuario de Windows se conecta con un inicio de sesión basado en un grupo de Windows, es posible que algunas actividades requieran SQL Server para crear un inicio de sesión o un usuario para representar al usuario concreto de Windows. Por ejemplo, un grupo de Windows (Ingenieros) contiene usuarios (María, Luis, Juan) y el grupo Ingenieros tiene una cuenta de usuario de base de datos. Si María tiene permiso y crea una tabla, es posible que se cree un usuario (María) para que sea el propietario de la tabla. O bien, si se deniega a Luis un permiso que el resto del grupo Ingenieros tiene, entonces debe crearse el usuario Luis para realizar un seguimiento de la denegación del permiso.

Recuerde que es posible que un usuario de Windows sea miembro de más de un grupo de Windows (por ejemplo, Ingenieros y Administradores). Los permisos concedidos o denegados al inicio de sesión de Ingenieros, al inicio de sesión de Administradores, concedidos o denegados al usuario de forma individual y concedidos o denegados a los roles de los que el usuario es miembro, se agregan y se evalúan para los permisos efectivos. La función `HAS_PERMS_BY_NAME` puede mostrar si un usuario o un inicio de sesión tiene un permiso concreto. Pero no hay ninguna manera obvia de determinar el origen de la concesión o denegación del permiso. Se debe estudiar la lista de permisos y quizás experimentar mediante prueba y error.

## <a name="useful-queries"></a>Consultas útiles

### <a name="server-permissions"></a>Permisos de servidor

La consulta siguiente devuelve una lista de los permisos que se han concedido o denegado en el nivel de servidor. Esta consulta debe ejecutarse en la base de datos maestra.   
>  [!NOTE] 
>  Los permisos de nivel de servidor se no se pueden conceder ni consultar en la base de datos SQL o SQL Data Warehouse.   
```tsql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
 FROM sys.server_principals AS pr
 LEFT OUTER JOIN sys.server_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 WHERE is_fixed_role = 0 -- Remove for SQL Server 2008
 ORDER BY pr.name, type_desc;
```

### <a name="database-permissions"></a>Permisos para la base de datos

La consulta siguiente devuelve una lista de los permisos que se han concedido o denegado en el nivel de base de datos. Esta consulta debe ejecutarse en todas las bases de datos.   
```tsql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
FROM sys.database_principals AS pr
LEFT OUTER JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE pr.is_fixed_role = 0 
ORDER BY pr.name, type_desc;
```

Cada clase de permiso en la tabla de permisos puede combinarse con otras vistas del sistema que proporcionan información relacionada con esa clase de elemento protegible. Por ejemplo, la consulta siguiente proporciona el nombre del objeto de base de datos que se ve afectado por el permiso.    
```tsql
SELECT pr.type_desc, pr.name, pe.state_desc, 
 pe.permission_name, s.name + '.' + oj.name AS Object, major_id
 FROM sys.database_principals AS pr
 JOIN sys.database_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 JOIN sys.objects AS oj
   ON oj.object_id = pe.major_id
 JOIN sys.schemas AS s
   ON oj.schema_id = s.schema_id
 WHERE class_desc = 'OBJECT_OR_COLUMN';
```
Use la función `HAS_PERMS_BY_NAME` para determinar si un usuario determinado (en este caso `TestUser`) tiene un permiso. Por ejemplo:   
```tsql
EXECUTE AS USER = 'TestUser';
SELECT HAS_PERMS_BY_NAME ('dbo.T1', 'OBJECT', 'SELECT');
REVERT;
```
Para obtener detalles de la sintaxis, vea [HAS_PERMS_BY_NAME](../../../t-sql/functions/has-perms-by-name-transact-sql.md).

## <a name="see-also"></a>Ver también:

[Introducción a los permisos de los motores de bases de datos](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)    
[Tutorial: Introducción al motor de base de datos](Tutorial:%20Getting%20Started%20with%20the%20Database%20Engine.md) 


