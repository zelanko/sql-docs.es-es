---
title: Roles de nivel de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 09/22/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server 2014
f1_keywords:
- sql12.swb.roleproperties.database.f1
- sql12.swb.roleproperties.general.f1
- sql12.swb.roleproperties.object.f1
- SQL12.SWB.DBROLEPROPERTIES.GENERAL.F1
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
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 337252b4b5203003bc6bec6b44b12d86183ab343
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188062"
---
# <a name="database-level-roles"></a>Roles de nivel de base de datos
  Para administrar con facilidad los permisos en las bases de datos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona varios *roles* , que son las entidades de seguridad que agrupan a otras entidades de seguridad. Son como los ***grupos*** del sistema operativo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Los roles de nivel de base de datos se aplican a toda la base de datos en lo que respecta a su ámbito de permisos.  
  
 Existen dos tipos de roles de nivel de base de datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: los *roles fijos de base de datos* , que están predefinidos en la base de datos, y los *roles flexibles de base de datos* , que pueden crearse.  
  
 Los roles fijos de base de datos se definen en el nivel de base de datos y existen en cada una de ellas. Los miembros de los roles de base de datos **db_owner** pueden administrar la pertenencia a roles fijos de base de datos. Hay también algunos roles fijos de base de datos con fines especiales en la base de datos msdb.  
  
 Puede agregar cualquier cuenta de la base de datos y otros roles de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a los roles de nivel de base de datos. Cada miembro de un rol fijo de base de datos puede agregar otros inicios de sesión a ese mismo rol.  
  
> [!IMPORTANT]  
>  No agregue roles flexibles de la base de datos como miembros de roles fijos. Esto podría habilitar un aumento de privilegios no deseado.  
  
 En la tabla siguiente se muestran los roles fijos de nivel de base de datos y sus capacidades. Estos roles existen en todas las bases de datos.  
  
|Nombre de rol de nivel de base de datos|Descripción|  
|-------------------------------|-----------------|  
|**db_owner**|Los miembros del rol fijo de base de datos **db_owner** pueden realizar todas las actividades de configuración y mantenimiento en la base de datos y también pueden quitar la base de datos.|  
|**db_securityadmin**|Los miembros del rol fijo de base de datos **db_securityadmin** pueden modificar la pertenencia a roles y administrar permisos. Si se agregan entidades de seguridad a este rol, podría habilitarse un aumento de privilegios no deseado.|  
|**db_accessadmin**|Los miembros del rol fijo de base de datos **db_accessadmin** pueden agregar o quitar el acceso a la base de datos para inicios de sesión de Windows, grupos de Windows e inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|**db_backupoperator**|Los miembros del rol fijo de base de datos **db_backupoperator** pueden crear copias de seguridad de la base de datos.|  
|**db_ddladmin**|Los miembros del rol fijo de base de datos **db_ddladmin** pueden ejecutar cualquier comando del lenguaje de definición de datos (DDL) en una base de datos.|  
|**db_datawriter**|Los miembros del rol fijo de base de datos **db_datawriter** pueden agregar, eliminar o cambiar datos en todas las tablas de usuario.|  
|**db_datareader**|Los miembros del rol fijo de base de datos **db_datareader** pueden leer todos los datos de todas las tablas de usuario.|  
|**db_denydatawriter**|Los miembros del rol fijo de base de datos **db_denydatawriter** no pueden agregar, modificar ni eliminar datos de tablas de usuario de una base de datos.|  
|**db_denydatareader**|Los miembros del rol fijo de base de datos **db_denydatareader** no pueden leer datos de las tablas de usuario dentro de una base de datos.|  
  
## <a name="msdb-roles"></a>Roles de msdb  
 La base de datos msdb contiene los roles con fines especiales que se muestran en la tabla siguiente.  
  
