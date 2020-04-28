---
title: sp_changedbowner (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changedbowner
- sp_changedbowner_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changedbowner
ms.assetid: 516ef311-e83b-45c9-b9cd-0e0641774c04
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4bca86b00ca5b2d84cc1c737ecf9d253a0451ea9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68126460"
---
# <a name="sp_changedbowner-transact-sql"></a>sp_changedbowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el propietario de la base de datos actual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, use [ALTER Authorization](../../t-sql/statements/alter-authorization-transact-sql.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changedbowner [ @loginame = ] 'login'  
     [ , [ @map = ] remap_alias_flag ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame= ] '*login*'  
 Es el identificador de inicio de sesión del nuevo propietario de la base de datos actual. *login* es de **tipo sysname**y no tiene ningún valor predeterminado. *login* debe ser un inicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sesión o un usuario de Windows ya existente. el *Inicio de sesión* no puede convertirse en el propietario de la base de datos actual si ya tiene acceso a la base de datos a través de una cuenta de seguridad de usuario existente en la base de datos. Para evitar esto, quite antes el usuario de la base de datos actual.  
  
 [ @map= ] *remap_alias_flag*  
 El parámetro *remap_alias_flag* está desusado porque los alias de inicio de sesión se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]han quitado de. El uso del parámetro *remap_alias_flag* no produce un error, pero no tiene ningún efecto.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 Después de ejecutar sp_changedbowner, el nuevo propietario se conoce como el usuario dbo de la base de datos. El dbo disfruta implícitamente de permisos para realizar todas las actividades de la base de datos.  
  
 No se puede cambiar el propietario de las bases de datos maestra, de modelos o tempdb del sistema.  
  
 Para mostrar una lista de los valores de *Inicio de sesión* válidos, ejecute el sp_helplogins procedimiento almacenado.  
  
 La ejecución de sp_changedbowner solo con el parámetro *login* cambia la propiedad de la base de datos al *Inicio de sesión*.  
  
 Puede cambiar el propietario de cualquier elemento protegible usando la instrucción ALTER AUTHORIZATION. Para obtener más información, vea [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere permiso TAKE OWNERSHIP en la base de datos. Si el nuevo propietario tiene un usuario correspondiente en la base de datos, requiere el permiso IMPERSONATE en el inicio de sesión, en caso contrario, requiere el permiso CONTROL SERVER en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, el nombre de inicio de sesión `Albert` se convierte en el propietario de la base de datos actual.  
  
```  
EXEC sp_changedbowner 'Albert';  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sp_dropalias &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md)   
 [sp_dropuser &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helpdb &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helplogins &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
