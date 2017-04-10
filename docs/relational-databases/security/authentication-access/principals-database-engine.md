---
title: "Entidades de seguridad (motor de base de datos) | Microsoft Docs"
ms.custom: ""
ms.date: "01/09/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.roleproperties.selectroll.f1"
  - "sql13.swb.databaseuser.permissions.user.f1--May use common.permissions"
helpviewer_keywords: 
  - "certificados [SQL Server], entidades de seguridad"
  - "roles [SQL Server], entidades de seguridad"
  - "permisos [SQL Server], entidades de seguridad"
  - "##MS_SQLAuthenticatorCertificate##"
  - "entidades de seguridad [SQL Server]"
  - "##MS_SQLResourceSigningCertificate##"
  - "grupos [SQL Server], entidades de seguridad"
  - "##MS_AgentSigningCertificate##"
  - "autenticación [SQL Server], entidades de seguridad"
  - "esquemas [SQL Server], entidades de seguridad"
  - "entidades de seguridad [SQL Server], acerca de las entidades de seguridad"
  - "seguridad [SQL Server], entidades de seguridad"
  - "usuarios [SQL Server], entidades de seguridad"
  - "##MS_SQLReplicationSigningCertificate##"
ms.assetid: 3f7adbf7-6e40-4396-a8ca-71cbb843b5c2
caps.latest.revision: 57
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 55
---
# Entidades de seguridad (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  Las*entidades de seguridad* son entidades que pueden solicitar recursos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Igual que otros componentes del modelo de autorización de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , las entidades de seguridad se pueden organizar en jerarquías. El ámbito de influencia de una entidad de seguridad depende del ámbito de su definición: Windows, servidor o base de datos; y de si la entidad de seguridad es indivisible o es una colección. Un Inicio de sesión de Windows es un ejemplo de entidad de seguridad indivisible y un Grupo de Windows es un ejemplo de una del tipo colección. Toda entidad de seguridad tiene un identificador de seguridad (SID).  
  
 **Entidades de seguridad a nivel de Windows**  
  
-   Inicio de sesión del dominio de Windows  
  
-   Inicio de sesión local de Windows  
  
 **Entidades de seguridad**-**de nivel de** **SQL Server**  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Inicio de sesión  
  
-   Rol del servidor  
  
 **Entidades de seguridad de nivel de bases de datos**  
  
-   Usuario de la base de datos  
  
-   Rol de base de datos  
  
-   Rol de aplicación  
  
## Inicio de sesión sa de SQL Server  
 El inicio de sesión sa de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es una entidad de seguridad de nivel de servidor. Se crea de forma predeterminada cuando se instala una instancia. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], la base de datos predeterminada de sa es master. Es un cambio de comportamiento con respecto a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## Rol de base de datos public  
 Todos los usuarios de una base de datos pertenecen al rol de base de datos public. Cuando a un usuario no se le han concedido ni denegado permisos concretos para un elemento protegible, hereda los permisos para ese elemento concedidos a public.  
  
## INFORMATION_SCHEMA y sys  
 Todas las bases de datos incluyen dos entidades que aparecen como usuarios en las vistas de catálogo: INFORMATION_SCHEMA y sys. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] necesita estas dos entidades. No son entidades de seguridad y no se pueden modificar ni quitar.  
  
## Inicios de sesión de SQL Server basados en certificados  
 Las entidades de seguridad de servidor con nombres incluidos entre signos de número dobles (##) son exclusivamente para uso interno del sistema. Las siguientes entidades de seguridad se crean a partir de certificados cuando se instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y no deben eliminarse.  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## Usuario guest  
 Cada base de datos incluye un usuario **guest**. Los permisos concedidos al usuario **guest** se aplican a todos los usuarios que tienen acceso a la base de datos, pero no disponen de una cuenta en la base de datos. No se puede quitar el usuario **guest** , pero se puede deshabilitar si se revoca su permiso **CONNECT** . El permiso **CONNECT** se puede revocar si se ejecuta `REVOKE CONNECT FROM GUEST` en cualquier base de datos que no sea master ni tempdb.  
  
## Cliente y servidor de base de datos  
 Por definición, un cliente y un servidor de base de datos son entidades de seguridad y se pueden proteger. Estas entidades se pueden autenticar mutuamente antes de establecer una conexión de red segura. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite el protocolo de autenticación [Kerberos](http://go.microsoft.com/fwlink/?LinkId=100758) , que define cómo interactúan los clientes con un servicio de autenticación de red.  
  
## Tareas relacionadas  
 Para más información acerca de cómo diseñar un sistema de permisos, consulte [Getting Started with Database Engine Permissions](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
 Los temas siguientes se incluyen en esta sección de Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   [Temas de procedimientos de la administración de inicios de sesión, usuarios y esquemas](../../../relational-databases/security/authentication-access/managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Roles de nivel de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)  
  
-   [Roles de nivel de base de datos](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
-   [Roles de aplicación](../../../relational-databases/security/authentication-access/application-roles.md)  
  
## Vea también  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.sql_logins &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [Roles de nivel de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Roles de nivel de base de datos](../../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  