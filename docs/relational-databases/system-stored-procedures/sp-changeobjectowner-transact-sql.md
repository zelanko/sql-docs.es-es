---
title: sp_changeobjectowner (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_changeobjectowner_TSQL
- sp_changeobjectowner
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changeobjectowner
ms.assetid: 45b3dc1c-1cde-45b7-a248-5195c12973e9
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 5426d05f577016a2a93f131a7eaca85abe6e4f21
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangeobjectowner-transact-sql"></a>sp_changeobjectowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el propietario de un objeto en la base de datos actual.  
  
> [!IMPORTANT]  
>  Este procedimiento almacenado solo funciona con los objetos disponibles en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER SCHEMA](../../t-sql/statements/alter-schema-transact-sql.md) o [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) en su lugar. **sp_changeobjectowner** cambia el esquema y el propietario. Para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], este procedimiento almacenado solo cambia los propietarios de los objetos cuando el propietario actual y el nuevo poseen esquemas con el mismo nombre que sus nombres de usuario de base de datos.  
  
> [!IMPORTANT]  
>  Se ha agregado un nuevo requisito a los permisos de este procedimiento almacenado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changeobjectowner [ @objname = ] 'object' , [ @newowner = ] 'owner'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@objname =** ] **'***objeto***'**  
 Es el nombre de una tabla, una vista, una función definida por el usuario o un procedimiento almacenado existentes en la base de datos actual. *objeto* es un **nvarchar(776)**, no tiene ningún valor predeterminado. *objeto* se puede calificar con el propietario del objeto existente, en el formulario *existing_owner.Object ***.*** objeto* si el esquema y su propietario tienen el mismo nombre.  
  
 [  **@newowner=**] **' *** propietario* **'**  
 Es el nombre de la cuenta de seguridad que corresponde al nuevo propietario del objeto. *propietario* es **sysname**, no tiene ningún valor predeterminado. *propietario* debe ser un usuario de base de datos válido, el rol de servidor [!INCLUDE[msCoName](../../includes/msconame-md.md)] inicio de sesión de Windows o grupo de Windows con acceso a la base de datos actual. Si el nuevo propietario es un usuario o grupo de Windows que no tiene una entidad de seguridad de base de datos correspondiente, se creará un usuario de base de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changeobjectowner** quita todos los permisos existentes del objeto. Tendrá que volver a aplicar los permisos que desea mantener después de ejecutar **sp_changeobjectowner**. Por lo tanto, se recomienda que es un script para los permisos existentes antes de ejecutar **sp_changeobjectowner**. Una vez modificado el propietario del objeto, se puede utilizar el script para volver a aplicar los permisos. Deberá modificar el propietario del objeto en el script de permisos antes de la ejecución.  
  
 Para cambiar el propietario de un elemento protegible, utilice ALTER AUTHORIZATION. Para cambiar un esquema, utilice ALTER SCHEMA.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **db_owner** rol fijo de base de datos, o pertenencia tanto en el **db_ddladmin** rol fijo de base de datos y la **db_securityadmin** función fija de base de datos, y también el permiso CONTROL en el objeto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el propietario de la `authors` tabla a `Corporate\GeorgeW`.  
  
```  
EXEC sp_changeobjectowner 'authors', 'Corporate\GeorgeW';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER SCHEMA &#40;Transact-SQL&#41;](../../t-sql/statements/alter-schema-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_changedbowner &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
