---
title: Permisos de PDW (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e271980-bec8-424b-9f68-cea11b4e64e8
caps.latest.revision: 23
ms.openlocfilehash: 95843be163714be27e6eeb7f28825e98a5371e19
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="pdw-permissions"></a>Permisos de PDW
Este tema describe los requisitos y opciones para administrar permisos de base de datos para SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Conceptos básicos de permiso de motor de base de datos  
Permisos del motor de base de datos en SQL Server PDW se administran en el nivel de servidor mediante inicios de sesión y en el nivel de base de datos a través de los usuarios de base de datos y roles de base de datos definido por el usuario.  
  
**Inicios de sesión**  
Los inicios de sesión son cuentas de usuario individuales para iniciar sesión en SQL Server PDW. SQL Server PDW es compatible con los inicios de sesión mediante la autenticación de autenticación de Windows y SQL Server.  Los inicios de sesión de autenticación de Windows pueden ser usuarios de Windows o grupos de Windows de cualquier dominio que sea de confianza para PDW de SQL Server. Los inicios de sesión de autenticación de SQL Server se definen y autenticados por SQL Server PDW y deben crearse mediante la especificación de una contraseña.  
  
Los miembros de la **sysadmin** rol fijo de servidor (como la **sa** inicio de sesión) puede conectarse a una base de datos sin tener que se asigna a un usuario de base de datos. Se asignan a la **dbo** usuario. El propietario de la base de datos también se asigna como el **dbo** usuario.  
  
**Roles de servidor**  
Existen cuatro roles de servidor especial con un conjunto de roles preconfigurados que proporcionan un práctico grupo de permisos de nivel de servidor. El **sysadmin**, **MediumRC**, **LargeRC**, y **XLargeRCfixed** roles de servidor son los roles de servidor solo implementados actualmente en SQL Servidor PDW. El **sa** inicio de sesión es el único miembro de la **sysadmin** rol fijo de servidor y los inicios de sesión adicionales no se pueden agregar a la **sysadmin** rol. Los inicios de sesión pueden tener la **CONTROL SERVER** permiso, que es similar, aunque no idéntica, a la **sysadmin** rol fijo de servidor. Use [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) para agregar miembros a los otros roles de servidor. PDW de SQL Server no admite roles de servidor definidos por el usuario.  
  
**Usuarios de base de datos**  
Para conceder acceso a una base de datos, inicios de sesión se crea un usuario de base de datos en una base de datos y asigna ese usuario de base de datos a un inicio de sesión. Normalmente, el nombre de usuario de base de datos es el mismo que el nombre de inicio de sesión, aunque no tiene por qué ser así en todos los casos. Cada usuario de base de datos se asigna a un inicio de sesión único. Un inicio de sesión se puede asignar a un único usuario en una base de datos, pero se puede asignar como usuario de base de datos en distintas bases de datos.  
  
**Roles fijos de base de datos**  
Roles fijos de base de datos son un conjunto de roles preconfigurados que proporcionan un práctico grupo de permisos de nivel de base de datos. Los usuarios de base de datos y roles de base de datos definido por el usuario pueden agregarse a los roles fijos de base de datos mediante la [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) procedimiento. Para obtener más información acerca de los roles fijos de base de datos, vea [Roles fijos de base de datos](#fixed-database-roles).  
  
**Roles de base de datos definido por el usuario**  
Los usuarios con el **CREATE ROLE** permiso puede crear nuevos roles de base de datos definido por el usuario para representar grupos de usuarios con permisos comunes. Normalmente, los permisos se conceden o deniegan a todo el rol, lo que simplifica la administración y supervisión de permisos.  
  
Los permisos se conceden a las entidades de seguridad (inicios de sesión, usuarios y roles) mediante la **GRANT** instrucción. Los permisos se deniegan explícitamente mediante el uso de la **DENY** comando. Elimina un previamente concedido o denegado el permiso, se usa el **REVOCAR** instrucción. Los permisos son acumulativos, de modo que el usuario recibe todos los permisos concedidos al usuario, al inicio de sesión y a cualquier pertenencia a algún grupo. Sin embargo, las denegaciones de permisos invalidan todas las concesiones. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
En el ejemplo siguiente se muestra un método común y recomendado para la configuración de permisos.  
  
1.  Si utiliza la autenticación de Windows, cree un inicio de sesión para cada usuario de Windows o un grupo de Windows que se conectan a SQL Server PDW. Si utiliza autenticación de SQL Server, cree un inicio de sesión para cada persona que se conectará a SQL Server PDW.  
  
2.  Cree un usuario de base de datos para cada inicio de sesión en todas las bases de datos necesarias.  
  
3.  Crear uno o varios roles de base de datos definido por el usuario, cada uno representa una función similar. Por ejemplo, analista financiero y analista de ventas.  
  
4.  Agregar usuarios de base de datos a uno o varios roles de base de datos definido por el usuario.  
  
5.  Conceda permisos a los roles de base de datos definidos por el usuario.  
  
Inicios de sesión son objetos de nivel de servidor y puede aparecer observando [sys.server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Permisos de nivel de servidor solo pueden concederse a las entidades de seguridad de servidor.  
  
Los usuarios y roles de base de datos son objetos de nivel de base de datos y puede aparecer observando [sys.database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Solo se pueden conceder permisos de nivel de base de datos a entidades de seguridad de base de datos.  
  
## <a name="BackupTypes"></a>Permisos predeterminados  
En la lista siguiente se describen los permisos predeterminados:  
  
-   Cuando se crea un inicio de sesión mediante instrucciones using **CREATE LOGIN** (instrucción), el inicio de sesión recibe el **CONNECT SQL** permiso Permitir el inicio de sesión para conectarse a SQL Server PDW.  
  
-   Cuando se crea un usuario de base de datos mediante el uso de la **CREATE USER** (instrucción), el usuario recibe el **CONNECT ON DATABASE:: *** < database_name >* permiso, lo que permite el inicio de sesión para conectarse a esa base de datos como un usuario.  
  
-   Todas las entidades, incluida la función pública, no tengan ningún permiso explícito o implícito de forma predeterminada porque se heredan los permisos implícitos de permisos explícitos. Por lo tanto, cuando no hay ningún permiso explícito, también no puede haber ningún permiso implícito.  
  
-   Cuando un inicio de sesión se convierte en el propietario de un objeto o la base de datos, el inicio de sesión siempre tiene todos los permisos en el objeto o la base de datos. Los permisos de la propiedad no están visibles como permisos explícitos. El **GRANT**, **REVOCAR**, y **DENY** instrucciones no tienen ningún efecto en los permisos de la propiedad. La propiedad puede cambiarse mediante el [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) instrucción.  
  
-   El inicio de sesión de sa tiene todos los permisos en el dispositivo. Para los permisos de la propiedad, los permisos de sa no se puede cambiar y no están visibles como permisos explícitos. El **GRANT**, **REVOCAR**, y **DENY** instrucciones no tienen ningún efecto en los permisos de sa.  
  
-   El rol de servidor público no recibe ningún permiso de forma predeterminada y no heredan los permisos de otros roles de servidor. El rol de servidor público puede tener concedido permisos explícitos con el **GRANT**, **REVOCAR**, y **DENY** instrucciones.  
  
-   Las transacciones no requieren permisos. Pueden ejecutar todas las entidades del **BEGIN TRANSACTION**, **confirmar**, y **reversión** comandos de transacción. Sin embargo, una entidad de seguridad debe tener los permisos adecuados para ejecutar cada instrucción dentro de la transacción.  
  
-   La instrucción **USE** no requiere permisos. Pueden ejecutar todas las entidades del **USE** instrucción en cualquier base de datos, sin embargo, para tener acceso a una base de datos deben tener una entidad de seguridad de usuario en la base de datos o el usuario invitado debe estar habilitado.  
  
### <a name="the-public-role"></a>La función PUBLIC  
Todos los nuevos inicios de sesión de dispositivo automáticamente pertenecen a la función PUBLIC. El rol de servidor PUBLIC tiene las siguientes características:  
  
-   El rol de servidor público no tiene permisos de forma predeterminada.  
  
-   Todas las entidades son miembros del rol de servidor público y el rol de servidor público no es un miembro de otro rol de servidor.  
  
-   El rol de servidor público no puede heredar permisos implícitos. Los permisos concedidos a la función PUBLIC se deben conceder explícitamente.  
  
## <a name="BackupProc"></a>Determinar los permisos  
Si un inicio de sesión tiene permiso para realizar una acción concreta depende de los permisos concedidos o denegados para inicio de sesión, usuarios y roles de de que usuario es miembro. Permisos de nivel de servidor (como **CREATE LOGIN** y **VIEW SERVER STATE**) están disponibles para las entidades de seguridad de nivel de servidor (inicios de sesión). Permisos de nivel de base de datos (como **seleccione** de una tabla o **EXECUTE** en un procedimiento) están disponibles para las entidades de seguridad de nivel de base de datos (usuarios y roles de base de datos).  
  
### <a name="implicit-and-explicit-permissions"></a>Permisos implícitos y explícitos  
Un *permiso explícito* es un permiso **GRANT** o **DENY** concedido a una entidad de seguridad mediante una instrucción **GRANT** o **DENY**. Permisos de nivel de base de datos se muestran en la [sys.database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) vista. Permisos de nivel de servidor se muestran en la [sys.server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) vista.  
  
Un *permiso implícito* es un **GRANT** o **DENY** permiso que se ha heredado una entidad de seguridad (rol de servidor o inicio de sesión). Un permiso se puede heredar de las maneras siguientes.  
  
-   Una entidad de seguridad puede heredar un permiso de una función de si la entidad de seguridad es un miembro de la función incluso si la entidad de seguridad no tiene una explícita **GRANT** o **DENY** permiso.  
  
-   Una entidad de seguridad puede heredar un permiso en un objeto subordinado (por ejemplo, una tabla) si la entidad de seguridad tiene un permiso en uno de los ámbitos de elemento primario de objetos (por ejemplo, el esquema de la tabla o el permiso en la base de datos completa).  
  
-   Una entidad de seguridad puede heredar un permiso al tener un permiso que incluya un permiso subordinado. Por ejemplo la **ALTER ANY USER** permiso incluye tanto el **CREATE USER** y **ALTER ON USER:: ***<name>*  permisos.  
  
### <a name="determining-permissions-when-performing-actions"></a>Determinar los permisos al realizar acciones  
El proceso de determinar qué permiso para asignar a una entidad de seguridad es complejo. Se produce la complejidad al determinar permisos implícitos porque las entidades de seguridad pueden ser miembros de varios roles y permisos se pueden pasar a través de varios niveles en la jerarquía de roles.  
  
En la lista siguiente describe las reglas generales para determinar los permisos:  
  
-   La propiedad implica el permiso.  
  
    Un propietario del objeto tiene todos los permisos en el objeto. Del mismo modo, un propietario de base de datos tiene todos los permisos en la base de datos y todos los permisos en los objetos en la base de datos. No se puede cambiar estos permisos.  
  
-   Se pueden heredar permisos a través de varios niveles en la jerarquía de miembros de la función de servidor.  
  
    Por ejemplo, suponga que tiene la siguiente situación:  
  
    -   David de inicio de sesión es miembro del rol de base de datos PerfAnalysts.  
  
    -   PerfAnalysts es un miembro del rol de base de datos producción.  
  
    -   David y PerfAnalysts no tienen ningún **seleccione** permiso en la tabla Customer. El permiso se revoca o concede nunca de forma explícita.  
  
    -   Producción tiene **seleccione** permiso en la tabla Customer.  
  
    En este caso, heredará PerfAnalysts **GRANT** heredará el permiso en la tabla de clientes de producción y David **GRANT** permiso en la tabla de clientes de producción.  
  
-   **DENY** invalida **GRANT** cuando permisos entran en conflicto.  
  
    Por ejemplo, suponga que David de inicio de sesión no tiene permisos en la tabla Customer y es un miembro de dos roles de base de datos: dbgroup1, que tiene **DENY** permiso en la tabla Customer y dbgroup2, que tiene **GRANT** permiso en la tabla Customer. En este caso, David heredará la **DENY** permiso en la tabla Customer. Esto sucede si los roles adquirida sus permisos de forma explícita o implícita.  
  
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
  
-   Ejecute la siguiente consulta para determinar qué inicios de sesión se les ha concedido permisos explícitos.  
  
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
  
-   Ejecute la siguiente consulta en una base de datos de usuario para determinar qué usuarios de base de datos y funciones se han concedido o denegado permisos específicos. Tendrá que vistas adicionales de consulta como sys.objects y sys.schemas para identificar los elementos descritos con la major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Prácticas recomendadas de permisos de base de datos  
  
-   Conceder permisos de nivel más granular que resulta muy práctico. Conceda permisos en la tabla o los permisos de nivel de vista podrían resultar difíciles de administrar. Pero la concesión de permisos en el nivel de base de datos pudieron ser demasiado permisivos. Si la base de datos está diseñada con esquemas para definir los límites de trabajo, es posible conceder permiso para el esquema es un equilibrio adecuado entre el nivel de tabla y el nivel de base de datos.  
  
-   Conceder permisos a los roles, en lugar de a usuarios o inicios de sesión. Administración de derechos mediante el uso de roles en lugar de los usuarios facilita la rápida conceder o revocar un conjunto de permisos para un usuario o inicio de sesión moviéndolos dentro o fuera de la función. Cuando pasa una función de una persona a otra, los permisos pueden permanecer intactos en el nivel de rol mientras los cambios de pertenencia al rol.  
  
-   Conceder permisos a los roles basados en función de trabajo y en los roles de grupo de nivel superiores que combinan los roles de la función de trabajo basados en el grupo de la empresa realiza las acciones.  
  
-   Cada usuario final debe tener un inicio de sesión único. No se permiten a los usuarios compartir inicios de sesión. Proporcionar un inicio de sesión para cada usuario garantiza una pista de auditoría y simplifica la administración de permisos.  
  
## <a name="fixed-database-roles"></a>Roles fijos de base de datos
SQL Server proporciona roles de nivel de base de datos (fijos) preconfigurados para ayudarle a administrar los permisos en un servidor. Los roles preconfigurados son fijos en que no se puede cambiar los permisos asignados a ellos. También se pueden crear roles de base de datos definido por el usuario. Puede cambiar los permisos asignados a los roles de base de datos definido por el usuario.  
  
Roles son entidades de seguridad que agrupan otras entidades de seguridad. Roles de base de datos son toda la base de datos en su ámbito de permisos. Los usuarios de base de datos y otros roles de base de datos se pueden agregar como miembros de roles de base de datos. No se puede agregar los roles fijos de base de datos entre sí. (Los*roles* son como los *grupos* del sistema operativo Windows).  
  
Hay 9 rol fijo de base de datos.  
  
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
El sistema de roles fijos de servidor y roles fijos de base de datos es un sistema heredado que se haya originado en los años de 80. Las funciones fijas de todavía se admiten y son útiles en entornos donde hay pocos usuarios y las necesidades de seguridad son sencillas. A partir de SQL Server 2005, se creó un sistema más detallado de concesión de permisos. Este nuevo sistema sea más granular, proporciona muchas más opciones para conceder y denegar permisos. La complejidad adicional del sistema más granular hace más difícil obtener información, pero la mayoría de los sistemas de empresa deben conceder permisos en lugar de usar los roles fijos. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->El gráfico siguiente muestra los permisos que están asociados a cada rol fijo de base de datos. Todos los permisos en el gráfico de SQL Server no están disponibles (o necesario) en puntos de acceso.  
  
![Funciones fijas de base de datos de seguridad de APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Contenido relacionado  
  
-   Para crear funciones definidas por el usuario, consulte [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Roles fijos de servidor
SQL Server crea automáticamente los roles fijos de servidor. PDW de SQL Server tiene una implementación limitada de roles fijos de servidor de SQL Server. Solo el **sysadmin** y **público** tienen inicios de sesión de usuario como miembros. El **setupadmin** y **dbcreator** roles son utilizados internamente por SQL Server PDW. No se pueden agregar miembros adicionales o quitarse de ninguna función.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin Fixed Server Role  
Los miembros del rol fijo de servidor **sysadmin** pueden realizar cualquier actividad en el servidor. El **sa** inicio de sesión es el único miembro de la **sysadmin** rol fijo de servidor. No se puede agregar inicios de sesión adicionales a la **sysadmin** rol fijo de servidor. La concesión del permiso **CONTROL SERVER** es similar a la pertenencia al rol fijo de servidor **sysadmin**. El siguiente ejemplo se concede el **CONTROL SERVER** permiso para un inicio de sesión denominado Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> El **CONTROL SERVER** permiso proporciona un control casi completo de SQL Server PDW. Siempre que sea posible, proporcionar permisos más granulares para los inicios de sesión en su lugar. Por ejemplo, considere la posibilidad de conceder la **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, o **CREATE ANY DATABASE** permisos.  
  
### <a name="public-server-role"></a>Rol de servidor Public  
Cada inicio de sesión que puede conectarse a SQL Server PDW es un miembro de la **público** rol de servidor. Todos los inicios de sesión heredan los permisos concedidos a **público** en cualquier objeto. Solo puede asignar **público** permisos en un objeto cuando desee que el objeto esté disponible para todos los usuarios. No se puede cambiar la pertenencia en el **público** rol.  
  
> [!NOTE]  
> **pública** se implementa de manera diferente que otros roles. Dado que todas las entidades de seguridad de servidor son miembros de público, la pertenencia de la **público** rol no aparece en la **sys.server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Frente a Roles de servidor fijo. Conceder permisos  
El sistema de roles fijos de servidor y roles fijos de base de datos es un sistema heredado que se haya originado en los años de 80. Las funciones fijas de todavía se admiten y son útiles en entornos donde hay pocos usuarios y las necesidades de seguridad son sencillas. A partir de SQL Server 2005, se creó un sistema más detallado de concesión de permisos. Este nuevo sistema sea más granular, proporciona muchas más opciones para conceder y denegar permisos. La complejidad adicional del sistema más granular hace más difícil obtener información, pero la mayoría de los sistemas de empresa deben conceder permisos en lugar de usar los roles fijos. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Temas relacionados  
  
- [Conceder permisos](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

