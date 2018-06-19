---
title: Roles de nivel de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.roleproperties.database.f1
- sql13.swb.roleproperties.object.f1
- SQL13.SWB.DBROLEPROPERTIES.GENERAL.F1
- sql13.swb.roleproperties.general.f1
helpviewer_keywords:
- db_denydatareader role
- users [SQL Server], database roles
- database-level roles [SQL Server]
- db_denydatawriter role
- roles [SQL Server], database
- principals [SQL Server], database-level
- db_backupoperator role
- credentials [SQL Server], roles
- db_accessadmin role
- schemas [SQL Server], roles
- permissions [SQL Server], roles
- database roles [SQL Server], listed
- db_datareader role
- db_ddladmin role
- db_datawriter role
- db_securityadmin role
- db_owner role
- database roles [SQL Server]
- fixed database roles [SQL Server]
- authentication [SQL Server], roles
- groups [SQL Server], roles
ms.assetid: 7f3fa5f6-6b50-43bb-9047-1544ade55e39
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e2a6b17efe0fd6cc836af208f3d53d4252d3c1ce
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700987"
---
# <a name="database-level-roles"></a>Roles de nivel de base de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para administrar con facilidad los permisos en las bases de datos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona varios *roles* , que son las entidades de seguridad que agrupan a otras entidades de seguridad. Son como los ***grupos*** del sistema operativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Los roles de nivel de base de datos se aplican a toda la base de datos en lo que respecta a su ámbito de permisos.  

Para agregar y quitar usuarios en un rol de base de datos, use las opciones `ADD MEMBER` y `DROP MEMBER` de la instrucción [ALTER ROLE](../../../t-sql/statements/alter-role-transact-sql.md) . [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] no admite este uso de `ALTER ROLE`. En su lugar, use los procedimientos [sp_addrolemember](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) y [sp_droprolemember](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) anteriores.
  
 Existen dos tipos de roles en el nivel de base de datos: los *roles fijos de base de datos* que están predefinidos en la base de datos y los *roles de base de datos definidos por el usuario* que el usuario puede crear.  
  
 Los roles fijos de base de datos se definen en el nivel de base de datos y existen en cada una de ellas. Los miembros de los roles de base de datos **db_owner** pueden administrar la pertenencia a roles fijos de base de datos. También hay algunos roles de base de datos con fines especiales en la base de datos msdb.  
  
 Puede agregar cualquier cuenta de la base de datos y otros roles de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a los roles de nivel de base de datos. Cada miembro de un rol fijo de base de datos puede agregar otros usuarios a ese mismo rol.  
  
> [!TIP]  
>  No agregue roles de base de datos definidos por el usuario como miembros de los roles fijos. Esto podría habilitar un aumento de privilegios no deseado.  

Los permisos de los roles de base de datos definidos por el usuario se pueden personalizar con las instrucciones GRANT, DENY y REVOKE. Para más información, consulte [Permisos (motor de base de datos)](../../../relational-databases/security/permissions-database-engine.md).

Para una lista de todos los permisos, consulte el póster [Permisos del motor de base de datos](https://aka.ms/sql-permissions-poster) . (Los permisos a nivel de servidor no se pueden conceder a los roles de base de datos. Los inicios de sesión y otras entidades de seguridad a nivel de servidor [como roles de servidor] no se pueden agregar a los roles de base de datos. Para la seguridad a nivel de servidor en [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)], use en su lugar [roles de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md) . Los permisos a nivel de servidor no se pueden conceder a través de roles en [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]).

## <a name="fixed-database-roles"></a>roles fijos de base de datos
  
 En la tabla siguiente se muestran los roles fijos de base de datos y sus funcionalidades. Estos roles existen en todas las bases de datos. A excepción del rol de base de datos **public**, no se pueden cambiar los permisos asignados a los roles fijos de base de datos.   
  
|Nombre del rol fijo de base de datos|Descripción|  
|-------------------------------|-----------------|  
|**db_owner**|Los miembros del rol fijo de base de datos **db_owner** pueden realizar todas las actividades de configuración y mantenimiento en la base de datos y también pueden quitar la base de datos en [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)]. (En [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)], algunas actividades de mantenimiento requieren permisos a nivel de servidor y los roles **db_owners**no las pueden realizar).|  
|**db_securityadmin**|Los miembros del rol fijo de base de datos **db_securityadmin** pueden modificar la pertenencia a roles y administrar permisos. Si se agregan entidades de seguridad a este rol, podría habilitarse un aumento de privilegios no deseado.|  
|**db_accessadmin**|Los miembros del rol fijo de base de datos **db_accessadmin** pueden agregar o quitar el acceso a la base de datos para inicios de sesión de Windows, grupos de Windows e inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|**db_backupoperator**|Los miembros del rol fijo de base de datos **db_backupoperator** pueden crear copias de seguridad de la base de datos.|  
|**db_ddladmin**|Los miembros del rol fijo de base de datos **db_ddladmin** pueden ejecutar cualquier comando del lenguaje de definición de datos (DDL) en una base de datos.|  
|**db_datawriter**|Los miembros del rol fijo de base de datos **db_datawriter** pueden agregar, eliminar o cambiar datos en todas las tablas de usuario.|  
|**db_datareader**|Los miembros del rol fijo de base de datos **db_datareader** pueden leer todos los datos de todas las tablas de usuario.|  
|**db_denydatawriter**|Los miembros del rol fijo de base de datos **db_denydatawriter** no pueden agregar, modificar ni eliminar datos de tablas de usuario de una base de datos.|  
|**db_denydatareader**|Los miembros del rol fijo de base de datos **db_denydatareader** no pueden leer datos de las tablas de usuario dentro de una base de datos.|  

