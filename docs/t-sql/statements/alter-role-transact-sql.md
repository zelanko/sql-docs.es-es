---
title: ALTER ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b24129d26523ec4bee866c96180c0907992099e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47760273"
---
# <a name="alter-role-transact-sql"></a>ALTER ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Agrega o quita miembros en un rol de base de datos o cambia el nombre de un rol de base de datos definido por el usuario.  
  
> [!NOTE]  
>  Para modificar roles o para agregar o quitar miembros en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) y [sp_droprolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md).  
  
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
-- Syntax for SQL Server 2008, Azure SQL Data Warehouse and Parallel Data Warehouse
  
-- Change the name of a user-defined database role  
ALTER ROLE role_name   
    WITH NAME = new_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *role_name*  
 **SE APLICA A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2008), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica el rol de base de datos que cambiar.  
  
 ADD MEMBER *database_principal*l  
 **SE APLICA A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2012), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica que se agregue la entidad de seguridad de base de datos a la pertenencia de un rol de base de datos.  
  
-   *database_principal* es un usuario de base de datos o un rol de base de datos definido por el usuario.  
  
-   *database_principal* no puede ser un rol fijo de base de datos ni una entidad de seguridad del servidor.  
  
DROP MEMBER *database_principal*  
 **SE APLICA A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2012), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica que se quite la entidad de seguridad de base de datos de la pertenencia de un rol de base de datos.  
  
-   *database_principal* es un usuario de base de datos o un rol de base de datos definido por el usuario.  
  
-   *database_principal* no puede ser un rol fijo de base de datos ni una entidad de seguridad del servidor.  
  
WITH NAME = *new_name*  
 **SE APLICA A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2008), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 Especifica que se cambie el nombre de un rol de base de datos definido por el usuario. El nuevo nombre no debe existir en la base de datos.  
  
 El cambio de nombre de un rol de base de datos no modifica el número de identificación, el propietario, ni los permisos del rol.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este comando, se necesitan uno o varios de los siguientes permisos o pertenencias a grupos:  
  
-   Permiso **ALTER** en el rol  
-   Permiso **ALTER ANY ROLE** en la base de datos  
-   Pertenencia al rol fijo de base de datos **db_securityadmin**  
  
Además, para cambiar la pertenencia a un rol fijo de base de datos, se necesita lo siguiente:  
  
-   Pertenencia al rol fijo de base de datos **db_owner**  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 El nombre de los roles fijos de base de datos no se puede cambiar.  
  
## <a name="metadata"></a>Metadatos  
 Estas vistas del sistema contienen información sobre los roles de base de datos y las entidades de seguridad de las base de datos.  
  
-   [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)  
  
-   [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-change-the-name-of-a-database-role"></a>A. Cambiar el nombre de un rol de base de datos  
 **SE APLICA A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2008), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 En el ejemplo siguiente se cambia el nombre del rol `buyers` a `purchasing`.   Este ejemplo se puede ejecutar en la base de datos de ejemplo [AdventureWorks](http://msftdbprodsamples.codeplex.com/).
  
```sql  
ALTER ROLE buyers WITH NAME = purchasing;  
```  
  
### <a name="b-add-or-remove-role-members"></a>B. Agregar o quitar a miembros del rol  
 **SE APLICA A:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de 2012), [!INCLUDE[ssSDS](../../includes/sssds-md.md)]  
  
 En este ejemplo se crea el rol de base de datos `Sales`. Se agrega un usuario de base de datos denominado Barry a la pertenencia y, luego, se indica cómo quitar el miembro Barry.   Este ejemplo se puede ejecutar en la base de datos de ejemplo [AdventureWorks](http://msftdbprodsamples.codeplex.com/).
  
```sql  
CREATE ROLE Sales;  
ALTER ROLE Sales ADD MEMBER Barry;  
ALTER ROLE Sales DROP MEMBER Barry;  
```  
  
## <a name="see-also"></a>Ver también  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)  
  
  
