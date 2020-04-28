---
title: sp_dbfixedrolepermission (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2a51fcc7108c7f6af6237d77cbad73c87ed7c6e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78180120"
---
# <a name="sp_dbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra los permisos de un rol fijo de base de datos. **sp_dbfixedrolepermission** devuelve la información correcta [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]en. El resultado no refleja los cambios en la jerarquía de permisos que se implementaron [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]en. Para obtener más información, vea [roles de nivel de base de datos](../../relational-databases/security/authentication-access/database-level-roles.md#fixed-database-roles), que muestra una lista de roles fijos de base de datos y sus permisos correspondientes.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`Es el nombre de un rol [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fijo de base de datos válido. *role* es de **tipo sysname y su**valor predeterminado es NULL. Si no se especifica *role* , se muestran los permisos de todos los roles fijos de base de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|Nombre del rol fijo de base de datos|  
|**Permiso**|**nvarchar (70)**|Permisos asociados a **DbFixedRole**|  
  
## <a name="remarks"></a>Observaciones  
 Para mostrar una lista de los roles fijos de base de datos, ejecute **sp_helpdbfixedrole**. En la tabla siguiente se muestran los roles fijos de base de datos.  
  
|Rol fijo de base de datos|Descripción|  
|-------------------------|-----------------|  
|**db_owner**|Propietarios de base de datos|  
|**db_accessadmin**|Administradores de acceso a la base de datos|  
|**db_securityadmin**|Administradores de seguridad de la base de datos|  
|**db_ddladmin**|Administradores del Lenguaje de definición de datos (DDL, Data Definition Language) de base de datos |  
|**db_backupoperator**|Operadores de copia de seguridad de la base de datos|  
|**db_datareader**|Lectores de datos de la base de datos|  
|**db_datawriter**|Escritores de datos de la base de datos|  
|**db_denydatareader**|Lectores de datos denegados de la base de datos|  
|**db_denydatawriter**|Escritores de datos denegados de la base de datos|  
  
 Los miembros del rol fijo de base de datos **db_owner** tienen los permisos de todos los demás roles fijos de base de datos. Para mostrar los permisos de los roles fijos de servidor, ejecute **sp_srvrolepermission**.  
  
 El conjunto de resultados contiene las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que se pueden ejecutar y otras actividades especiales que pueden realizar los miembros del rol de base de datos.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En la siguiente consulta se devuelven los permisos de todos los roles fijos de base de datos porque no se especifica un rol fijo de base de datos.  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