No se pueden cambiar los permisos asignados a los roles fijos de base de datos. La ilustración siguiente muestra los permisos asignados a los roles fijos de base de datos:

![fixed_database_role_permissions](../../../relational-databases/security/authentication-access/media/permissions-of-database-roles.png)

## <a name="special-roles-for-includesssdsmdincludessssds-mdmd-and-includesssdwmdincludessssdw-mdmd"></a>Roles especiales para [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)]

Estos roles de base de datos solo existen en la base de datos maestra virtual. Sus permisos están restringidos a las acciones realizadas en la base de datos maestra. Solo los usuarios de base de datos en la base de datos maestra se pueden agregar a estos roles. Los inicios de sesión no se pueden agregar a estos roles, pero los usuarios se pueden crear basados en inicios de sesión y, luego, esos usuarios se pueden agregar a los roles. Los usuarios de bases de datos independientes en la base de datos maestra también se pueden agregar a estos roles.

|Nombre de rol|Descripción|  
|--------------------|-----------------|
**dbmanager** | Puede crear y eliminar bases de datos. Un miembro del rol dbmanager que crea una base de datos se convierte en el propietario de dicha base de datos, lo que permite que el usuario se conecte a ella como el usuario dbo. El usuario dbo tiene todos los permisos de base de datos en la base de datos. Los miembros del rol dbmanager no necesariamente tienen permiso para obtener acceso a las bases de datos que no son de su propiedad.
**loginmanager** | Puede crear y eliminar inicios de sesión en la base de datos maestra virtual.  

