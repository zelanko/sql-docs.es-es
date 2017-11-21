---
title: "Crear rol de aplicación (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- APPLICATION_ROLE_TSQL
- CREATE APPLICATION ROLE
- sql13.swb.applicationrole.permissions.f1
- APPLICATION
- APPLICATION ROLE
- CREATE_APPLICATION_ROLE_TSQL
- APPLICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE APPLICATION ROLE statement
- application roles [SQL Server], creating
ms.assetid: 647386da-ee80-41cf-86c9-dd590f9d66b6
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 68f185c59672e4414192fc75dbb7bb137800d69f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-application-role-transact-sql"></a>CREATE APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Agrega un rol de aplicación a la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE APPLICATION ROLE application_role_name   
    WITH PASSWORD = 'password' [ , DEFAULT_SCHEMA = schema_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *application_role_name*  
 Especifica el nombre del rol de aplicación. Ninguna entidad de seguridad de la base de datos debe utilizar este nombre.  
  
 CONTRASEÑA **='***contraseña***'**  
 Especifica la contraseña que utilizarán los usuarios de la base de datos para activar el rol de aplicación. Debe utilizar siempre contraseñas seguras. *contraseña* debe cumplir los requisitos de directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 DEFAULT_SCHEMA  **=**  *schema_name*  
 Especifica el primer esquema donde buscará el servidor cuando resuelva los nombres de objetos de este rol. Si DEFAULT_SCHEMA se deja sin definir, el rol de aplicación utilizará DBO como esquema predeterminado. *schema_name* puede ser un esquema que no existe en la base de datos.  
  
## <a name="remarks"></a>Comentarios  
  
> [!IMPORTANT]  
>  Al establecer las contraseñas de los roles de aplicación se comprueba la complejidad de la contraseña. Las aplicaciones que invocan roles de aplicación deben almacenar sus propias contraseñas. Las contraseñas de roles de aplicación deben almacenarse cifradas.  
  
 Roles de aplicación están visibles en el [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) vista de catálogo.  
  
 Para obtener información sobre cómo usar las funciones de aplicación, consulte [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY APPLICATION ROLE en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea un rol de aplicación denominado `weekly_receipts` con la contraseña `987Gbv876sPYY5m23` y con el esquema predeterminado `Sales`.  
  
```  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987G^bv876sPY)Y5m23'   
    , DEFAULT_SCHEMA = Sales;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_setapprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