|Nombre de rol de msdb|Descripción|  
|--------------------|-----------------|  
|`db_ssisadmin`<br /><br /> **db_ssisoperator**<br /><br /> **db_ssisltduser**|Los miembros de estos roles de base de datos pueden administrar y utilizar [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se actualizan desde una versión anterior podrían contener una versión anterior del rol cuya denominación se realizaba al usar Servicios de transformación de datos (DTS) en lugar de [!INCLUDE[ssIS](../../../includes/ssis-md.md)]. Para obtener más información, vea [Roles de Integration Services &#40;servicio SSIS&#41;](../../../integration-services/security/integration-services-roles-ssis-service.md).|  
|`dc_admin`<br /><br /> **dc_operator**<br /><br /> **dc_proxy**|Los miembros de estos roles de base de datos pueden administrar y utilizar el recopilador de datos. Para obtener más información, consulte [Data Collection](../../data-collection/data-collection.md).|  
|**PolicyAdministratorRole**|Los miembros del rol de base de datos **db_ PolicyAdministratorRole** pueden realizar todas las actividades de mantenimiento y configuración en las condiciones y directivas de Administración basada en directivas. Para obtener más información, vea [Administrar servidores mediante administración basada en directivas](../../policy-based-management/administer-servers-by-using-policy-based-management.md).|  
|**ServerGroupAdministratorRole**<br /><br /> **ServerGroupReaderRole**|Los miembros de estos roles de base de datos pueden administrar y utilizar grupos de servidores registrados.|  
|**dbm_monitor**|Creado en el `msdb` cuando se registra la primera base de datos en el Monitor de creación de reflejo de base de datos de la base de datos. El rol **dbm_monitor** no tiene miembros hasta que un administrador del sistema asigna usuarios al rol.|  
  
> [!IMPORTANT]  
>  Los miembros del rol db_ssisadmin y del rol dc_admin quizá puedan elevar sus privilegios a sysadmin. Esta elevación de privilegio se puede producir porque estos roles pueden modificar los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] y los paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] los puede ejecutar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el contexto de seguridad de sysadmin del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para protegerse contra esta elevación de privilegio al ejecutar planes de mantenimiento, conjuntos de recopilación de datos y otros paquetes de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], configure los trabajos del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que ejecutan paquetes para utilizar una cuenta de proxy con privilegios limitados o agregar solo los miembros de sysadmin a los roles dc_admin y db_ssisadmin.  
  
## <a name="working-with-database-level-roles"></a>Trabajar con roles de nivel de base de datos  
 En la tabla siguiente se explican los comandos, las vistas y las funciones que se usan para trabajar con los roles de nivel de base de datos.  
  
|Característica|Tipo|Descripción|  
|-------------|----------|-----------------|  
|[sp_helpdbfixedrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql)|Metadatos|Devuelve la lista de los roles fijos de base de datos.|  
|[sp_dbfixedrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql)|Metadatos|Muestra los permisos de un rol fijo de base de datos.|  
|[sp_helprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprole-transact-sql)|Metadatos|Devuelve información acerca de los roles de la base de datos actual.|  
|[sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql)|Metadatos|Devuelve información acerca de los miembros de un rol de la base de datos actual.|  
|[sys.database_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-role-members-transact-sql)|Metadatos|Devuelve una fila por cada miembro de cada rol de base de datos.|  
|[IS_MEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-member-transact-sql)|Metadatos|Indica si el usuario actual es miembro del grupo de Microsoft Windows o del rol de base de datos de SQL Server especificados.|  
|[CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql)|Comando|Crea un rol de base de datos nuevo en la base de datos actual.|  
|[ALTER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-role-transact-sql)|Comando|Cambia el nombre de un rol de base de datos.|  
|[DROP ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-role-transact-sql)|Comando|Quita un rol de la base de datos.|  
|[sp_addrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrole-transact-sql)|Comando|Crea un rol de base de datos nuevo en la base de datos actual.|  
|[sp_droprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprole-transact-sql)|Comando|Quita un rol de base de datos de la base de datos actual.|  
|[sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)|Comando|Agrega un usuario de base de datos, un rol de base de datos, un inicio de sesión de Windows o un grupo de Windows a un rol de base de datos en la base de datos actual.|  
|[sp_droprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql)|Comando|Quita una cuenta de seguridad de un rol de SQL Server de la base de datos actual.|  
  
## <a name="public-database-role"></a>Rol de base de datos public  
 Todos los usuarios de una base de datos pertenecen al rol de base de datos **public** s. Cuando a un usuario no se le han concedido ni denegado permisos específicos para un objeto protegible, el usuario hereda los permisos concedidos a la **función pública** para ese objeto.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)  
  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/security-stored-procedures-transact-sql)  
  
 [Funciones de seguridad &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)  
  
 [Proteger SQL Server](../securing-sql-server.md)  
  
 [sp_helprotect &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprotect-transact-sql)  
  
  
