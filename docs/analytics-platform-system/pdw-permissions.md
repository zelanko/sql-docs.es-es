---
title: Permisos
description: En este artículo se describen los requisitos y las opciones para administrar los permisos de base de datos para el almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: d60c6f492b0735e70a2c3103e48ad08953039adc
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400868"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Administración de permisos en almacenamiento de datos paralelos
En este artículo se describen los requisitos y las opciones para administrar los permisos de base de datos para PDW de SQL Server.  
  
## <a name="BackupRestoreBasics"></a>Aspectos básicos de los permisos de Motor de base de datos  
Motor de base de datos permisos en PDW de SQL Server se administran en el nivel de servidor a través de inicios de sesión y en el nivel de base de datos a través de usuarios de base de datos y roles de base de datos definidos por el usuario.  
  
**Inicios**  
Los inicios de sesión son cuentas de usuario individuales para iniciar sesión en el PDW de SQL Server. PDW de SQL Server admite inicios de sesión con la autenticación de Windows y la autenticación de SQL Server.  Los inicios de sesión de autenticación de Windows pueden ser usuarios o grupos de Windows de cualquier dominio en el que confíe PDW de SQL Server. SQL Server los inicios de sesión de autenticación se definen y autentican mediante PDW de SQL Server y se deben crear especificando una contraseña.  
  
Los miembros del rol fijo de servidor **sysadmin** (como el inicio de sesión **SA** ) pueden conectarse a una base de datos sin tener que estar asignados a un usuario de base de datos. Se asignan al usuario **DBO** . El propietario de la base de datos también se asigna como el usuario **DBO** .  
  
**Roles de servidor**  
Hay cuatro roles de servidor especiales con un conjunto de roles preconfigurados que proporcionan un grupo práctico de permisos de nivel de servidor. Los roles de servidor **sysadmin**, **MediumRC**, **LargeRC**y **XLargeRCfixed** son los únicos roles de servidor implementados actualmente en PDW de SQL Server. El inicio de sesión **SA** es el único miembro del rol fijo de servidor **sysadmin** y no se pueden agregar inicios de sesión adicionales al rol **sysadmin** . A los inicios de sesión se les puede conceder el permiso **Control Server** , que es similar, aunque no idéntico, al rol fijo de servidor **sysadmin** . Utilice [ALTER Server role](../t-sql/statements/alter-server-role-transact-sql.md) para agregar miembros a los demás roles de servidor. PDW de SQL Server no admite roles de servidor definidos por el usuario.  
  
**Usuarios de base de datos**  
A los inicios de sesión se les concede acceso a una base de datos al crear un usuario de base de datos en una base de datos y asignar ese usuario de base de datos a un inicio de sesión Normalmente, el nombre de usuario de base de datos es el mismo que el nombre de inicio de sesión, aunque no tiene por qué ser así en todos los casos. Cada usuario de base de datos se asigna a un inicio de sesión único. Un inicio de sesión se puede asignar a un único usuario en una base de datos, pero se puede asignar como usuario de base de datos en distintas bases de datos.  
  
