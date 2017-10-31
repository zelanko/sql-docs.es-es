---
title: CONCEDER permisos de entidad de seguridad de base de datos (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/12/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- permissions [SQL Server], database roles
- granting permissions [SQL Server], database users
- granting permissions [SQL Server], application roles
- granting permissions [SQL Server], database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- GRANT statement, users
- GRANT statement, roles
- application roles [SQL Server], permissions
ms.assetid: 012588a2-cbe1-48f0-a731-b4a2b83203d5
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a2d78167459a509d788e65ad31d4660298107558
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="grant-database-principal-permissions-transact-sql"></a>GRANT (permisos de entidad de seguridad de base de datos de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concede permisos a un usuario de base de datos, un rol de base de datos o un rol de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
GRANT permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
    TO <database_principal> [ ,...n ]  
       [ WITH GRANT OPTION ]  
       [ AS <database_principal> ]  
  
<database_principal> ::=  
    Database_user   
  | Database_role   
  | Application_role   
  | Database_user_mapped_to_Windows_User   
  | Database_user_mapped_to_Windows_Group   
  | Database_user_mapped_to_certificate   
  | Database_user_mapped_to_asymmetric_key   
  | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>Argumentos  
 *permiso*  
 Especifica un permiso que se puede conceder para la entidad de seguridad de base de datos. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 USUARIO::*database_user*  
 Especifica la clase y nombre del usuario en el que se concede el permiso. Se requiere el calificador de ámbito (::).  
  
 ROL::*database_role*  
 Especifica la clase y nombre del rol en el que se concede el permiso. Se requiere el calificador de ámbito (::).  
  
 ROL de aplicación::*application_role*  
   
 Especifica la clase y nombre del rol de aplicación en el que se concede el permiso. Se requiere el calificador de ámbito (::).  
  
 WITH GRANT OPTION  
 Indica que la entidad de seguridad también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
 AS \<database_principal >  
 Especifica una entidad de seguridad de la que la entidad de seguridad que ejecuta esta consulta deriva su derecho de conceder el permiso.  
  
 *Database_user*  
 Especifica un usuario de base de datos.  
  
 *Database_role*  
 Especifica un rol de base de datos.  
  
 *Application_role*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica un rol de aplicación.  
  
 *Database_user_mapped_to_Windows_User*  
 Especifica un usuario de base de datos asignado a un usuario de Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
  
 Especifica un usuario de base de datos asignado a un grupo de Windows.  
  
 *Database_user_mapped_to_certificate*  
  
 Especifica un usuario de base de datos asignado a un certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
  
 Especifica un usuario de base de datos asignado a una clave asimétrica.  
  
 *Database_user_with_no_login*  
 Especifica un usuario de base de datos sin entidad de seguridad de servidor correspondiente.  
  
## <a name="remarks"></a>Comentarios  
 Información acerca de las entidades de base de datos está visible en el [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) vista de catálogo. Información acerca de los permisos de nivel de base de datos está visible en el [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) vista de catálogo.  
  
## <a name="database-user-permissions"></a>Permisos de usuario de base de datos  
 Un usuario de base de datos es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. La mayoría de permisos limitados y específicos que se pueden conceder a un usuario de base de datos se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de usuario de base de datos|Implícito en el permiso de usuario de base de datos|Implícito en el permiso de base de datos|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>Permisos de rol de base de datos  
 Un rol de base de datos es un elemento protegible de nivel de base de datos contenido en la base de datos que es su entidad primaria en la jerarquía de permisos. Los permisos más específicos y limitados que se pueden conceder a un rol de base de datos se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de rol de base de datos|Implícito en el permiso de rol de base de datos|Implícito en el permiso de base de datos|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>Permisos de rol de aplicación  
 Un rol de aplicación es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. Los permisos más específicos y limitados que se pueden conceder para un rol de aplicación se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de rol de aplicación|Implícito en el permiso de rol de aplicación|Implícito en el permiso de base de datos|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder.  
  
 Si utiliza la opción AS, se aplican los siguientes requisitos adicionales.  
  
|AS *granting_principal*|Permiso adicional necesario|  
|------------------------------|------------------------------------|  
|Usuario de la base de datos|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un usuario de Windows|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un grupo de Windows|Pertenencia al grupo de Windows, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un certificado|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a una clave asimétrica|Pertenecer al rol de base de datos db_securityadminfixed, pertenencia al rol db_owner rol fijo de base de datos o pertenencia en el rol fijo de servidor sysadmin.|  
|Usuario de la base de datos no asignado a una entidad de seguridad del servidor|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de base de datos|Modifique los permisos del rol, pertenencia al rol de base de datos db_securityadminfixed, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de aplicación|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
  
 Las entidades de seguridad que tienen el permiso CONTROL para un elemento protegible pueden conceder permisos para ese elemento.  
  
 Los receptores del permiso CONTROL para una base de datos, como los miembros del rol fijo de base de datos db_owner, pueden conceder los permisos para cualquier elemento protegible en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-granting-control-permission-on-a-user-to-another-user"></a>A. Conceder el permiso CONTROL sobre un usuario a otro usuario  
 En el siguiente ejemplo se concede el permiso `CONTROL` para el usuario `AdventureWorks2012` de `Wanida` al usuario `RolandX`.  
  
```  
GRANT CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-granting-view-definition-permission-on-a-role-to-a-user-with-grant-option"></a>B. Conceder el permiso VIEW DEFINITION sobre un rol a un usuario con GRANT OPTION  
 En el siguiente ejemplo se concede el permiso `VIEW DEFINITION` para el rol `AdventureWorks2012` de `SammamishParking` junto con `GRANT OPTION` al usuario de base de datos `JinghaoLiu`.  
  
```  
GRANT VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-impersonate-permission-on-a-user-to-an-application-role"></a>C. Conceder el permiso IMPERSONATE sobre un usuario a un rol de aplicación  
 En el siguiente ejemplo se concede el permiso `IMPERSONATE` para el usuario `HamithaL` al rol de aplicación `AdventureWorks2012` de `AccountsPayable17`.  
  
**Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
```  
GRANT IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>Vea también  
 [DENEGAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [REVOCAR permisos de entidad de seguridad de base de datos &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [Sys.database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Crear rol de aplicación &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Crear rol &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

