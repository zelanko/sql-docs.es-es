---
title: Entidades de seguridad (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.selectroll.f1
- sql13.swb.databaseuser.permissions.user.f1--May use common.permissions
helpviewer_keywords:
- certificates [SQL Server], principals
- roles [SQL Server], principals
- permissions [SQL Server], principals
- '##MS_SQLAuthenticatorCertificate##'
- principals [SQL Server]
- '##MS_SQLResourceSigningCertificate##'
- groups [SQL Server], principals
- '##MS_AgentSigningCertificate##'
- authentication [SQL Server], principals
- schemas [SQL Server], principals
- principals [SQL Server], about principals
- security [SQL Server], principals
- users [SQL Server], principals
- '##MS_SQLReplicationSigningCertificate##'
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 4860d2b38d6a2da7c6204e4fa6224b5ef08619c7
ms.sourcegitcommit: dceecfeaa596ade894d965e8e6a74d5aa9258112
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2018
ms.locfileid: "40008967"
---
# <a name="principals-database-engine"></a>Entidades de seguridad (motor de base de datos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Las*entidades de seguridad* son entidades que pueden solicitar recursos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Igual que otros componentes del modelo de autorización de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , las entidades de seguridad se pueden organizar en jerarquías. El ámbito de influencia de una entidad de seguridad depende del ámbito de su definición: Windows, servidor o base de datos; y de si la entidad de seguridad es indivisible o es una colección. Un Inicio de sesión de Windows es un ejemplo de entidad de seguridad indivisible y un Grupo de Windows es un ejemplo de una del tipo colección. Toda entidad de seguridad tiene un identificador de seguridad (SID). Este tema se aplica a todas las versiones de SQL Server, pero hay algunas restricciones en las entidades de seguridad de nivel de servidor de SQL Database o SQL Data Warehouse. 
  
## <a name="sql-server-level-principals"></a>Entidades de seguridad de nivel de SQL Server  
  
- Inicio de sesión con autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]   
- Inicio de sesión con autenticación de Windows para un usuario de Windows  
- Inicio de sesión con autenticación de Windows para un grupo de Windows   
- Inicio de sesión con autenticación de Azure Active Directory para un usuario de AD
- Inicio de sesión con autenticación de Azure Active Directory para un grupo de AD
- Rol del servidor  
  
## <a name="database-level-principals"></a>Entidades de seguridad de nivel de bases de datos
  
- Usuario de base de datos (hay 11 tipos de usuarios. Para obtener más información, vea [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md)).
- Rol de base de datos
- Rol de aplicación
  
## <a name="sa-login"></a>Inicio de sesión sa  
 El inicio de sesión `sa` de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es una entidad de seguridad a nivel de servidor. Se crea de forma predeterminada cuando se instala una instancia. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], la base de datos predeterminada de sa es master. Es un cambio de comportamiento con respecto a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El inicio de sesión `sa` es miembro del rol fijo de base de datos `sysadmin`. Este inicio de sesión `sa` tiene todos los permisos en el servidor y no puede limitarse. Además, `sa` no se puede quitar, pero puede deshabilitarse para que nadie lo emplee.

## <a name="dbo-user-and-dbo-schema"></a>Usuario y esquema dbo

El usuario `dbo` es una entidad de seguridad de usuario especial que hay en cada base de datos. Todos los administradores de SQL Server, los miembros del rol fijo de servidor `sysadmin`, el inicio de sesión `sa` y los propietarios de la base de datos especifican las bases de datos como el usuario `dbo`. El usuario `dbo` tiene todos los permisos en la base de datos y no se limitar ni quitar. `dbo` representa el propietario de la base de datos, pero la cuenta de usuario `dbo` no es lo mismo que el rol fijo de base de datos `db_owner`, mientras que el rol fijo de base de datos `db_owner` no es lo mismo que la cuenta de usuario que se registra como el propietario de la base de datos.     
El usuario `dbo` tiene la propiedad del esquema `dbo`. El esquema `dbo` es el predeterminado para todos los usuarios, salvo que se especifique otro.  El esquema `dbo` no puede quitarse.
  
## <a name="public-server-role-and-database-role"></a>Rol público de base de datos y de servidor  
Cada inicio de sesión pertenece al rol fijo de servidor `public` y cada usuario de base de datos pertenece al rol de base de datos `public`. Cuando a un usuario o inicio de sesión no se le han concedido ni denegado permisos concretos para un elemento protegible, hereda los permisos para ese elemento concedidos a public. El rol fijo de servidor `public` y el de base de datos `public` no pueden quitarse. Sin embargo, puede revocar los permisos de los roles `public`. Hay muchos de los permisos que se asignan a los roles `public` de forma predeterminada. La mayoría de estos permisos son necesarios para realizar operaciones rutinarias en la base de datos; el tipo de tareas que todo el mundo debe poder hacer. Tenga cuidado al revocar permisos desde el usuario o el inicio de sesión público, ya que afectará a todos los inicios de sesión y usuarios. Normalmente, no debe denegar permisos a public, ya que la instrucción deny invalida cualquier instrucción grant que podrían crear para los usuarios. 
  
## <a name="informationschema-and-sys-users-and-schemas"></a>INFORMATION_SCHEMA, y usuarios y esquemas sys 
 Todas las bases de datos incluyen dos entidades que aparecen como usuarios en las vistas de catálogo:`INFORMATION_SCHEMA` y `sys`. Estas entidades son necesarias para uso interno por parte del motor de base de datos. No se pueden modificar ni quitar.  
  
## <a name="certificate-based-sql-server-logins"></a>Inicios de sesión de SQL Server basados en certificados  
 Las entidades de seguridad de servidor con nombres incluidos entre signos de número dobles (##) son exclusivamente para uso interno del sistema. Las siguientes entidades de seguridad se crean a partir de certificados cuando se instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y no deben eliminarse.  
  
-   \##MS_SQLResourceSigningCertificate##    
-   \##MS_SQLReplicationSigningCertificate##    
-   \##MS_SQLAuthenticatorCertificate##    
-   \##MS_AgentSigningCertificate##   
-   \##MS_PolicyEventProcessingLogin##   
-   \##MS_PolicySigningCertificate##   
-   \##MS_PolicyTsqlExecutionLogin##   
 
 Estas cuentas principales no tienen contraseñas que los administradores puedan cambiar, ya que se basan en certificados emitidos a Microsoft.
  
## <a name="the-guest-user"></a>Usuario guest  
 Cada base de datos incluye un usuario `guest`. Los permisos concedidos al usuario `guest` se aplican a todos los usuarios que tienen acceso a la base de datos, pero no disponen de una cuenta en la base de datos. No se puede quitar el usuario `guest`, pero se puede deshabilitar si se revoca su permiso CONNECT. El permiso CONNECT se puede revocar si se ejecuta `REVOKE CONNECT FROM GUEST;` en cualquier base de datos que no sea `master` ni `tempdb`.  
  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
 Los temas siguientes se incluyen en esta sección de Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   [Temas de procedimientos de la administración de inicios de sesión, usuarios y esquemas](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Roles de nivel de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [Roles de nivel de base de datos](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [Roles de aplicación](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## <a name="see-also"></a>Ver también  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [Roles de nivel de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Roles de nivel de base de datos](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