**Roles fijos de base de datos**  
Los roles fijos de base de datos son un conjunto de roles preconfigurados que proporcionan un grupo práctico de permisos de nivel de base de datos. Los usuarios de base de datos y los roles de base de datos definidos por el usuario se pueden agregar a los roles fijos de base de datos mediante el procedimiento [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) . Para obtener más información acerca de los roles fijos de base de datos, consulte [roles fijos de base de datos](#fixed-database-roles).  
  
**Roles de base de datos definidos por el usuario**  
Los usuarios con el permiso **crear rol** pueden crear nuevos roles de base de datos definidos por el usuario para representar grupos de usuarios con permisos comunes. Normalmente, los permisos se conceden o deniegan a todo el rol, lo que simplifica la administración y supervisión de permisos.  
  
Los permisos se conceden a las entidades de seguridad (inicios de sesión, usuarios y roles) mediante la instrucción **Grant** . Los permisos se deniegan explícitamente mediante el comando **Deny** . Los permisos concedidos o denegados previamente se quitan mediante la instrucción **REVOKE** . Los permisos son acumulativos, de modo que el usuario recibe todos los permisos concedidos al usuario, al inicio de sesión y a cualquier pertenencia a algún grupo. Sin embargo, las denegaciones de permisos invalidan todas las concesiones. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
En el ejemplo siguiente se muestra un método común y recomendado para la configuración de permisos.  
  
1.  Si usa la autenticación de Windows, cree un inicio de sesión para cada usuario de Windows o grupo de Windows que se conectará a PDW de SQL Server. Si usa la autenticación de SQL Server, cree un inicio de sesión para cada persona que se conectará a PDW de SQL Server.  
  
2.  Cree un usuario de base de datos para cada inicio de sesión en todas las bases de datos necesarias.  
  
3.  Cree uno o varios roles de base de datos definidos por el usuario, cada uno de los cuales representa una función similar. Por ejemplo, analista financiero y analista de ventas.  
  
4.  Agregar usuarios de base de datos a uno o varios roles de base de datos definidos por el usuario.  
  
5.  Conceda permisos a los roles de base de datos definidos por el usuario.  
  
Los inicios de sesión son objetos de nivel de servidor y se pueden enumerar mediante la visualización de [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Solo se pueden conceder permisos de nivel de servidor a las entidades de seguridad de servidor.  
  
Los usuarios y los roles de base de datos son objetos de nivel de base de datos y se pueden enumerar mediante la visualización de [Sys. database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Solo se pueden conceder permisos de nivel de base de datos a las entidades de seguridad de base de datos.  
  
## <a name="BackupTypes"></a>Permisos predeterminados  
En la lista siguiente se describen los permisos predeterminados:  
  
-   Cuando se crea un inicio de sesión mediante la instrucción **Create login** , el inicio de sesión recibe el permiso **Connect SQL** , lo que permite que el inicio de sesión se conecte al PDW de SQL Server.  
  
-   Cuando se crea un usuario de base de datos mediante la instrucción **Create User** , el usuario recibe el permiso **Connect on database::** _<database_name>_ , lo que permite que el inicio de sesión se conecte a esa base de datos como un usuario.  
  
-   Todas las entidades de seguridad, incluido el rol público, no tienen permisos explícitos o implícitos de forma predeterminada porque los permisos implícitos se heredan de los permisos explícitos. Por lo tanto, si no hay ningún permiso explícito, tampoco puede haber permisos implícitos.  
  
-   Cuando un inicio de sesión se convierte en el propietario de un objeto o base de datos, el inicio de sesión siempre tiene todos los permisos en el objeto o la base de datos. Los permisos de propiedad no están visibles como permisos explícitos. Las instrucciones **Grant**, **REVOKE**y **Deny** no tienen ningún efecto en los permisos de propiedad. La propiedad se puede cambiar mediante la instrucción [ALTER Authorization](../t-sql/statements/alter-authorization-transact-sql.md) .  
  
-   El inicio de sesión sa tiene todos los permisos en el dispositivo. Al igual que sucede con los permisos de propiedad, los permisos sa no se pueden cambiar y no están visibles como permisos explícitos. Las instrucciones **Grant**, **REVOKE**y **Deny** no tienen ningún efecto en los permisos de SA.  
  
-   El rol de servidor público no recibe permisos de forma predeterminada y no hereda los permisos de otros roles de servidor. El rol de servidor público puede recibir permisos explícitos con las instrucciones **Grant**, **REVOKE**y **Deny** .  
  
-   Las transacciones no requieren permisos. Todas las entidades de seguridad pueden ejecutar los comandos **BEGIN TRANSACTION**, **commit**y **Rollback** Transaction. Sin embargo, una entidad de seguridad debe tener los permisos adecuados para ejecutar cada instrucción dentro de la transacción.  
  
-   La instrucción **USE** no requiere permisos. Todas las entidades de seguridad pueden ejecutar la instrucción **use** en cualquier base de datos; sin embargo, para tener acceso a una base de datos deben tener una entidad de seguridad de usuario en la base de datos o el usuario Guest debe estar habilitado.  
  
### <a name="the-public-role"></a>El rol PUBLIC  
Todos los nuevos inicios de sesión de aplicación pertenecen automáticamente al rol PUBLIC. El rol de servidor público tiene las siguientes características:  
  
-   El rol de servidor público no tiene permisos de forma predeterminada.  
  
-   Todas las entidades de seguridad son miembros del rol de servidor público y el rol de servidor público no es miembro de otro rol de servidor.  
  
-   El rol de servidor público no puede heredar permisos implícitos. Los permisos asignados al rol PUBLIC deben concederse explícitamente.  
  
## <a name="BackupProc"></a>Determinar los permisos  
El hecho de que un inicio de sesión tenga permiso para realizar una acción específica dependerá de los permisos concedidos o denegados para iniciar sesión, el usuario y los roles de los que es miembro el usuario. Los permisos de nivel de servidor (como **crear inicio de sesión** y **ver estado del servidor**) están disponibles para las entidades de seguridad de nivel de servidor (inicios de sesión). Los permisos de nivel de base de datos (como **Select** from a TABLE o **Execute** on a procedure) están disponibles para las entidades de seguridad de nivel de base de datos (usuarios y roles de base de datos).  
  
### <a name="implicit-and-explicit-permissions"></a>Permisos implícitos y explícitos  
Un *permiso explícito* es un permiso **GRANT** o **DENY** concedido a una entidad de seguridad mediante una instrucción **GRANT** o **DENY**. Los permisos de nivel de base de datos se muestran en la vista [Sys. database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) . Los permisos de nivel de servidor se enumeran en la vista [Sys. server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) .  
  
Un *permiso implícito* es un permiso **Grant** o **Deny** que ha heredado una entidad de seguridad (rol de servidor o inicio de sesión). Los permisos se pueden heredar de las siguientes maneras.  
  
-   Una entidad de seguridad puede heredar un permiso de un rol si la entidad de seguridad es miembro del rol, incluso si la entidad de seguridad no tiene un permiso **Grant** o **Deny** explícito.  
  
-   Una entidad de seguridad puede heredar un permiso en un objeto subordinado (como una tabla) si la entidad de seguridad tiene un permiso en uno de los ámbitos principales de los objetos (por ejemplo, el esquema de la tabla o el permiso en toda la base de datos).  
  
-   Una entidad de seguridad puede heredar un permiso teniendo un permiso que incluye un permiso subordinado. Por ejemplo, el permiso **ALTER any User** incluye tanto el **usuario Create** como **ALTER en User::** _<name>_ Permissions.  
  
### <a name="determining-permissions-when-performing-actions"></a>Determinar los permisos al realizar acciones  
El proceso de determinar qué permiso asignar a una entidad de seguridad es complejo. La complejidad se produce al determinar los permisos implícitos porque las entidades de seguridad pueden ser miembros de varios roles y los permisos se pueden pasar a través de varios niveles en la jerarquía de roles.  
  
En la lista siguiente se describen las reglas generales para determinar los permisos:  
  
-   La propiedad implica el permiso.  
  
    Un propietario del objeto tiene todos los permisos en el objeto. Del mismo modo, un propietario de la base de datos tiene todos los permisos en la base de datos y todos los permisos en los objetos de la base de datos. Estos permisos no se pueden cambiar.  
  
-   Los permisos se pueden heredar entre varios niveles en la jerarquía de pertenencias a roles de servidor.  
  
    Por ejemplo, supongamos que tiene la siguiente situación:  
  
    -   El inicio de sesión David es miembro del rol de base de datos PerfAnalysts.  
  
    -   PerfAnalysts es un miembro del rol de base de datos Production.  
  
    -   David y PerfAnalysts no tienen ningún permiso **Select** en la tabla Customer. El permiso se ha revocado o nunca se ha concedido explícitamente.  
  
    -   Production tiene el permiso **Select** en la tabla Customer.  
  
    En este caso, PerfAnalysts heredará el permiso **Grant** en la tabla Customer de Production y David heredará el permiso **Grant** en la tabla Customer de Production.  
  
-   **Deny** invalidaciones **Grant** cuando hay conflictos de permisos.  
  
    Por ejemplo, supongamos que el inicio de sesión David no tiene permisos en la tabla Customer y es miembro de dos roles de base de datos-dbgroup1, que tiene el permiso **Deny** en la tabla Customer y dbgroup2, que tiene el permiso **Grant** en la tabla Customer. En este caso, David heredará el permiso **Deny** en la tabla Customer. Este es el caso de que los roles hayan adquirido sus permisos explícita o implícitamente.  
  
### <a name="auditing-permissions"></a>Permisos de auditoría  
Para investigar los permisos de un usuario, compruebe lo siguiente.  
  
-   Ejecute la siguiente consulta para determinar qué inicios de sesión son administradores del sistema.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Ejecute la siguiente consulta para determinar a qué inicios de sesión se les ha concedido permisos explícitos.  
  
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
  
-   Ejecute la siguiente consulta en una base de datos de usuario para determinar a qué usuarios y roles de base de datos se les han concedido o denegado permisos específicos. Tendrá que consultar vistas adicionales como sys. Objects y sys. Schemas para identificar los elementos que se describen con el major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Procedimientos recomendados de permisos de base de datos  
  
-   Conceda permisos en el nivel más granular que sea práctico. La concesión de permisos en los permisos de nivel de tabla o vista podría ser no administrable. Pero conceder permisos en el nivel de base de datos podría ser demasiado permisivo. Si la base de datos está diseñada con esquemas para definir los límites de trabajo, quizás el permiso de concesión al esquema sea un riesgo adecuado entre el nivel de tabla y el nivel de base de datos.  
  
-   Conceda permisos a los roles, en lugar de a usuarios o inicios de sesión. La administración de derechos mediante el uso de roles en lugar de usuarios facilita la concesión o la revocación rápida de un conjunto de permisos para un usuario o un inicio de sesión mediante su traslado al rol o desde él. Cuando una función pasa de una persona a otra, los permisos pueden permanecer intactos en el nivel de rol mientras cambia la pertenencia al rol.  
  
-   Conceda permisos a los roles según la función de trabajo y en los roles de grupo de nivel superior que combinen los roles de función de trabajo en función del grupo de empresa que realiza las acciones.  
  
-   Cada usuario final debe tener un inicio de sesión único. No permita que los usuarios compartan inicios de sesión. Proporcionar un inicio de sesión para cada usuario garantiza una traza de auditoría y simplifica la administración de permisos.  
  
## <a name="fixed-database-roles"></a>Roles fijos de base de datos
SQL Server proporciona roles de nivel de base de datos preconfigurados (fijos) para ayudarle a administrar los permisos en un servidor. Los roles configurados previamente son fijos en que no se pueden cambiar los permisos asignados a ellos. También se pueden crear roles de base de datos definidos por el usuario. Puede cambiar los permisos asignados a los roles de base de datos definidos por el usuario.  
  
Los roles son entidades de seguridad que agrupan otras entidades de seguridad. Los roles de base de datos están en el ámbito de los permisos de toda la base de datos. Los usuarios de base de datos y otros roles de base de datos se pueden agregar como miembros de roles de base de datos. Los roles fijos de base de datos no se pueden agregar entre sí. (Los*roles* son como los *grupos* del sistema operativo Windows).  
  
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
  
### <a name="permissions-of-the-fixed-database-roles"></a>Permisos de los roles fijos de base de datos  
El sistema de los roles fijos de servidor y los roles fijos de base de datos es un sistema heredado originado en los 1980. Los roles fijos todavía se admiten y son útiles en entornos donde hay pocos usuarios y las necesidades de seguridad son sencillas. A partir de SQL Server 2005, se ha creado un sistema más detallado de concesión de permisos. Este nuevo sistema es más granular y ofrece muchas más opciones para conceder y denegar permisos. La complejidad adicional del sistema más granular dificulta el aprendizaje, pero la mayoría de los sistemas empresariales deben conceder permisos en lugar de usar los roles fijos. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->En el gráfico siguiente se muestran los permisos que están asociados a cada rol fijo de base de datos. Todos los permisos de este gráfico SQL Server no están disponibles (o necesarios) en APS.  
  
![Roles fijos de base de datos de seguridad de APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Contenido relacionado  
  
-   Para crear roles definidos por el usuario, consulte [crear rol](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Roles fijos de servidor
Los roles fijos de servidor se crean automáticamente mediante SQL Server. PDW de SQL Server tiene una implementación limitada de roles fijos de servidor SQL Server. Solo los **administradores** de conexiones de usuario y los usuarios **públicos** tienen inicios de sesión como miembros. Los roles **setupadmin** y **dbcreator** son utilizados internamente por PDW de SQL Server. No se pueden agregar ni quitar miembros adicionales de ningún rol.  
  
### <a name="sysadmin-fixed-server-role"></a>Rol fijo de servidor sysadmin  
Los miembros del rol fijo de servidor **sysadmin** pueden realizar cualquier actividad en el servidor. El inicio de sesión **SA** es el único miembro del rol fijo de servidor **sysadmin** . No se pueden agregar inicios de sesión adicionales al rol fijo de servidor **sysadmin** . La concesión del permiso **CONTROL SERVER** es similar a la pertenencia al rol fijo de servidor **sysadmin**. En el ejemplo siguiente se concede el permiso **Control Server** a un inicio de sesión denominado Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> El permiso **Control Server** proporciona un control prácticamente completo de PDW de SQL Server. Siempre que sea posible, proporcione permisos más granulares a los inicios de sesión en su lugar. Por ejemplo, considere la posibilidad de conceder los permisos **ver estado del servidor**, **modificar cualquier inicio de sesión**, **ver cualquier base de datos**o **crear cualquier base de datos** .  
  
### <a name="public-server-role"></a>Rol de servidor público  
Cada inicio de sesión que se puede conectar a PDW de SQL Server es miembro del rol de servidor **Public** . Todos los inicios de sesión heredan los permisos concedidos a **Public** en cualquier objeto. Asigne solo permisos **públicos** en un objeto cuando desee que el objeto esté disponible para todos los usuarios. No se puede cambiar la pertenencia al rol **Public** .  
  
> [!NOTE]  
> **Public** se implementa de manera diferente que otros roles. Dado que todas las entidades de seguridad de servidor son miembros de Public, la pertenencia del rol **Public** no aparece en la DMV **Sys. server_role_members** .  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Roles fijos de servidor frente a permisos de concesión  
El sistema de los roles fijos de servidor y los roles fijos de base de datos es un sistema heredado originado en los 1980. Los roles fijos todavía se admiten y son útiles en entornos donde hay pocos usuarios y las necesidades de seguridad son sencillas. A partir de SQL Server 2005, se ha creado un sistema más detallado de concesión de permisos. Este nuevo sistema es más granular y ofrece muchas más opciones para conceder y denegar permisos. La complejidad adicional del sistema más granular dificulta el aprendizaje, pero la mayoría de los sistemas empresariales deben conceder permisos en lugar de usar los roles fijos. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Temas relacionados  
  
- [Conceder permisos](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->

