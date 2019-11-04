---
title: CREATE APPLICATION ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dc3caf4c1643405cc7db31e2a9c76cf70456b272
ms.sourcegitcommit: e9c1527281f2f3c7c68981a1be94fe587ae49ee9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2019
ms.locfileid: "73064591"
---
# <a name="create-application-role-transact-sql"></a>CREATE APPLICATION ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Agrega un rol de aplicación a la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE APPLICATION ROLE application_role_name   
    WITH PASSWORD = 'password' [ , DEFAULT_SCHEMA = schema_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *application_role_name*  
 Especifica el nombre del rol de aplicación. Ninguna entidad de seguridad de la base de datos debe utilizar este nombre.  
  
 PASSWORD **='** _password_ **'**  
 Especifica la contraseña que utilizarán los usuarios de la base de datos para activar el rol de aplicación. Debe utilizar siempre contraseñas seguras. *password* debe cumplir los requisitos de la directiva de contraseñas de Windows del equipo que ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 DEFAULT_SCHEMA **=** _schema\_name_  
 Especifica el primer esquema donde buscará el servidor cuando resuelva los nombres de objetos de este rol. Si DEFAULT_SCHEMA se deja sin definir, el rol de aplicación utilizará DBO como esquema predeterminado. *schema_name* puede ser un esquema que no exista en la base de datos.  
  
## <a name="remarks"></a>Notas  
  
> [!IMPORTANT]  
>  Al establecer las contraseñas de los roles de aplicación se comprueba la complejidad de la contraseña. Las aplicaciones que invocan roles de aplicación deben almacenar sus propias contraseñas. Las contraseñas de roles de aplicación deben almacenarse cifradas.  
  
 Puede ver los roles de aplicación en la vista de catálogo [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md).  
  
 Para saber más sobre cómo usar roles de aplicación, vea [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY APPLICATION ROLE en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se crea un rol de aplicación denominado `weekly_receipts` con la contraseña `987Gbv876sPYY5m23` y con el esquema predeterminado `Sales`.  
  
```sql  
CREATE APPLICATION ROLE weekly_receipts   
    WITH PASSWORD = '987G^bv876sPY)Y5m23'   
    , DEFAULT_SCHEMA = Sales;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Roles de aplicación](../../relational-databases/security/authentication-access/application-roles.md)   
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [ALTER APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [Directiva de contraseñas](../../relational-databases/security/password-policy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
