---
title: Solucionar problemas de usuarios huérfanos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38a33b34b64cf285e94f66c547b2309b8daf1ae8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48167645"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>Solucionar problemas de usuarios huérfanos (SQL Server)
  Para iniciar sesión en una instancia de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], una entidad de seguridad debe tener un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido. Este inicio de sesión se utiliza en el proceso de autenticación que comprueba si la entidad de seguridad tiene permiso para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión en una instancia de servidor están visibles en el **sys.server_principals** vista de catálogo y el **sys.syslogins** vista de compatibilidad.  
  
 Los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen acceso a bases de datos individuales mediante un usuario de base de datos que está asignado al inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta regla tiene dos excepciones:  
  
-   La cuenta de invitado.  
  
     Al habilitar esta cuenta en la base de datos, se habilitan todos los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no estén asignados a un usuario de base de datos para entrar en la base de datos como usuario invitado.  
  
-   La pertenencia a grupos de Microsoft Windows.  
  
     Un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado desde un usuario de Windows puede entrar en una base de datos si este usuario es miembro de un grupo de Windows que también sea usuario en la base de datos.  
  
 La información sobre la asignación de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un usuario de la base de datos se almacena en la base de datos. Incluye el nombre del usuario de la base de datos y el SID del inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente. Los permisos de este usuario de la base de datos se utilizan para otorgar autorizaciones en la base de datos.  
  
 Un usuario de base de datos cuyo inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente está sin definir o se ha definido de forma incorrecta en una instancia de servidor no podrá iniciar una sesión en la instancia. Es lo que se denomina un *usuario huérfano* de la base de datos en esa instancia de servidor. Un usuario de base de datos puede convertirse en huérfano si se quita el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondiente. También puede convertirse en huérfano si una base de datos se restaura o se conecta a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Otra manera de convertirse en huérfano es que el SID al que se asigna el usuario de la base de datos no esté presente en la nueva instancia de servidor.  
  
> [!NOTE]  
>  Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión no puede tener acceso a una base de datos que le falte un usuario de base de datos correspondiente a menos que **invitado** está habilitada en esa base de datos. Para obtener información acerca de cómo crear una cuenta de usuario de base de datos, vea [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql).  
  
## <a name="to-detect-orphaned-users"></a>Para detectar usuarios huérfanos  
 Ejecute las instrucciones de Transact-SQL siguientes:   
  
```  
USE <database_name>;  
GO;   
sp_change_users_login @Action='Report';  
GO;  
```  
  
 En los resultados se enumeran los usuarios y sus identificadores de seguridad (SID) correspondientes, que se encuentran en la base de datos actual y no están vinculados a ningún inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql).  
  
> [!NOTE]  
>  **sp_change_users_login** no se puede usar con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicios de sesión que se crean a partir de Windows.  
  
## <a name="to-resolve-an-orphaned-user"></a>Para resolver un usuario huérfano  
 Utilice el siguiente procedimiento:  
  
1.  El siguiente comando vuelve a vincular la cuenta de inicio de sesión de servidor especificada por *< login_name >* con el usuario de base de datos especificado por *< database_user >*.  
  
    ```  
    USE <database_name>;  
    GO  
    sp_change_users_login @Action='update_one', @UserNamePattern='<database_user>', @LoginName='<login_name>';  
    GO  
  
    ```  
  
     Para obtener más información, consulte [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql).  
  
2.  Una vez ejecutado el código del paso anterior, el usuario podrá obtener acceso a la base de datos. El usuario puede modificar la contraseña de la *< login_name >* cuenta de inicio de sesión mediante el uso de la **sp_password** procedimiento almacenado, como sigue:  
  
    ```  
    USE master   
    GO  
    sp_password @old=NULL, @new='password', @loginame='<login_name>';  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  Solo los inicios de sesión con el permiso ALTER ANY LOGIN pueden cambiar la contraseña de inicio de sesión de otro usuario. Sin embargo, solo los miembros del rol **sysadmin** pueden modificar las contraseñas de los miembros del rol **sysadmin** .  
  
    > [!NOTE]  
    >  **sp_password** no se puede usar para [!INCLUDE[msCoName](../../includes/msconame-md.md)] las cuentas de Windows. Windows autentica los usuarios que se conectan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de su cuenta de red de Windows y, por tanto, sus contraseñas solo se pueden cambiar en Windows.  
  
     Para obtener más información, consulte [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)   
 [sp_change_users_login &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)   
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)   
 [sp_grantlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-grantlogin-transact-sql)   
 [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)   
 [sys.sysusers &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysusers-transact-sql)   
 [Sys.syslogins &#40;Transact-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-syslogins-transact-sql)  
  
  
