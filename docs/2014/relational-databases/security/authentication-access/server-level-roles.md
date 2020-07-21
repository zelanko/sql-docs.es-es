---
title: Roles de nivel de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.Security.BUILTIN.administrators
- sql12.Security.NT_AUTHORITY.SYSTEM
helpviewer_keywords:
- roles [SQL Server], server-level
- principals [SQL Server], server-level
- CONTROL SERVER permission
- fixed server roles [SQL Server]
- credentials [SQL Server], roles
- sysadmin fixed server role
- server-level roles [SQL Server]
- authentication [SQL Server], roles
ms.assetid: 7adf2ad7-015d-4cbe-9e29-abaefd779008
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4e8f2e75eb5272f30153814e923048b4f5c4f8b1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016213"
---
# <a name="server-level-roles"></a>Roles de nivel de servidor
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona roles de nivel de servidor para ayudarle a administrar los permisos de un servidor. Estos roles son entidades de seguridad que agrupan otras entidades de seguridad. Los roles de nivel de servidor se aplican a todo el servidor en lo que respecta a su ámbito de permisos. (Los*roles* son como los *grupos* del sistema operativo Windows).  
  
 Los roles fijos de servidor se proporcionan por comodidad y compatibilidad con versiones anteriores. Siempre que sea posible, asigne permisos más específicos.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona nueve roles fijos de servidor. Los permisos que se conceden a los roles fijos de servidor no se pueden modificar. A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], puede crear roles de servidor definidos por el usuario y agregarles permisos de nivel de servidor.  
  
 Puede agregar entidades de seguridad a nivel de servidor (inicios de sesión de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , cuentas de Windows y grupos de Windows) a los roles de nivel de servidor. Cada miembro de un rol fijo de servidor puede agregar otros inicios de sesión a ese mismo rol. Los miembros de roles de servidor definidos por el usuario no pueden agregar otras entidades de seguridad de servidor al rol.  
  
## <a name="fixed-server-level-roles"></a>Roles fijos de nivel de servidor  
 En la tabla siguiente se muestran los roles fijos de nivel de servidor y sus capacidades.  
  
|Rol fijo de nivel de servidor|Description|  
|------------------------------|-----------------|  
|sysadmin|Los miembros del rol fijo de servidor sysadmin pueden realizar cualquier actividad en el servidor.|  
|serveradmin|Los miembros del rol fijo de servidor serveradmin pueden cambiar las opciones de configuración en el servidor y cerrar el servidor.|  
|securityadmin|Los miembros del rol fijo de servidor securityadmin administran los inicios de sesión y sus propiedades. Administran los permisos de servidor GRANT, DENY y REVOKE. También pueden administrar los permisos de nivel de base de datos GRANT, DENY y REVOKE si tienen acceso a una base de datos. Asimismo, pueden restablecer contraseñas para inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Nota de seguridad la capacidad de conceder acceso a y configurar los permisos de usuario permite que el administrador de seguridad asigne la mayoría de los permisos de servidor. ** \* \* \* \* ** [!INCLUDE[ssDE](../../../includes/ssde-md.md)] El `securityadmin` rol se debe tratar como equivalente al `sysadmin` rol.|  
|processadmin|Los miembros del rol fijo de servidor processadmin pueden finalizar los procesos que se ejecutan en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|setupadmin|Los miembros del rol fijo de servidor setupadmin pueden agregar y quitar servidores vinculados mediante instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)] . (Es necesaria la pertenencia a sysadmin cuando se usa [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]).|  
|bulkadmin|Los miembros del rol fijo de servidor bulkadmin pueden ejecutar la instrucción BULK INSERT.|  
|diskadmin|El rol fijo de servidor diskadmin se utiliza para administrar archivos de disco.|  
|dbcreator|Los miembros del rol fijo de servidor dbcreator pueden crear, modificar, quitar y restaurar cualquier base de datos.|  
|public|Cada inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pertenece al rol público de servidor. Cuando a una entidad de seguridad de servidor no se le han concedido ni denegado permisos específicos para un objeto protegible, el usuario hereda los permisos concedidos al rol pública para ese elemento. Solo asigne los permisos públicos en cualquier objeto cuando desee que el objeto esté disponible para todos los usuarios. No puede cambiar la pertenencia en public.<br /><br /> Nota: public se implementa de manera diferente que otros roles. Pero se pueden conceder, denegar o revocar permisos desde public.|  
  
