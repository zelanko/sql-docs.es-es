---
title: Los permisos en el almacenamiento de datos paralelos | Microsoft Docs
description: En este artículo se describe los requisitos y opciones para administrar permisos de base de datos para el almacenamiento de datos paralelos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639522"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Administrar permisos en el almacenamiento de datos paralelos
En este artículo se describe los requisitos y opciones para administrar permisos de base de datos de SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Conceptos básicos de permiso de motor de base de datos  
Los permisos del motor de base de datos en PDW de SQL Server se administran en el nivel de servidor a través de los inicios de sesión y en el nivel de base de datos a través de los usuarios de base de datos y roles de base de datos definido por el usuario.  
  
**Inicios de sesión**  
Los inicios de sesión son cuentas de usuario individuales para iniciar sesión en el PDW de SQL Server. PDW de SQL Server es compatible con los inicios de sesión mediante la autenticación de autenticación de Windows y SQL Server.  Los inicios de sesión de autenticación de Windows pueden ser usuarios de Windows o grupos de Windows de cualquier dominio de confianza para PDW de SQL Server. Inicios de sesión de autenticación de SQL Server se definen y se autentica con PDW de SQL Server y debe crearse mediante la especificación de una contraseña.  
  
Los miembros de la **sysadmin** rol fijo de servidor (como el **sa** inicio de sesión) puede conectarse a una base de datos sin tener que se asigna a un usuario de base de datos. Se asignan a la **dbo** usuario. El propietario de la base de datos también se asigna como el **dbo** usuario.  
  
**Roles de servidor**  
Hay cuatro funciones especiales de servidor con un conjunto de roles preconfigurados que proporcionan un práctico grupo de permisos de nivel de servidor. El **sysadmin**, **MediumRC**, **LargeRC**, y **XLargeRCfixed** roles de servidor son los roles de servidor solo implementados actualmente en SQL Servidor de PDW. El **sa** inicio de sesión es el único miembro de la **sysadmin** rol fijo de servidor y los inicios de sesión adicionales no pueden agregarse a la **sysadmin** rol. Los inicios de sesión se pueden conceder el **CONTROL SERVER** permiso, que es similar, aunque no idéntico, al **sysadmin** rol fijo de servidor. Use [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) para agregar miembros a los roles de servidor. PDW de SQL Server no admite roles de servidor definido por el usuario.  
  
**Usuarios de base de datos**  
Los inicios de sesión tienen acceso a una base de datos mediante la creación de un usuario de base de datos en una base de datos y asignar ese usuario de base de datos a un inicio de sesión. Normalmente, el nombre de usuario de base de datos es el mismo que el nombre de inicio de sesión, aunque no tiene por qué ser así en todos los casos. Cada usuario de base de datos se asigna a un inicio de sesión único. Un inicio de sesión se puede asignar a un único usuario en una base de datos, pero se puede asignar como usuario de base de datos en distintas bases de datos.  
  