> [!NOTE]
> La entidad de seguridad a nivel de servidor y el administrador de Azure Active Directory (si está configurado) tienen todos los permisos en [!INCLUDE[ssSDS_md](../../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../../includes/sssdw-md.md)] sin la necesidad de ser miembros de ninguno de los roles. Para más información, consulte [Autorización y autenticación de SQL Database: concesión de acceso](https://azure.microsoft.com/documentation/articles/sql-database-manage-logins/). 
  
## <a name="msdb-roles"></a>Roles de msdb  
 La base de datos msdb contiene los roles con fines especiales que se muestran en la tabla siguiente.  
  
|Nombre de rol de msdb|Descripción|  
|--------------------|-----------------|  
|**db_ssisadmin**<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|Los miembros de estos roles de base de datos pueden administrar y utilizar [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se actualizan desde una versión anterior podrían contener una versión anterior del rol cuya denominación se realizaba al usar Servicios de transformación de datos (DTS) en lugar de [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Para obtener más información, vea [Roles de Integration Services &#40;servicio SSIS&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md).|  
|**dc_admin**<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|Los miembros de estos roles de base de datos pueden administrar y utilizar el recopilador de datos. Para obtener más información, consulte [Data Collection](../../../relational-databases/data-collection/data-collection.md).|  
|**PolicyAdministratorRole**|Los miembros del rol de base de datos **db_ PolicyAdministratorRole** pueden realizar todas las actividades de mantenimiento y configuración en las condiciones y directivas de Administración basada en directivas. Para obtener más información, vea [Administrar servidores mediante administración basada en directivas](../../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|Los miembros de estos roles de base de datos pueden administrar y utilizar grupos de servidores registrados.|  
|**dbm_monitor**|Se crea en la base de datos **msdb** cuando se registra la primera base de datos en el Monitor de creación de reflejo de la base de datos. El rol **dbm_monitor** no tiene miembros hasta que un administrador del sistema asigna usuarios al rol.|  
  
> [!IMPORTANT]  
>  Los miembros de los roles **db_ssisadmin** y **dc_admin** quizás puedan elevar sus privilegios a sysadmin. Esta elevación de privilegio se puede producir porque estos roles pueden modificar los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] los puede ejecutar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el contexto de seguridad de sysadmin del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para protegerse contra esta elevación de privilegio al ejecutar planes de mantenimiento, conjuntos de recopilación de datos y otros paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , configure los trabajos del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que ejecutan paquetes para usar una cuenta de proxy con privilegios limitados o agregar solo los miembros de **sysadmin** a los roles **db_ssisadmin** y **dc_admin** .  

## <a name="working-with-r-services"></a>Trabajo con R Services  

**Se aplica a:** SQL Server a partir de [!INCLUDE[ssSQLv14_md](../../../includes/sssqlv14-md.md)]   

Si R Services está instalado, hay roles de base de datos adicionales disponibles para administrar paquetes. Para más información, vea [R Package management for SQL Server (Administración de paquetes de R para SQL Server)](../../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md).

|Nombre de rol |Descripción|  
|-------------|-----------------|
|**rpkgs-users** |Permite a los usuarios usar cualquier paquete compartido que los miembros del rol rpkgs-shared hayan instalado.|
|**rpkgs-private** |Proporciona acceso a los paquetes compartidos con los mismos permisos que el rol rpkgs-users. Los miembros de este rol también pueden instalar, quitar y usar paquetes de ámbito privado.|
|**rpkgs-shared** |Proporciona los mismos permisos que el rol rpkgs-private. Los usuarios que son miembros de este rol también pueden instalar o quitar paquetes compartidos.|
  
## <a name="working-with-database-level-roles"></a>Trabajar con roles de nivel de base de datos  
 En la tabla siguiente se explican los comandos, las vistas y las funciones que se usan para trabajar con los roles de nivel de base de datos.  
  
|Característica|Tipo|Descripción|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)|Metadatos|Devuelve la lista de los roles fijos de base de datos.|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)|Metadatos|Muestra los permisos de un rol fijo de base de datos.|  
|[sp_helprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)|Metadatos|Devuelve información acerca de los roles de la base de datos actual.|  
|[sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)|Metadatos|Devuelve información acerca de los miembros de un rol de la base de datos actual.|  
|[sys.database_role_members &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|Metadatos|Devuelve una fila por cada miembro de cada rol de base de datos.|  
|[IS_MEMBER &#40;Transact-SQL&#41;](../../../t-sql/functions/is-member-transact-sql.md)|Metadatos|Indica si el usuario actual es miembro del grupo de Microsoft Windows o del rol de base de datos de SQL Server especificados.|  
|[CREATE ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-role-transact-sql.md)|Comando|Crea un rol de base de datos nuevo en la base de datos actual.|  
|[ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md)|Comando|Cambia el nombre o la pertenencia de un rol de base de datos.|  
|[DROP ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-role-transact-sql.md)|Comando|Quita un rol de la base de datos.|  
|[sp_addrole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)|Comando|Crea un rol de base de datos nuevo en la base de datos actual.|  
|[sp_droprole &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)|Comando|Quita un rol de base de datos de la base de datos actual.|  
|[sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)|Comando|Agrega un usuario de base de datos, un rol de base de datos, un inicio de sesión de Windows o un grupo de Windows a un rol de base de datos en la base de datos actual. Todas las plataformas, salvo [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] , deben usar `ALTER ROLE` en su lugar.|  
|[sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)|Comando|Quita una cuenta de seguridad de un rol de SQL Server de la base de datos actual. Todas las plataformas, salvo [!INCLUDE[ssPDW_md](../../../includes/sspdw-md.md)] , deben usar `ALTER ROLE` en su lugar.|
|[GRANT](../../../t-sql/statements/grant-transact-sql.md)| Permisos | Agrega el permiso a un rol.
|[DENY](../../../t-sql/statements/deny-transact-sql.md)| Permisos | Deniega un permiso a un rol.
|[REVOKE](../../../t-sql/statements/revoke-transact-sql.md)| Permisos | Quita un permiso concedido o denegado anteriormente.
  
  
## <a name="public-database-role"></a>Rol de base de datos public  
 Todos los usuarios de una base de datos pertenecen al rol de base de datos **public** s. Cuando a un usuario no se le han concedido ni denegado permisos específicos para un objeto protegible, el usuario hereda los permisos concedidos a la **función pública** para ese objeto. Los usuarios de base de datos no se pueden quitar del rol **public** . 
  
## <a name="related-content"></a>Contenido relacionado  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
 [Funciones de seguridad &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)  
  
 [Proteger SQL Server](../../../relational-databases/security/securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)  
  
  
