---
title: ROL ALTER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROLE_TSQL
- ALTER ROLE
dev_langs:
- TSQL
helpviewer_keywords:
- modifying database roles
- ALTER ROLE statement
- renaming database roles
- database roles [SQL Server], modifying
- names [SQL Server], database roles
ms.assetid: e1e83caa-17cc-4871-b2db-2711339fb64f
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3eaee2d346eda964545caa60cd7168b531f47ad9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Agrega o quita los miembros de un rol de base de datos o cambia el nombre de un rol de base de datos definido por el usuario.  
  
> [!NOTE]  
>  Para modificar los roles en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_addrolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) y [sp_droprolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server (starting with 2012) and Azure SQL Database  
  
ALTER ROLE  role_name  
{  
       ADD MEMBER database_principal  
    |  DROP MEMBER database_principal  
    |  WITH NAME = new_name  
}  
[;]  
```  
  
 
```  
-- Syntax for SQL Server 2008 only  
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *role_name*  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2008),  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica el rol de base de datos para cambiar.  
  
 Agregar miembro *database_principal*l  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2012),  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica que se agregue la entidad de seguridad de base de datos a la pertenencia de un rol de base de datos.  
  
-   *database_principal* es un usuario de base de datos o un rol de base de datos definido por el usuario.  
  
-   *database_principal* no puede ser un rol fijo de base de datos o una entidad de seguridad de servidor.  
  
DROP MEMBER *database_principal*  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2012),  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica que se quite una entidad de seguridad de base de datos de la pertenencia de un rol de base de datos.  
  
-   *database_principal* es un usuario de base de datos o un rol de base de datos definido por el usuario.  
  
-   *database_principal* no puede ser un rol fijo de base de datos o una entidad de seguridad de servidor.  
  
CON nombre = *new_name*  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2008),  [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica que se cambie el nombre de un rol de base de datos definido por el usuario. El nuevo nombre no debe existir ya en la base de datos.  
  
 El cambio de nombre de un rol de base de datos no modifica el número de identificación, el propietario, ni los permisos del rol.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este comando necesita uno o varios de estos permisos o las pertenencias a grupos:  
  
-   **ALTER** permiso para el rol  
-   **ALTER ANY ROLE** permiso en la base de datos  
-   Pertenencia en el **db_securityadmin** rol fijo de base de datos  
  
Además, para cambiar la pertenencia a un rol fijo de base de datos debe:  
  
-   Pertenencia en el **db_owner** rol fijo de base de datos  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede cambiar el nombre de un rol fijo de base de datos.  
  
## <a name="metadata"></a>Metadatos  
 Estas vistas del sistema contienen información sobre los roles de base de datos y las entidades de seguridad de base de datos.  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. Cambiar el nombre de un rol de base de datos  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2008),  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 En el ejemplo siguiente se cambia el nombre del rol `buyers` a `purchasing`. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. Agregar o quitar a miembros del rol  
 **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2012),  [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 Este ejemplo crea un rol de base de datos denominado `Sales`. Agrega un usuario de base de datos denominado a Barry a la pertenencia y, a continuación, se muestra cómo quitar el miembro Barry. [!INCLUDE[AdWorks-example](../../includes/adworks-example-md.md)]  
  
```tsql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear rol &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [ELIMINAR rol &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  

