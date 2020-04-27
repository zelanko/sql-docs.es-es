---
title: Creación de un perfil de correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], public profiles
- profiles [SQL Server], Database Mail
- public profiles [Database Mail]
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 55eab0bbfacdde17ff69dd36a0641561695bc14d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62872211"
---
# <a name="create-a-database-mail-profile"></a>Crear un perfil de correo electrónico de base de datos
  Para crear perfiles públicos y privados de Correo electrónico de base de datos, use el **Asistente para configuración de Correo electrónico de base de datos** o [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Cree una o varias cuentas de correo de base de datos para el perfil. Para obtener más información sobre la creación de cuentas de Correo electrónico de base de datos, vea [Crear una nueva cuenta de Correo electrónico de base de datos](create-a-database-mail-account.md).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Los perfiles públicos permiten que cualquier usuario con acceso a la base de datos **msdb** envíe correo electrónico mediante ese perfil. Un perfil privado puede ser usado por un usuario o por un rol. Al conceder a los roles derechos de acceso a los perfiles, se crea una arquitectura más fácil de mantener. Para enviar correo, debe ser un miembro de la función **DatabaseMailUserRole** en la base de datos **msdb** y tener acceso como mínimo a un perfil de Correo electrónico de base de datos.  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 El usuario que crea cuentas de perfil y ejecuta procedimientos almacenados debe ser miembro del rol fijo de servidor sysadmin.  
  

  
##  <a name="using-database-mail-configuration-wizard"></a><a name="SSMSProcedure"></a> Usar el asistente para configuración del Correo electrónico de base de datos  
 **Para crear un perfil de correo electrónico de base de datos**  
  
-   En el explorador de objetos, conecte a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que quiera configurar el Correo electrónico de base de datos y expanda el árbol del servidor.  
  
-   Expanda el nodo **Administración** .  
  
-   Haga doble clic en el correo electrónico de base de datos para abrir el asistente de configuración del correo electrónico de base de datos.  
  
-   En la página **seleccionar tarea de configuración** , seleccione la opción **administrar cuentas y perfiles de correo electrónico de base de datos** y haga clic en **siguiente**.  
  
-   En la página **Administrar perfiles y cuentas** , seleccione la opción **Crear nuevo perfil** y haga clic en **Siguiente**.  
  
-   En la página **Nuevo perfil**, especifique el nombre de perfil, la descripción y agregue las cuentas que se van a incluir en el perfil, y haga clic **Siguiente**.  
  
-   En la página **Finalización del asistente** , revise las acciones que realizará y haga clic en **Finalizar** para completar crear el nuevo perfil.  
  
-   **Para configurar un perfil privado de Correo electrónico de base de datos:**  
  
    -   Abra el Asistente para configuración del Correo electrónico de base de datos.  
  
    -   En la página **Seleccionar tarea de configuración** , seleccione la opción **Administrar cuentas y perfiles de Correo electrónico de base de datos** y haga clic en **Siguiente**.  
  
    -   En la página **Administrar perfiles y cuentas** , seleccione la opción **Administrar seguridad del perfil** y haga clic en **Siguiente**.  
  
    -   En la pestaña **Perfiles privados** , active la casilla correspondiente al perfil que desea configurar y haga clic en **Siguiente**.  
  
    -   En la página **Finalización del asistente** , revise las acciones que realizará y haga clic en **Finalizar** para completar la configuración del perfil.  
  
-   **Para configurar un perfil público de Correo electrónico de base de datos:**  
  
    -   Abra el Asistente para configuración del Correo electrónico de base de datos.  
  
    -   En la página **Seleccionar tarea de configuración** , seleccione la opción **Administrar cuentas y perfiles de Correo electrónico de base de datos** y haga clic en **Siguiente**.  
  
    -   En la página **Administrar perfiles y cuentas** , seleccione la opción **Administrar seguridad del perfil** y haga clic en **Siguiente**.  
  
    -   En la pestaña **Perfiles públicos** , active la casilla correspondiente al perfil que desea configurar y haga clic en **Siguiente**.  
  
    -   En la página **Finalización del asistente** , revise las acciones que realizará y haga clic en **Finalizar** para completar la configuración del perfil.  
  

  
## <a name="using-transact-sql"></a>Usar Transact-SQL  
  
###  <a name="to-create-a-database-mail-private-profile"></a><a name="PrivateProfile"></a>Para crear un perfil privado de Correo electrónico de base de datos  
  
-   Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para crear un nuevo perfil, ejecute el procedimiento almacenado del sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) como sigue:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name*= '*Nombre del perfil*'  
  
     *@description*= '*Descripción*'  
  
     donde *@profile_name* es el nombre del perfil y *@description* es la descripción del perfil. Este parámetro es opcional.  
  