**Roles fijos de base de datos**  
Roles fijos de base de datos son un conjunto de roles preconfigurados que proporcionan un práctico grupo de permisos de nivel de base de datos. Los usuarios de base de datos y roles de base de datos definido por el usuario se pueden agregar a los roles fijos de base de datos mediante el [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) procedimiento. Para obtener más información acerca de los roles fijos de base de datos, vea [Roles fijos de base de datos](#fixed-database-roles).  
  
**Roles de base de datos definido por el usuario**  
Los usuarios con el **CREATE ROLE** permiso puede crear nuevos roles de base de datos definido por el usuario para representar grupos de usuarios con permisos comunes. Normalmente, los permisos se conceden o deniegan a todo el rol, lo que simplifica la administración y supervisión de permisos.  
  
Los permisos se conceden a entidades de seguridad (inicios de sesión, usuarios y roles) mediante el uso de la **GRANT** instrucción. Los permisos se deniegan explícitamente mediante el **DENY** comando. Se quita un previamente concedido o denegado el permiso utilizando la **REVOCAR** instrucción. Los permisos son acumulativos, de modo que el usuario recibe todos los permisos concedidos al usuario, al inicio de sesión y a cualquier pertenencia a algún grupo. Sin embargo, las denegaciones de permisos invalidan todas las concesiones. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
En el ejemplo siguiente se muestra un método común y recomendado para la configuración de permisos.  
  
1.  Si utiliza la autenticación de Windows, cree un inicio de sesión para cada usuario de Windows o un grupo de Windows que se conectan a SQL Server PDW. Si usa la autenticación de SQL Server, cree un inicio de sesión para cada persona que se conectará a SQL Server PDW.  
  
2.  Cree un usuario de base de datos para cada inicio de sesión en todas las bases de datos necesarias.  
  
3.  Crear uno o varios roles de base de datos definido por el usuario, cada uno de los cuales representa una función similar. Por ejemplo, analista financiero y analista de ventas.  
  
4.  Agregar usuarios de base de datos a uno o varios roles de base de datos definido por el usuario.  
  
5.  Conceda permisos a los roles de base de datos definidos por el usuario.  
  
Inicios de sesión son objetos de nivel de servidor y se pueden enumerar mediante la visualización [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Permisos de nivel de servidor solo pueden concederse a las entidades de seguridad del servidor.  
  
Los usuarios y roles de base de datos son objetos de nivel de base de datos y se pueden enumerar mediante la visualización [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Solo se pueden conceder permisos de nivel de base de datos a entidades de seguridad de base de datos.  
  
## <a name="BackupTypes"></a>Permisos predeterminados  
En la lista siguiente se describen los permisos predeterminados:  
  
-   Cuando se crea un inicio de sesión mediante instrucciones using **CREATE LOGIN** instrucción, el inicio de sesión recibe el **CONNECT SQL** permiso Permitir el inicio de sesión para conectarse a SQL Server PDW.  
  
-   Cuando se crea un usuario de base de datos mediante el uso de la **CREATE USER** instrucción, el usuario recibe la **CONNECT ON DATABASE::** _< database_name >_ permiso, lo que permite el inicio de sesión para conectarse a esa base de datos como un usuario.  
  
-   Todas las entidades, incluida la función pública, no tengan ningún permiso explícito o implícito de forma predeterminada porque se heredan permisos implícitos de los permisos explícitos. Por lo tanto, cuando no hay ningún permiso explícito, también no puede haber ningún permiso implícito.  
  
-   Cuando un inicio de sesión se convierte en el propietario de un objeto o la base de datos, el inicio de sesión siempre tiene todos los permisos en el objeto o la base de datos. Los permisos de propiedad no están visibles como permisos explícitos. El **GRANT**, **REVOCAR**, y **DENY** instrucciones no tienen ningún efecto sobre los permisos de la propiedad. La propiedad se puede cambiar mediante la [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) instrucción.  
  
-   Inicio de sesión sa tiene todos los permisos en el dispositivo. Al igual que los permisos de propiedad, los permisos de sa no se puede cambiar y no están visibles como permisos explícitos. El **GRANT**, **REVOCAR**, y **DENY** instrucciones no tienen ningún efecto sobre los permisos de sa.  
  
-   El rol de servidor público no recibe ningún permiso de forma predeterminada y no hereda los permisos de otros roles de servidor. El rol de servidor público puede tener concedido permisos explícitos con el **GRANT**, **REVOCAR**, y **DENY** instrucciones.  
  
-   Las transacciones no requieren permisos. Pueden ejecutar todas las entidades del **BEGIN TRANSACTION**, **confirmar**, y **reversión** comandos de transacción. Sin embargo, una entidad de seguridad debe tener los permisos adecuados para ejecutar cada instrucción dentro de la transacción.  
  
-   La instrucción **USE** no requiere permisos. Pueden ejecutar todas las entidades del **USE** instrucción en cualquier base de datos, sin embargo, para tener acceso a una base de datos deben tener una entidad de seguridad del usuario en la base de datos o el usuario invitado debe estar habilitado.  
  
### <a name="the-public-role"></a>La función pública  
Todos los nuevos inicios de sesión de dispositivo automáticamente pertenecen al rol PUBLIC. El rol de servidor PUBLIC tiene las siguientes características:  
  
-   El rol de servidor público no tiene permisos de forma predeterminada.  
  
-   Todas las entidades son miembros del rol de servidor público y el rol de servidor público no es un miembro de otro rol de servidor.  
  
-   El rol de servidor público no puede heredar permisos implícitos. Se deben conceder explícitamente los permisos otorgados a la función PUBLIC.  
  
## <a name="BackupProc"></a>Determinar los permisos  
Si un inicio de sesión tiene permiso para realizar una acción específica depende de los permisos concedidos o denegados al inicio de sesión, usuarios y roles de de que usuario es miembro. Permisos de nivel de servidor (como **CREATE LOGIN** y **VIEW SERVER STATE**) están disponibles para las entidades de seguridad de nivel de servidor (inicios de sesión). Permisos de nivel de base de datos (como **seleccione** de una tabla o **EXECUTE** en un procedimiento) están disponibles para las entidades de seguridad de nivel de base de datos (usuarios y roles de base de datos).  
  
### <a name="implicit-and-explicit-permissions"></a>Permisos implícitos y explícitos  
Un *permiso explícito* es un permiso **GRANT** o **DENY** concedido a una entidad de seguridad mediante una instrucción **GRANT** o **DENY**. Permisos de nivel de base de datos se muestran en el [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) vista. Permisos de nivel de servidor se muestran en el [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista.  
  
Un *permiso implícito* es un **GRANT** o **DENY** permiso que ha heredado una entidad de seguridad (rol de servidor o de inicio de sesión). Un permiso se puede heredar de las maneras siguientes.  
  
-   Una entidad de seguridad puede heredar un permiso de una función de si la entidad de seguridad es un miembro del rol, incluso si la entidad de seguridad no tiene una explícita **GRANT** o **DENY** permiso.  
  
-   Una entidad de seguridad puede heredar un permiso en un objeto subordinado (por ejemplo, una tabla) si la entidad de seguridad tiene un permiso en uno de los ámbitos de los objetos primarios (por ejemplo, el esquema de la tabla o el permiso en toda la base de datos).  
  
-   Una entidad de seguridad puede heredar un permiso al tener un permiso que incluya un permiso subordinado. Por ejemplo el **ALTER ANY USER** permiso incluye tanto el **CREATE USER** y **ALTER ON USER::** _<name>_ permisos.  
  
### <a name="determining-permissions-when-performing-actions"></a>Determinar los permisos al realizar acciones  
El proceso de determinar qué permiso para asignar a una entidad de seguridad es complejo. Se produce la complejidad al determinar permisos implícitos porque las entidades de seguridad pueden ser miembros de varios roles y permisos se pueden pasar a través de varios niveles en la jerarquía de roles.  
  
En la lista siguiente describe las reglas generales para determinar los permisos:  
  
-   La propiedad implica el permiso.  
  
    Un propietario del objeto tiene todos los permisos en el objeto. Del mismo modo, un propietario de la base de datos tiene todos los permisos en la base de datos y todos los permisos en los objetos en la base de datos. No se puede cambiar estos permisos.  
  
-   Se pueden heredar permisos en varios niveles de la jerarquía de las pertenencias a roles de servidor.  
  
    Por ejemplo, suponga que tiene la siguiente situación:  
  
    -   David de inicio de sesión es miembro del rol de base de datos PerfAnalysts.  
  
    -   PerfAnalysts es un miembro del rol de base de datos producción.  
  
    -   David y PerfAnalysts no tienen **seleccione** permiso en la tabla Customer. El permiso se revoca o concede nunca de forma explícita.  
  
    -   Producción tiene **seleccione** permiso en la tabla Customer.  
  
    En este caso, heredará PerfAnalysts **GRANT** heredarán los permisos en la tabla Customer de producción y David **GRANT** permiso en la tabla Customer de producción.  
  
-   **DENEGAR** invalida **GRANT** cuando entran en conflicto permisos.  
  
    Por ejemplo, suponga que David de inicio de sesión no tiene permisos en la tabla Customer y es un miembro de dos roles de base de datos-dbgroup1, que tiene **DENY** permiso en la tabla Customer y dbgroup2, que tiene **GRANT** permiso en la tabla Customer. En este caso, David heredará el **DENY** permiso en la tabla Customer. Esto sucede si los roles adquirida sus permisos, implícita o explícita.  
  
### <a name="auditing-permissions"></a>Permisos de auditoría  
Para obtener información sobre los permisos de un usuario, compruebe lo siguiente.  
  
-   Ejecute la siguiente consulta para determinar qué inicios de sesión son administradores del sistema.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Ejecute la siguiente consulta para determinar qué inicios de sesión han concedido permisos explícitos.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Ejecute la siguiente consulta en una base de datos de usuario para determinar qué usuarios de base de datos son miembros de un rol de base de datos.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Ejecute la siguiente consulta en una base de datos de usuario para determinar qué usuarios de base de datos y funciones se han concedido o denegado permisos específicos. Tendrá que las vistas de consulta adicionales, como sys.objects y sys.schemas para identificar los elementos descritos con el major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Procedimientos recomendados de los permisos de base de datos  
  
-   Conceder permisos de nivel más granular que sea práctico. Podrían dificultar la concesión de permisos en la tabla o permisos de nivel de vista. Pero la concesión de permisos en el nivel de base de datos podría ser demasiado permisiva. Si la base de datos está diseñada con esquemas para definir los límites de trabajo, quizás el conceder un permiso en el esquema es un equilibrio adecuado entre el nivel de tabla y el nivel de base de datos.  
  
-   Conceder permisos a roles, en lugar de a usuarios o inicios de sesión. Administración de derechos mediante el uso de roles en lugar de usuarios facilita la rápidamente conceder o revocar un conjunto de permisos para un usuario o inicio de sesión por moverlas dentro o fuera de la función. Cuando se pasa una función de una persona a otra, los permisos pueden permanecen intactos en el nivel de rol mientras los cambios de pertenencia al rol.  
  
-   Conceder permisos a los roles según la función de su trabajo y roles del grupo de nivel superior que se combinan los roles de la función de trabajo basados en el grupo de la empresa realiza las acciones.  
  
-   Todos los usuarios finales deben tener un inicio de sesión único. No permitir a los usuarios compartir inicios de sesión. Proporcionar un inicio de sesión para cada usuario garantiza una pista de auditoría y simplifica la administración de permisos.  
  
## <a name="fixed-database-roles"></a>Roles fijos de base de datos
SQL Server proporciona roles de nivel de base de datos (fijos) preconfigurados para ayudarle a administrar los permisos en un servidor. Los roles preconfigurados son fijos en que no se puede cambiar los permisos asignados a ellos. También se pueden crear roles de base de datos definido por el usuario. Puede cambiar los permisos asignados a roles de base de datos definido por el usuario.  
  
Roles son entidades de seguridad que agrupan otras entidades de seguridad. Roles de base de datos son toda la base de datos en su ámbito de permisos. Los usuarios de base de datos y otros roles de base de datos se pueden agregar como miembros de roles de base de datos. No se puede agregar los roles fijos de base de datos entre sí. (Los*roles* son como los *grupos* del sistema operativo Windows).  
  
Hay 9 roles fijos de base de datos.  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>Permisos de los Roles fijos de base de datos  
El sistema de roles fijos de servidor y los roles fijos de base de datos es un sistema heredado que se originó en los años 80. Roles fijos son todavía compatibles y son útiles en entornos donde hay pocos usuarios y las necesidades de seguridad son sencillas. A partir de SQL Server 2005, se creó un sistema más detallado de cómo conceder permiso. Este nuevo sistema es más granular, que proporciona muchas más opciones para otorgar y denegar permisos. La complejidad adicional del sistema más granular de hace más difícil aprender, pero la mayoría de los sistemas de empresa deben conceder permisos en lugar de usar los roles fijos. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->El gráfico siguiente muestra los permisos que están asociados con cada rol fijo de base de datos. Todos los permisos en este gráfico de SQL Server no están disponibles (o necesario) los puntos de acceso.  
  
![Funciones fijas de base de datos de seguridad de APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Contenido relacionado  
  
-   Para crear funciones definidas por el usuario, consulte [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Roles fijos de servidor
SQL Server crea automáticamente los roles fijos de servidor. PDW de SQL Server tiene una implementación limitada de roles fijos de servidor de SQL Server. Solo el **sysadmin** y **pública** tener inicios de sesión de usuario como miembros. El **setupadmin** y **dbcreator** roles usados internamente por SQL Server PDW. Miembros adicionales no se agregan o quitan de ningún rol.  
  
### <a name="sysadmin-fixed-server-role"></a>función sysadmin rol fijo de servidor  
Los miembros del rol fijo de servidor **sysadmin** pueden realizar cualquier actividad en el servidor. El **sa** inicio de sesión es el único miembro de la **sysadmin** rol fijo de servidor. No se pueden agregar inicios de sesión adicionales para el **sysadmin** rol fijo de servidor. La concesión del permiso **CONTROL SERVER** es similar a la pertenencia al rol fijo de servidor **sysadmin**. El siguiente ejemplo se concede el **CONTROL SERVER** permiso para un inicio de sesión denominado Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> El **CONTROL SERVER** permiso proporciona control casi completado de SQL Server PDW. Siempre que sea posible, proporcionar permisos más granulares a inicios de sesión en su lugar. Por ejemplo, considere la posibilidad de conceder la **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, o **CREATE ANY DATABASE** permisos.  
  
### <a name="public-server-role"></a>Rol de servidor Public  
Cada inicio de sesión que puede conectarse a SQL Server PDW es un miembro de la **pública** rol de servidor. Todos los inicios de sesión heredan los permisos concedidos a **pública** en cualquier objeto. Solo puede asignar **pública** permisos en un objeto cuando desee que el objeto esté disponible para todos los usuarios. No se puede cambiar la pertenencia en el **pública** rol.  
  
> [!NOTE]  
> **pública** se implementa de manera diferente que otros roles. Dado que todas las entidades de seguridad de servidor son miembros del público, la pertenencia de la **pública** rol no aparece en el **sys.server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Vs de Roles de servidor fijos. La concesión de permisos  
El sistema de roles fijos de servidor y los roles fijos de base de datos es un sistema heredado que se originó en los años 80. Roles fijos son todavía compatibles y son útiles en entornos donde hay pocos usuarios y las necesidades de seguridad son sencillas. A partir de SQL Server 2005, se creó un sistema más detallado de cómo conceder permiso. Este nuevo sistema es más granular, que proporciona muchas más opciones para otorgar y denegar permisos. La complejidad adicional del sistema más granular de hace más difícil aprender, pero la mayoría de los sistemas de empresa deben conceder permisos en lugar de usar los roles fijos. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Temas relacionados  
  
- [Conceder permisos](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

