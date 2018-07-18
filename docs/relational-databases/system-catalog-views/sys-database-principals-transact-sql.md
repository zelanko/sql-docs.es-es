---
title: Sys.database_principals (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
caps.latest.revision: 46
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a879dfcc6dd0feb57126574947b51f84261af915
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37995882"
---
# <a name="sysdatabaseprincipals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para cada entidad de seguridad de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre de la entidad de seguridad, único en la base de datos.|  
|**principal_id**|**int**|Id. de la entidad de seguridad, único en la base de datos.|  
|**Tipo**|**char(1)**|Tipo de entidad de seguridad:<br /><br /> A = Rol de aplicación<br /><br /> C = Usuario asignado a un certificado<br /><br /> E = usuario externo de Azure Active Directory<br /><br /> G = Grupo de Windows<br /><br /> K = Usuario asignado a una clave asimétrica<br /><br /> R = Rol de base de datos<br /><br /> S = Usuario de SQL<br /><br /> U = Usuario de Windows<br /><br /> X = grupo externo desde aplicaciones o el grupo de Azure Active Directory|  
|**type_desc**|**nvarchar(60)**|Descripción del tipo de entidad de seguridad.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|Nombre que se utilizará al nombre SQL no especifica un esquema. Null para entidades de seguridad que no son del tipo S, U o A.|  
|**create_date**|**datetime**|Hora en que se creó la entidad de seguridad.|  
|**modify_date**|**datetime**|Hora en que se modificó por última vez la entidad de seguridad.|  
|**owning_principal_id**|**int**|Id. de la entidad de seguridad propietaria de esta entidad de seguridad. Todas las entidades de seguridad excepto Roles de base de datos deben pertenecer a **dbo**.|  
|**SID**|**varbinary(85)**|SID (identificador de seguridad) de la entidad de seguridad.  NULL para SYS e INFORMATION SCHEMAS.|  
|**is_fixed_role**|**bit**|Si es 1, esta fila representa una entrada para uno de los roles fijos de base de datos: db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter.|  
|**authentication_type**|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Tipo de autenticación. Los siguientes son los valores posibles y sus descripciones.<br /><br /> 0: sin autenticación<br />1: autenticación de instancias<br />2: autenticación de base de datos<br />3: autenticación de Windows|  
|**authentication_type_desc definida**|**nvarchar(60)**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Descripción del tipo de autenticación. Los siguientes son los valores posibles y sus descripciones.<br /><br /> NONE: Sin autenticación<br />INSTANCIA: Autenticación de la instancia<br />Base de datos: Autenticación de base de datos de<br />WINDOWS: Autenticación de Windows|  
|**default_language_name**|**sysname**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Idioma predeterminado para esta entidad de seguridad.|  
|**default_language_lcid**|**int**|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> LCID predeterminado para esta entidad de seguridad.|  
|**allow_encrypted_value_modifications**|**bit**|**Se aplica a**: de [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Suprime las comprobaciones de metadatos criptográficos en el servidor en operaciones de copia masiva. Esto permite al usuario a la copia masiva de datos cifrado con Always Encrypted, entre las tablas o bases de datos, sin descifrar los datos. El valor predeterminado es OFF. |      
  
## <a name="remarks"></a>Notas  
 El *PasswordLastSetTime* propiedades están disponibles en todas las configuraciones admitidas de SQL Server, pero las demás propiedades solo están disponibles cuando se ejecuta SQL Server en Windows Server 2003 o posterior y tanto CHECK_POLICY como CHECK_ EXPIRACIÓN están habilitados. Consulte [directiva de contraseñas](../../relational-databases/security/password-policy.md) para obtener más información.  
  
## <a name="permissions"></a>Permisos  
 Cualquier usuario puede ver su propio nombre de usuario, los usuarios del sistema y los roles fijos de base de datos. Para ver otros usuarios, requiere ALTER ANY USER o un permiso en el usuario. Para ver los roles definidos por el usuario, se requiere ALTER ANY ROLE o la pertenencia al rol.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A: Enumerar todos los permisos de entidades de seguridad de base de datos  
 La consulta siguiente enumera los permisos que se otorgan o deniegan específicamente a las entidades de seguridad de base de datos.  
  
> [!IMPORTANT]  
>  Los permisos de roles fijos de base de datos no aparecen en sys.database_permissions. Por tanto, es posible que las entidades de seguridad de base de datos tengan permisos adicionales que no aparezcan aquí.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B: Enumerar permisos para objetos de esquema en una base de datos  
 La consulta siguiente se combina con sys.database_principals y sys.database_permissions para que sys.objects y sys.schemas enumeren los permisos otorgados o denegados a objetos de esquema específicos.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: enumerar todos los permisos de las entidades de seguridad de base de datos  
 La consulta siguiente enumera los permisos que se otorgan o deniegan específicamente a las entidades de seguridad de base de datos.  
  
> [!IMPORTANT]  
>  Los permisos de los roles fijos de base de datos no aparecen en `sys.database_permissions`. Por tanto, es posible que las entidades de seguridad de base de datos tengan permisos adicionales que no aparezcan aquí.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: enumerar los permisos de objetos de esquema dentro de una base de datos  
 La siguiente consulta combinaciones `sys.database_principals` y `sys.database_permissions` a `sys.objects` y `sys.schemas` enumerar los permisos concedidos o denegados a objetos de esquema específico.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="see-also"></a>Vea también  
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Usuarios de base de datos independiente: hacer que la base de datos sea portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