-   Para cada cuenta, ejecute el procedimiento almacenado [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) como sigue:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name*= '*Nombre del perfil*'  
  
     *@account_name*= '*Nombre de la cuenta*'  
  
     *@sequence_number*= '*número de secuencia de la cuenta en el perfil.* '  
  
     donde *@profile_name* es el nombre del perfil y *@account_name* es el nombre de la cuenta que se va a agregar al perfil, *@sequence_number* determina el orden en el que se usan las cuentas en el perfil.  
  
-   Para cada rol o usuario de base de datos que vaya a enviar correo mediante este perfil, concédale acceso a dicho perfil. Para ello, ejecute el procedimiento almacenado [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) como sigue:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name*= '*Nombre del perfil*'  
  
     *@ principal_name* = '*Nombre del usuario o rol de la base de datos*'  
  
     *@is_default*= '*Estado de perfil predeterminado* '  
  
     donde *@profile_name* es el nombre del perfil y *@principal_name* es el nombre del usuario o rol de la base de datos *@is_default* , determina si este perfil es el predeterminado para el usuario o el rol de la base de datos.  
  
 El siguiente ejemplo crea una cuenta de Correo electrónico de base de datos, crea un perfil privado de Correo de base de datos y, a continuación, agrega la cuenta al perfil y le concede acceso al rol de base de datos **DBMailUsers** en la base de datos **msdb** .  
  
```  
-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @account_name = 'AdventureWorks Administrator',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @principal_name = 'ApplicationUser',  
    @is_default = 1 ;  
```  
  
 
  
###  <a name="to-create-a-database-mail-public-profile"></a><a name="PublicProfile"></a>Para crear un perfil público de Correo electrónico de base de datos  
  
-   Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para crear un nuevo perfil, ejecute el procedimiento almacenado del sistema [sysmail_add_profile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql) como sigue:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *@profile_name*= '*Nombre del perfil*'  
  
     *@description*= '*Descripción*'  
  
     donde *@profile_name* es el nombre del perfil y *@description* es la descripción del perfil. Este parámetro es opcional.  
  
-   Para cada cuenta, ejecute el procedimiento almacenado [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql) como sigue:  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *@profile_name*= '*Nombre del perfil*'  
  
     *@account_name*= '*Nombre de la cuenta*'  
  
     *@sequence_number*= '*número de secuencia de la cuenta en el perfil.* '  
  
     donde *@profile_name* es el nombre del perfil y *@account_name* es el nombre de la cuenta que se va a agregar al perfil, *@sequence_number* determina el orden en el que se usan las cuentas en el perfil.  
  
-   Para conceder acceso público, ejecute el procedimiento almacenado [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql) como sigue:  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *@profile_name*= '*Nombre del perfil*'  
  
     *@ principal_name* = '**público** o **0**'  
  
     *@is_default*= '*Estado de perfil predeterminado* '  
  
     donde *@profile_name* es el nombre del perfil y *@principal_name* , para indicar que se trata de un perfil público *@is_default* , determina si este perfil es el predeterminado para el usuario o el rol de la base de datos.  
  
 El ejemplo siguiente se crea una cuenta de Correo electrónico de base de datos, crea un perfil privado de Correo electrónico de base de datos, agrega la cuenta al perfil y concede acceso público al perfil.  
  
```  
-- Create a Database Mail account  
  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Public Account',  
    @description = 'Mail account for use by all database users.',  
    @email_address = 'db_users@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @account_name = 'AdventureWorks Public Account',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to all users in the msdb database  
  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @principal_name = 'public',  
    @is_default = 1 ;  
```  
  

  
  