## <a name="permissions-of-fixed-server-roles"></a>Permisos de los roles fijos de servidor  
 Cada rol fijo de servidor cuenta con diversos permisos asignados. Para obtener un gráfico de los permisos asignados a los roles del servidor, vea [Database Engine Fixed Server and Fixed Database Roles](https://social.technet.microsoft.com/wiki/contents/articles/2024.database-engine-fixed-server-and-fixed-database-roles.aspx).  
  
> [!IMPORTANT]  
>  El permiso `CONTROL SERVER` es similar, pero no idéntico al rol fijo de servidor `sysadmin`. Los permisos no conllevan la pertenencia a los roles y la pertenencia a los roles no otorga permisos. (P. ej., `CONTROL SERVER`no implica la pertenencia al `sysadmin` rol fijo de servidor). Sin embargo, a veces es posible suplantar entre roles y permisos equivalentes. La mayoría de los comandos `DBCC` y muchos procedimientos del sistema necesitan pertenencia al rol fijo de servidor `sysadmin`. Para obtener una lista de los procedimientos almacenados del sistema 171 que requieren `sysadmin` pertenencia, consulte la siguiente entrada de blog de Andreas Wolter [Control Server vs. sysadmin/SA: permisos, procedimientos del sistema, DBCC, creación automática de esquemas y escalado de privilegios: ADVERTENCIAS](http://www.insidesql.org/blogs/andreaswolter/2013/08/control-server-vs-sysadmin-sa-permissions-privilege-escalation-caveats).  
  
## <a name="server-level-permissions"></a>Permisos de nivel de servidor  
 Solo se pueden agregar a los roles de servidor definidos por el usuario los permisos de nivel de servidor. Para obtener una lista de los permisos en el nivel de servidor, ejecute la siguiente instrucción: Los permisos en el nivel de servidor son:  
  
```sql  
SELECT * FROM sys.fn_builtin_permissions('SERVER') ORDER BY permission_name;  
```  
  
 Para obtener más información sobre los permisos, vea [Permisos &#40;motor de base de datos&#41;](../permissions-database-engine.md) y [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql).  
  
## <a name="working-with-server-level-roles"></a>Trabajar con roles de nivel de servidor  
 En la tabla siguiente se explican los comandos, las vistas y las funciones que se pueden utilizar para trabajar con roles de nivel de servidor.  
  
|Característica|Tipo|Description|  
|-------------|----------|-----------------|  
|[sp_helpsrvrole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql)|Metadatos|Devuelve una lista de roles de nivel de servidor.|  
|[sp_helpsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql)|Metadatos|Devuelve información acerca de los miembros de un rol de nivel de servidor.|  
|[sp_srvrolepermission &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql)|Metadatos|Muestra los permisos de un rol de nivel de servidor.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|Metadatos|Indica si un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es miembro del rol de nivel de servidor especificado.|  
|[sys.server_role_members &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-role-members-transact-sql)|Metadatos|Devuelve una fila por cada miembro de cada rol de nivel de servidor.|  
|[sp_addsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql)|Get-Help|Agrega un inicio de sesión como miembro de un rol de nivel de servidor. En desuso. Utilice [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) en su lugar.|  
|[sp_dropsrvrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql)|Get-Help|Quita un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o un usuario o grupo de Windows de un rol de nivel de servidor. En desuso. Utilice [ALTER SERVER ROLE](/sql/t-sql/statements/alter-server-role-transact-sql) en su lugar.|  
|[CREATE SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-role-transact-sql)|Get-Help|Crea un rol de servidor definido por el usuario.|  
|[ALTER SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-role-transact-sql)|Get-Help|Cambia la pertenencia de un rol de servidor o cambia el nombre de un rol de servidor definido por el usuario.|  
|[DROP SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-role-transact-sql)|Get-Help|Quita un rol de servidor definido por el usuario.|  
|[IS_SRVROLEMEMBER &#40;Transact-SQL&#41;](/sql/t-sql/functions/is-srvrolemember-transact-sql)|Función|Determina la pertenencia del rol de servidor.|  
  
## <a name="see-also"></a>Consulte también  
 [Roles de nivel de base de datos](../authentication-access/database-level-roles.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)   
 [Funciones de seguridad &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)   
 [Proteger SQL Server](../securing-sql-server.md)   
 [GRANT &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](/sql/t-sql/statements/grant-server-principal-permissions-transact-sql)   
 [REVOKE &#40;permisos de entidad de seguridad de servidor de Transact-SQL&#41;](/sql/t-sql/statements/revoke-server-principal-permissions-transact-sql)   
 [DENY permisos de entidad de seguridad de servidor &#40;Transact-SQL&#41;](/sql/t-sql/statements/deny-server-principal-permissions-transact-sql)   
 [Crear un rol de servidor](../authentication-access/create-a-server-role.md)  
  
  
