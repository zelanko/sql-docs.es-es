---
title: Entidades de seguridad (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.roleproperties.selectroll.f1
- sql12.swb.databaseuser.permissions.user.f1--May use common.permissions
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 54aab33e754331482ef154d9172f0e41cd251db0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63011910"
---
# <a name="principals-database-engine"></a>Entidades de seguridad (motor de base de datos)
  Las*entidades de seguridad* son entidades que pueden solicitar recursos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Igual que otros componentes del modelo de autorización de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , las entidades de seguridad se pueden organizar en jerarquías. El ámbito de influencia de una entidad de seguridad depende del ámbito de su definición: Windows, servidor o base de datos; y de si la entidad de seguridad es indivisible o es una colección. Un Inicio de sesión de Windows es un ejemplo de entidad de seguridad indivisible y un Grupo de Windows es un ejemplo de una del tipo colección. Toda entidad de seguridad tiene un identificador de seguridad (SID).  
  
 **Entidades de seguridad a nivel de Windows**  
  
-   Inicio de sesión del dominio de Windows  
  
-   Inicio de sesión local de Windows  
  
 **SQL Server**-**level** **Entidades** de seguridad de nivel de SQL Server  
  
-   Inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
-   Rol de servidor  
  
 **Entidades de seguridad de nivel de bases de datos**  
  
-   Usuario de la base de datos  
  
-   Rol de base de datos  
  
-   Rol de aplicación  
  
## <a name="the-sql-server-sa-login"></a>Inicio de sesión sa de SQL Server  
 El inicio de sesión sa de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es una entidad de seguridad de nivel de servidor. Se crea de forma predeterminada cuando se instala una instancia. A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], la base de datos predeterminada de sa es master. Es un cambio de comportamiento con respecto a versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="public-database-role"></a>Rol de base de datos public  
 Todos los usuarios de una base de datos pertenecen al rol de base de datos public. Cuando a un usuario no se le han concedido ni denegado permisos concretos para un elemento protegible, hereda los permisos para ese elemento concedidos a public.  
  
## <a name="information_schema-and-sys"></a>INFORMATION_SCHEMA y sys  
 Todas las bases de datos incluyen dos entidades que aparecen como usuarios en las vistas de catálogo: INFORMATION_SCHEMA y sys. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]necesita estas dos entidades. No son entidades de seguridad y no se pueden modificar ni quitar.  
  
## <a name="certificate-based-sql-server-logins"></a>Inicios de sesión de SQL Server basados en certificados  
 Las entidades de seguridad de servidor con nombres incluidos entre signos de número dobles (##) son exclusivamente para uso interno del sistema. Las siguientes entidades de seguridad se crean a partir de certificados cuando se instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y no deben eliminarse.  
  
-   \##MS_SQLResourceSigningCertificate##  
  
-   \##MS_SQLReplicationSigningCertificate##  
  
-   \##MS_SQLAuthenticatorCertificate##  
  
-   \##MS_AgentSigningCertificate##  
  
-   \##MS_PolicyEventProcessingLogin##  
  
-   \##MS_PolicySigningCertificate##  
  
-   \##MS_PolicyTsqlExecutionLogin##  
  
## <a name="the-guest-user"></a>Usuario guest  
 Cada base de datos incluye un usuario **guest**. Los permisos concedidos al usuario **guest** se aplican a todos los usuarios que tienen acceso a la base de datos, pero no disponen de una cuenta en la base de datos. No se puede quitar el usuario **Guest** , pero se puede deshabilitar si se revoca su `CONNECT` permiso. El `CONNECT` permiso se puede revocar si se ejecuta `REVOKE CONNECT FROM GUEST` en cualquier base de datos que no sea Master o tempdb.  
  
## <a name="client-and-database-server"></a>Cliente y servidor de base de datos  
 Por definición, un cliente y un servidor de base de datos son entidades de seguridad y se pueden proteger. Estas entidades se pueden autenticar mutuamente antes de establecer una conexión de red segura. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]admite el protocolo de autenticación [Kerberos](https://go.microsoft.com/fwlink/?LinkId=100758) , que define cómo interactúan los clientes con un servicio de autenticación de red.  
  
## <a name="related-tasks"></a>Related Tasks  
 Los temas siguientes se incluyen en esta sección de Libros en pantalla de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   [Temas de procedimientos de la administración de inicios de sesión, usuarios y esquemas](managing-logins-users-and-schemas-how-to-topics.md)  
  
-   [Roles de nivel de servidor](server-level-roles.md)  
  
-   [Roles de nivel de base de datos](database-level-roles.md)  
  
-   [Roles de aplicación](application-roles.md)  
  
## <a name="see-also"></a>Consulte también  
 [Proteger SQL Server](../securing-sql-server.md)   
 [Sys. database_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-principals-transact-sql)   
 [Sys. server_principals &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-principals-transact-sql)   
 [Sys. sql_logins &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-logins-transact-sql)   
 [Sys. database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)   
 [Roles de nivel de servidor](server-level-roles.md)   
 [Roles de nivel de base de datos](database-level-roles.md)  
  
  
