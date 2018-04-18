---
title: sp_helprotect (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helprotect
- sp_helprotect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprotect
ms.assetid: faaa3e40-1c95-43c2-9fdc-c61a1d3cc0c3
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3e0942b8d2b66a76db9e50616f63d6d7a3cc959e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelprotect-transact-sql"></a>sp_helprotect (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve un informe con información acerca de los permisos de usuario para un objeto o los permisos de una instrucción en la base de datos actual.  
  
> [!IMPORTANT]  
>  **sp_helprotect** no devuelve información sobre elementos protegibles que se introdujeron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Use [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) y [fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) en su lugar.  
  
 No muestra los permisos que se asignan siempre a los roles fijos de servidor o a los roles fijos de base de datos. No incluye los inicios de sesión o los usuarios que reciben los permisos en función de su pertenencia a un rol.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helprotect [ [ @name = ] 'object_statement' ]   
     [ , [ @username = ] 'security_account' ]   
     [ , [ @grantorname = ] 'grantor' ]   
     [ , [ @permissionarea = ] 'type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name =** ] **'***object_statement***'**  
 Es el nombre del objeto de la base de datos actual, o una instrucción, cuyos permisos se van a presentar. *el argumento object_statement* es **nvarchar(776)**, su valor predeterminado es null, que devuelve todos los permisos de objetos e instrucciones. Si el valor es un objeto (tabla, vista, procedimiento almacenado o procedimiento almacenado extendido), tiene que ser un objeto válido de la base de datos actual. El nombre del objeto puede incluir un calificador de propietario en el formulario *propietario***.*** objeto*.  
  
 Si *object_statement* es una instrucción puede ser una instrucción CREATE.  
  
 [  **@username =** ] **'***security_account***'**  
 Es el nombre de la entidad de seguridad para la que se muestran los permisos. *security_account* es **sysname**, su valor predeterminado es null, que devuelve todas las entidades de la base de datos actual. *security_account* debe existir en la base de datos actual.  
  
 [  **@grantorname =** ] **'***otorgante de permisos***'**  
 Es el nombre de la entidad de seguridad que ha concedido los permisos. *otorgante de permisos* es **sysname**, su valor predeterminado es null, que devuelve toda la información de permisos concedidos por la entidad de seguridad de la base de datos.  
  
 [  **@permissionarea =** ] **'***tipo***'**  
 Es una cadena de caracteres que indica si se muestran los permisos de objeto (cadena de caracteres **o**), los permisos de instrucción (cadena de caracteres **s**), o ambos (**os**). *tipo de* es **varchar (10)**, su valor predeterminado es **os**. *tipo de* puede ser cualquier combinación de **o** y **s**, con o sin comas o espacios en blanco entre **o** y **s**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Propietario**|**sysname**|Nombre del propietario del objeto.|  
|**Objeto**|**sysname**|Nombre del objeto.|  
|**receptor**|**sysname**|Nombre de la entidad de seguridad en la que se conceden los permisos.|  
|**Otorgante de permisos**|**sysname**|Nombre de la entidad de seguridad que ha concedido los permisos al receptor de permisos especificado.|  
|**ProtectType**|**nvarchar (10)**|Nombre del tipo de protección:<br /><br /> GRANT REVOKE|  
|**Acción**|**nvarchar(60)**|Nombre del permiso. Las instrucciones válidas de permisos dependen del tipo de objeto.|  
|**Columna**|**sysname**|Tipo de permiso:<br /><br /> All = Permiso sobre todas las columnas actuales del objeto.<br /><br /> New = Permiso sobre las nuevas columnas del objeto que se pueden cambiar (mediante la instrucción ALTER) posteriormente.<br /><br /> All+New = Combinación de Todas y Nuevas.<br /><br /> Devuelve un punto si el tipo de permiso no se aplica a las columnas.|  
  
## <a name="remarks"></a>Comentarios  
 Todos los parámetros del siguiente procedimiento son opcionales. Si se ejecuta sin parámetros, `sp_helprotect` presenta todos los permisos que se han concedido o denegado en la base de datos actual.  
  
 Si se especifican algunos parámetros, pero no todos, se tienen que utilizar parámetros con nombre para identificar el parámetro concreto o `NULL` como marcador de posición. Por ejemplo, para presentar todos los permisos del propietario de la base de datos del otorgante de permisos (`dbo`), ejecute:  
  
```  
EXEC sp_helprotect NULL, NULL, dbo;  
```  
  
 O bien  
  
```  
EXEC sp_helprotect @grantorname = 'dbo';  
```  
  
 El resultado está ordenada por categoría de los permisos, propietario, objeto, beneficiario, asignador, categoría del tipo de protección, tipo de protección, acción e Id. secuencial de columna.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
 La información mostrada está sometida a restricciones de acceso a los metadatos. No se mostrarán las entidades en las que la entidad de seguridad no tiene permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-the-permissions-for-a-table"></a>A. Presentar los permisos de una tabla  
 En el siguiente ejemplo se presentan los permisos de la tabla `titles`.  
  
```  
EXEC sp_helprotect 'titles';  
```  
  
### <a name="b-listing-the-permissions-for-a-user"></a>B. Presentar los permisos de un usuario  
 En el siguiente ejemplo se presentan todos los permisos que el usuario `Judy` tiene en la base de datos actual.  
  
```  
EXEC sp_helprotect NULL, 'Judy';  
```  
  
### <a name="c-listing-the-permissions-granted-by-a-specific-user"></a>C. Presentar los permisos concedidos por un usuario específico  
 En el siguiente ejemplo se presentan todos los permisos concedidos por el usuario `Judy` en la base de datos actual, con `NULL` como marcador de posición en los parámetros no especificados.  
  
```  
EXEC sp_helprotect NULL, NULL, 'Judy';  
```  
  
### <a name="d-listing-the-statement-permissions-only"></a>D. Presentar solo los permisos de las instrucciones  
 En el siguiente ejemplo se presentan todos los permisos de instrucciones de la base de datos actual, con `NULL` como marcador de posición para los parámetros no especificados.  
  
```  
EXEC sp_helprotect NULL, NULL, NULL, 's';   
```  
  
### <a name="e-listing-the-permissions-for-a-create-statement"></a>e. Presentar los permisos de una instrucción CREATE  
 En el ejemplo siguiente se muestran todos los usuarios a los que se ha concedido el permiso CREATE TABLE.  
  
```  
EXEC sp_helprotect @name = 'CREATE TABLE';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
