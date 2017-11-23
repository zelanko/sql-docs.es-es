---
title: sp_helpuser (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpuser
- sp_helpuser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7fce035be3ddb7e61f9a8f4af34645c30e8a16e6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpuser-transact-sql"></a>sp_helpuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información acerca de las entidades de seguridad de base de datos en la base de datos actual.  
  
> [!IMPORTANT]  
>  **sp_helpuser** no devuelve información sobre elementos protegibles que se introdujeron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Use [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) en su lugar.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name_in_db =** ] **'***security_account***'**  
 Es el nombre de un usuario o un rol de la base de datos actual. *security_account* debe existir en la base de datos actual. *security_account* es **sysname**, su valor predeterminado es null. Si *security_account* no se especifica, **sp_helpuser** devuelve información acerca de todas las entidades de base de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 La siguiente tabla muestra el conjunto de resultados cuando ninguna de ellas una cuenta de usuario ni una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o usuario de Windows se especifica para *security_account*.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**UserName**|**sysname**|Usuarios en la base de datos actual.|  
|**RoleName**|**sysname**|Roles a los que **nombre de usuario** pertenece.|  
|**LoginName**|**sysname**|Inicio de sesión de **nombre de usuario**.|  
|**DefDBName**|**sysname**|Base de datos predeterminada **nombre de usuario**.|  
|**DefSchemaName**|**sysname**|Esquema predeterminado del usuario de la base de datos.|  
|**UserID**|**smallint**|Id. de **nombre de usuario** en la base de datos actual.|  
|**SID**|**smallint**|Número de identificación de seguridad del usuario (SID).|  
  
 En la siguiente tabla se muestra el conjunto de resultados cuando no se especifica una cuenta de usuario y existen alias en la base de datos actual.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|Inicios de sesión asociados con los usuarios en la base de datos actual.|  
|**UserNameAliasedTo**|**sysname**|Nombre de usuario en la base de datos actual al que está asociado el inicio de sesión.|  
  
 La siguiente tabla muestra el conjunto de resultados cuando se especifica un rol para *security_account*.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Role_name**|**sysname**|Nombre del rol en la base de datos actual.|  
|**Role_id**|**smallint**|Id. de rol para el rol en la base de datos actual.|  
|**Users_in_role**|**sysname**|Miembro del rol en la base de datos actual.|  
|**Identificador de usuario**|**smallint**|Id. de usuario para el miembro del rol.|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener información acerca de la pertenencia de roles de base de datos, use [sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md). Para obtener información acerca de los miembros del rol de servidor, use [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)y para obtener información acerca de las entidades de nivel de servidor, use [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
 La información mostrada está sometida a restricciones de acceso a los metadatos. No se mostrarán las entidades en las que la entidad de seguridad no tiene permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-users"></a>A. Presentar todos los usuarios  
 En el siguiente ejemplo se presentan todos los usuarios de la base de datos actual.  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. Presentar información de un solo usuario  
 En el siguiente ejemplo se presenta información acerca del propietario de la base de datos del usuario (`dbo`).  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. Presentar información de un rol de base de datos  
 En el siguiente ejemplo se presenta información acerca del rol fijo de base de datos `db_securityadmin`.  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguridad almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
