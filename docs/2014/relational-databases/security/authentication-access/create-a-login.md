---
title: Creación de un inicio de sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.LOGIN.SERVERROLES.F1
- sql12.swb.login.databaseaccess.f1
- sql12.swb.login.general.f1
- sql12.swb.login.effectivepermissions.f1
- sql12.swb.login.status.f1
helpviewer_keywords:
- authentication [SQL Server], logins
- logins [SQL Server], creating
- creating logins with Management Studio
- Create login [SQL Server]
- SQL Server logins
ms.assetid: fb163e47-1546-4682-abaa-8c9494e9ddc7
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b765248e43dc66b9e1c038df27ca9a8b6135706d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63012027"
---
# <a name="create-a-login"></a>Crear un inicio de sesión
  En este tema se describe cómo crear un inicio de sesión en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Un inicio de sesión es la identidad de la persona o proceso que se está conectando a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Información preliminar](#Background)  
  
     [Seguridad](#Security)  
  
-   **Para crear un inicio de sesión, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Pasos que se deben realizar después de crear un inicio de sesión](#FollowUp)  
  
##  <a name="background"></a>Información previa de <a name="Background"></a>  
 Un inicio de sesión es una entidad de seguridad o una entidad que puede ser autenticada por un sistema seguro. Los usuarios necesitan iniciar sesión para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Puede crear un inicio de sesión basado en una entidad de seguridad de Windows (como un usuario de dominio o un grupo de dominio de Windows) o puede crear un inicio de sesión que no lo esté (como un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ).  
  
> [!NOTE]  
>  Para usar la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el [!INCLUDE[ssDE](../../../includes/ssde-md.md)] debe utilizar la autenticación de modo mixto. Para obtener más información, consulte [elegir un modo de autenticación](../choose-an-authentication-mode.md).  
  
 Como entidad de seguridad, se pueden conceder permisos a los inicios de sesión. El ámbito de un inicio de sesión es todo el [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Para establecer conexión con una base de datos concreta de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], un inicio de sesión debe estar asignado a un usuario de la base de datos. Los permisos dentro de la base de datos se conceden y deniegan al usuario de la base de datos, no al inicio de sesión. Los permisos que tienen como ámbito la instancia completa de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (por ejemplo, el permiso `CREATE ENDPOINT`) se pueden conceder a un inicio de sesión.  
  
##  <a name="security"></a><a name="Security"></a> Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere el permiso `ALTER ANY LOGIN` o `ALTER LOGIN` del servidor.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
##### <a name="to-create-a-sql-server-login"></a>Para crear un inicio de sesión de SQL Server  
  
1.  En el Explorador de objetos, expanda la carpeta de la instancia de servidor en la que desea crear el nuevo inicio de sesión.  
  
2.  Haga clic con el botón secundario en la carpeta **seguridad** , seleccione **nuevo**y seleccione **Inicio de sesión..**..  
  
3.  En el cuadro de diálogo **Inicio de sesión - Nuevo**, en la página **General**, escriba el nombre de un usuario en el cuadro **Nombre de inicio de sesión**. Como alternativa, haga clic en **Buscar...** para abrir el cuadro de diálogo **Seleccionar usuario o grupo** .  
  
     Si hace clic en **Buscar...**:  
  
    1.  En **Seleccionar este tipo de objeto**, haga clic en **Tipos de objeto...** para abrir el cuadro de diálogo **Tipos de objeto** y seleccione alguna o todas las opciones siguientes: **Entidades de seguridad integradas**, **Grupos** y **Usuarios**. Las opciones**Entidades de seguridad integradas** y **Usuarios** están seleccionadas de forma predeterminada. Cuando termine, haga clic en **Aceptar**.  
  
    2.  En **Desde esta ubicación**, haga clic en **Ubicaciones...** para abrir el cuadro de diálogo **Ubicaciones** y seleccione una de las ubicaciones de servidor disponibles. Cuando haya terminado, haga clic en **Aceptar**.  
  
    3.  En **Escribir los nombres de objeto para seleccionar (ejemplos)**, escriba el usuario o el nombre de grupo que quiere buscar. Para obtener más información, vea [Seleccionar usuarios, equipos o grupos (cuadro de diálogo)](https://technet.microsoft.com/library/cc771712.aspx).  
  
    4.  Haga clic en **Avanzadas...** para obtener más opciones avanzadas de búsqueda. Para obtener más información, vea [Seleccionar usuarios, equipos o grupos (cuadro de diálogo) - Página Avanzadas](https://technet.microsoft.com/library/cc733110.aspx).  
  
    5.  Haga clic en **Aceptar**.  
  
4.  Para crear un inicio de sesión basado en una entidad de seguridad de Windows, seleccione **Autenticación de Windows**. Esta es la selección predeterminada.  
  
5.  Para crear un inicio de sesión que se guarde en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , seleccione **Autenticación de SQL Server**.  
  
    1.  En el cuadro **Contraseña**, escriba una contraseña para el nuevo usuario. Vuelva a escribir la contraseña en el cuadro **Confirmar contraseña**.  
  
    2.  Al cambiar una contraseña existente, seleccione **Especificar contraseña anterior**y escriba la contraseña anterior en el cuadro **Contraseña anterior** .  
  
    3.  Para aplicar las opciones de la directiva de contraseñas a efectos de complejidad y exigencia, seleccione **Exigir directivas de contraseñas**. Para obtener más información, vea [Password Policy](../password-policy.md). Esta es una opción predeterminada cuando se selecciona **SQL Server autenticación** .  
  
    4.  Para aplicar las opciones de la directiva de contraseñas a efectos de expiración, seleccione **Exigir expiración de contraseña**. Debe seleccionar la opción **exigir la Directiva de contraseñas** para habilitar esta casilla. Esta es una opción predeterminada cuando se selecciona **SQL Server autenticación** .  
  
    5.  Para obligar al usuario a crear una nueva contraseña después de utilizarse el inicio de sesión por primera vez, seleccione **El usuario debe cambiar la contraseña en el siguiente inicio de sesión**. **Forzar expiración de contraseña** debe estar seleccionada para habilitar esta casilla. Esta es una opción predeterminada cuando se selecciona **SQL Server autenticación** .  
  
6.  Para asociar el inicio de sesión a un certificado de seguridad independiente, seleccione **Asignado a certificado** y seleccione el nombre de un certificado existente de la lista.  
  
7.  Para asociar el inicio de sesión a una clave asimétrica independiente, seleccione **Asignado a clave asimétrica** y seleccione el nombre de una clave existente de la lista.  
  
8.  Para asociar el inicio de sesión a una credencial de seguridad, active la casilla de **Asignado a credencial** y seleccione una credencial existente de la lista o haga clic en **Agregar** para crear una nueva credencial. Para quitar una asignación a una credencial de seguridad del inicio de sesión, seleccione la credencial en **Credenciales asignadas** y haga clic en **Quitar**. Para obtener más información sobre las credenciales en general, vea [Credenciales &#40;motor de base de datos&#41;](credentials-database-engine.md).  
  
9. En la lista **Base de datos predeterminada** , seleccione una base de datos predeterminada para el inicio de sesión. **Master** es el valor predeterminado para esta opción.  
  
10. En la lista **Idioma predeterminado** , seleccione un idioma predeterminado para el inicio de sesión.  
  
11. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="additional-options"></a>Additional Options  
 El cuadro de diálogo **Inicio de sesión-nuevo** también ofrece opciones en cuatro páginas adicionales: **roles del servidor**, **asignación de usuarios**, elementos **protegibles**y **Estado**.  
  
### <a name="server-roles"></a>Roles del servidor  
 La página **Roles de servidor** enumera todos los roles posibles que se pueden asignar al nuevo inicio de sesión. Están disponibles las siguientes opciones:  
  
 Casilla**bulkadmin**  
 Los miembros del rol fijo de servidor **bulkadmin** pueden ejecutar la instrucción BULK INSERT.  
  
 Casilla**dbcreator**  
 Los miembros del rol fijo de servidor **dbcreator** pueden crear, modificar, quitar y restaurar cualquier base de datos.  
  
 Casilla**diskadmin**  
 Los miembros del rol fijo de servidor **diskadmin** pueden administrar archivos de disco.  
  
 Casilla**processadmin**  
 Los miembros del rol fijo de servidor **processadmin** pueden finalizar procesos mediante la ejecución de una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
 Casilla**public**  
 Todos los usuarios, grupos y roles de SQL Server pertenecen al rol fijo de servidor **public** de forma predeterminada.  
  
 Casilla**securityadmin**  
 Los miembros del rol fijo de servidor **securityadmin** administran los inicios de sesión y sus propiedades. Administran los permisos de servidor GRANT, DENY y REVOKE. También administran los permisos de base de datos GRANT, DENY y REVOKE. Asimismo, pueden restablecer contraseñas para inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Casilla**serveradmin**  
 Los miembros del rol fijo de servidor **serveradmin** pueden cambiar opciones de configuración en el servidor y cerrar el servidor.  
  
 Casilla**setupadmin**  
 Los miembros del rol fijo de servidor **setupadmin** pueden agregar y quitar servidores vinculados, y ejecutar algunos procedimientos almacenados del sistema.  
  
 Casilla**sysadmin**  
 Los miembros del rol fijo de servidor **sysadmin** pueden realizar cualquier actividad en el [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
### <a name="user-mapping"></a>Asignación de usuarios  
 La página **Asignación de usuarios** enumera todas las bases de datos posibles y las pertenencias al rol de base de datos en esas bases de datos que se pueden aplicar al inicio de sesión. Las bases de datos seleccionadas determinan las pertenencias a roles disponibles para el inicio de sesión. En esta página están disponibles las opciones siguientes:  
  
 **Usuarios asignados a este inicio de sesión**  
 Selecciona las bases de datos a las que se puede obtener acceso con este inicio de sesión. Cuando se seleccione una base de datos, sus roles de bases de datos válidos se mostrarán en el panel **Miembros del rol de base de datos para:** _nombre_baseDeDatos_ .  
  
 **Map**  
 Permite que el inicio de sesión obtenga acceso a las bases de datos que se muestran a continuación.  
  
 **Base de datos**  
 Muestra las bases de datos disponibles en el servidor.  
  
 **Usuario**  
 Especifica el usuario de base de datos que se va a asignar al inicio de sesión. De forma predeterminada, el nombre del usuario de base de datos coincide con el inicio de sesión.  
  
 **Esquema predeterminado**  
 Especifica el esquema predeterminado del usuario. Cuando se crea un usuario por primera vez, el esquema predeterminado es **dbo**. Es posible especificar un esquema predeterminado que aún no existe. No puede especificar un esquema predeterminado para un usuario asignado a un grupo, un certificado o una clave asimétrica de Windows.  
  
 **Cuenta de invitado habilitada para:**  _nombre_baseDeDatos_  
 Atributo de solo lectura que indica si la cuenta de invitado está habilitada en la base de datos seleccionada. Utilice la página **Estado** del cuadro de diálogo **Propiedades de inicio de sesión** de la cuenta de invitado para habilitarla o deshabilitarla.  
  
 **Miembros del rol de base de datos para:**  _nombre_baseDeDatos_  
 Selecciona los roles para el usuario en la base de datos especificada. Todos los usuarios son miembros del rol **public** de todas las bases de datos, y no pueden eliminarse. Para obtener más información sobre los roles de base de datos, vea [Roles de nivel de base de datos](database-level-roles.md).  
  
### <a name="securables"></a>Elementos protegibles  
 La página **Elementos protegibles** muestra todos los elementos protegibles posibles y los permisos en esos elementos protegibles que se pueden conceder al inicio de sesión. En esta página están disponibles las opciones siguientes:  
  
 **Cuadrícula superior**  
 Contiene uno o más elementos para los que se pueden establecer permisos. Las columnas mostradas en la cuadrícula superior varían dependiendo de la entidad de seguridad o el elemento protegible.  
  
 Para agregar elementos a la cuadrícula superior:  
  
1.  Haga clic en **Buscar**.  
  
2.  En el cuadro de diálogo **agregar objetos** , seleccione una de las opciones siguientes: **objetos específicos...**, **todos los objetos de los tipos...** o **el servidor**_SERVER_NAME_. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Al seleccionar **el servidor**_SERVER_NAME_ se rellena automáticamente la cuadrícula superior con todos los objetos protegibles de los servidores.  
  
3.  Si selecciona **objetos específicos...**:  
  
    1.  En el cuadro de diálogo **seleccionar objetos** , en **seleccionar estos tipos de objeto**, haga clic en **tipos de objeto..**..  
  
    2.  En el cuadro de diálogo **Seleccionar tipos de objeto** , seleccione alguno o todos los tipos de objeto siguientes: **Extremos**, **Inicios de sesión**, **Servidores**, **Grupos de disponibilidad**y **Roles del servidor**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    3.  En **Escriba los nombres de objeto que desea seleccionar (ejemplos)**, haga clic en **examinar..**..  
  
    4.  En el cuadro de diálogo **Buscar objetos** , seleccione cualquiera de los objetos disponibles del tipo que seleccionó en el cuadro de diálogo **Seleccionar tipos de objeto** y haga clic en **Aceptar**.  
  
    5.  En el cuadro de diálogo **Seleccionar objetos** , haga clic en **Aceptar**.  
  
4.  Si selecciona **todos los objetos de los tipos..**., en el cuadro de diálogo **seleccionar tipos de objeto** , seleccione alguno o todos los tipos de objeto siguientes: **extremos**, **inicios de sesión**, **servidores**, grupos de **disponibilidad**y **roles de servidor**. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 **Nombre**  
 El nombre de cada entidad de seguridad o elemento protegible que se agrega a la cuadrícula.  
  
 **Type**  
 Describe el tipo de cada elemento.  
  
 **Pestaña Explícito**  
 Enumere los posibles permisos del elemento protegible seleccionados en la cuadrícula superior. No todas las opciones están disponibles para todos los permisos explícitos.  
  
 **Permisos**  
 Nombre del permiso.  
  
 **Otorgante**  
 La entidad de seguridad que concedió el permiso.  
  
 **Garantizar**  
 Active esta casilla para conceder el permiso al inicio de sesión. Desactívela para revocar el permiso.  
  
 **WITH GRANT**  
 Refleja el estado de la opción WITH GRANT para el permiso indicado. Este cuadro es de solo lectura. Para aplicar este permiso, use la instrucción [GRANT](/sql/t-sql/statements/grant-transact-sql) .  
  
 **Deny**  
 Active esta casilla para denegar el permiso al inicio de sesión. Desactívela para revocar el permiso.  
  
### <a name="status"></a>Estado  
 La página **Estado** enumera algunas de las opciones de autenticación y autorización que se pueden configurar en el inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seleccionado.  
  
 En esta página están disponibles las opciones siguientes:  
  
 **Permiso para conectarse al motor de la base de datos**  
 Cuando trabaje con esta configuración, debe pensar en el inicio de sesión seleccionado como una entidad de seguridad a la que se le puede otorgar o denegar un permiso para un elemento protegible.  
  
 Seleccione **Conceder** para conceder el permiso CONNECT SQL al inicio de sesión. Seleccione **Denegar** para denegar el permiso CONNECT SQL al inicio de sesión.  
  
 **Inicio de sesión**  
 Cuando trabaje con esta configuración, debe pensar en el inicio de sesión seleccionado como un registro de una tabla. Los cambios que se realicen en los valores que se muestran aquí se aplicarán al registro.  
  
 Un inicio de sesión que se ha deshabilitado sigue existiendo en el registro. Pero si intenta conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el inicio de sesión no se autenticará.  
  
 Seleccione esta opción para habilitar o deshabilitar este inicio de sesión. Esta opción utiliza la instrucción ALTER LOGIN con las opciones ENABLE o DISABLE.  
  
 **Autenticación de SQL Server**  
 La casilla **Inicio de sesión bloqueado** solo está disponible si el inicio de sesión seleccionado se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conecta mediante la autenticación de y el inicio de sesión se ha bloqueado. Esta configuración es de solo lectura. Para desbloquear un inicio de sesión fuera el que se bloquea, ejecute ALTER LOGIN con la opción de UNLOCK.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-login-using-windows-authentication"></a>Para crear un inicio de sesión utilizando la autenticación de Windows  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Create a login for SQL Server by specifying a server name and a Windows domain account name.  
  
    CREATE LOGIN [<domainName>\<loginName>] FROM WINDOWS;  
    GO  
  
    ```  
  
#### <a name="to-create-a-login-using-sql-server-authentication"></a>Para crear un inicio de sesión utilizando la autenticación de SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- Creates the user "shcooper" for SQL Server using the security credential "RestrictedFaculty"   
    -- The user login starts with the password "Baz1nga," but that password must be changed after the first login.  
  
    CREATE LOGIN shcooper   
       WITH PASSWORD = 'Baz1nga' MUST_CHANGE,  
       CREDENTIAL = RestrictedFaculty;  
    GO  
  
    ```  
  
 Para obtener más información, vea [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql).  
  
##  <a name="follow-up-steps-to-take-after-you-create-a-login"></a><a name="FollowUp"></a>Seguimiento: pasos que se deben realizar después de crear un inicio de sesión  
 Después de crear un inicio de sesión, este puede conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], pero no necesariamente tiene permisos suficientes para realizar ningún trabajo útil. En la lista siguiente se proporcionan vínculos a las acciones de inicio de sesión comunes.  
  
-   Para combinar el inicio de sesión con un rol, vea [Combinar un rol](join-a-role.md).  
  
-   Para autorizar a un inicio de sesión para que use una base de datos, vea [Crear un usuario de base de datos](../authentication-access/create-a-database-user.md).  
  
-   Para conceder un permiso a un inicio de sesión, vea [Conceder un permiso a una entidad de seguridad](grant-a-permission-to-a-principal.md).  
  
  
