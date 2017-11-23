---
title: "Permisos de clave simétrica de GRANT (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], permissions
- permissions [SQL Server], symmetric keys
- encryption [SQL Server], symmetric keys
- GRANT statement, symmetric keys
- cryptography [SQL Server], symmetric keys
- granting permissions [SQL Server], symmetric keys
ms.assetid: 5c61557f-67ae-4e55-b86d-713575b27cea
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a80cd14f583074fa4d4d605c9f38b3df671d436d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="grant-symmetric-key-permissions-transact-sql"></a>GRANT (permisos de clave simétrica de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permisos para una clave simétrica. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GRANT permission [ ,...n ]    
    ON SYMMETRIC KEY :: symmetric_key_name   
    TO <database_principal> [ ,...n ] [ WITH GRANT OPTION ]  
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
 Especifica un permiso que se puede conceder para una clave simétrica. Para obtener una lista de permisos, vea la sección Comentarios que se muestra posteriormente en este tema.  
  
 CLAVE SIMÉTRICA de ON::*asymmetric_key_name*  
 Especifica la clave simétrica en la que se va a conceder el permiso. Se requiere el calificador de ámbito (::).  
  
 PARA \< *database_principal*>  
 Especifica la entidad de seguridad para la que se concede el permiso.  
  
 WITH GRANT OPTION  
 Indica que la entidad de seguridad también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
 AS \<database_principal > especifica una entidad de seguridad de la que la entidad de seguridad para ejecutar esta consulta deriva su derecho a conceder el permiso.  
  
 *Database_user*  
 Especifica un usuario de base de datos.  
  
 *Database_role*  
 Especifica un rol de base de datos.  
  
 *Application_role*  
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
 Información acerca de las claves simétricas está visible en el [sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) vista de catálogo.  
  
 Una clave simétrica es un elemento protegible de nivel de base de datos que contiene la base de datos que es su entidad primaria en la jerarquía de permisos. La mayoría de permisos limitados y específicos que se pueden conceder para una clave simétrica se muestran en la siguiente tabla, junto con permisos más generales que los incluyen por implicación.  
  
|Permiso de clave simétrica|Implícito en el permiso de clave simétrica|Implícito en el permiso de base de datos|  
|------------------------------|-----------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SYMMETRIC KEY|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder.  
  
 Si utiliza la opción AS, se aplican los siguientes requisitos adicionales.  
  
|AS *granting_principal*|Permiso adicional necesario|  
|------------------------------|------------------------------------|  
|Usuario de la base de datos|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un inicio de sesión de Windows|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un grupo de Windows|Pertenencia al grupo de Windows, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a un certificado|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos asignado a una clave asimétrica|Pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Usuario de la base de datos no asignado a una entidad de seguridad del servidor|Permiso IMPERSONATE para el usuario, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de base de datos|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
|Rol de aplicación|Permiso ALTER para el rol, pertenencia al rol fijo de base de datos db_securityadmin, pertenencia al rol fijo de base de datos db_owner o pertenencia al rol fijo de servidor sysadmin.|  
  
 Las entidades de seguridad con permiso CONTROL sobre un elemento protegible pueden conceder permisos para ese elemento.  
  
 Los receptores del permiso CONTROL SERVER como los miembros del rol fijo de servidor sysadmin pueden conceder los permisos sobre cualquier elemento protegible en el servidor. Los receptores del permiso CONTROL para una base de datos, como los miembros del rol fijo de base de datos db_owner, pueden conceder los permisos para cualquier elemento protegible en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se concede el permiso `ALTER` para la clave simétrica `SamInventory42` al usuario de base de datos `HamidS`.  
  
```  
USE AdventureWorks2012;  
GRANT ALTER ON SYMMETRIC KEY::SamInventory42 TO HamidS;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.symmetric_keys &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [DENEGAR permisos de clave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)   
 [REVOCAR permisos de clave simétrica &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

