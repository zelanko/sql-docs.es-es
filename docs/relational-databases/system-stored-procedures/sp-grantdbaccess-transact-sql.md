---
title: sp_grantdbaccess (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grantdbaccess
- sp_grantdbaccess_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grantdbaccess
ms.assetid: 3eb09513-03f1-42f8-9917-3a1f3a579bec
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 3b88badb8b1852617d9edd8acd31f2c19258cca7
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304866"
---
# <a name="sp_grantdbaccess-transact-sql"></a>sp_grantdbaccess (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un usuario de base de datos a la base de datos actual.  
  
> [!IMPORTANT]  
>  en su lugar [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)], use [Create User](../../t-sql/statements/create-user-transact-sql.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_grantdbaccess [ @loginame = ] 'login'  
    [ , [ @name_in_db = ] 'name_in_db' [ OUTPUT ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login_ '` es el nombre del grupo de Windows, Inicio de sesión de Windows o inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se va a asignar al nuevo usuario de base de datos. Los nombres de los grupos de Windows y los inicios de sesión de Windows deben calificarse con un nombre de dominio de Windows con el formato *dominio*\\*Inicio de sesión*; por ejemplo, **LONDON\Joeb**. El inicio de sesión ya no se puede asignar a un usuario de la base de datos. *login* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
``[ @name_in_db = ] 'name_in_db' [ OUTPUT]`` es el nombre del nuevo usuario de la base de datos. *name_in_db* es una variable de salida con un tipo de datos **sysname y su**valor predeterminado es NULL. Si no se especifica, se usa *login* . Si se especifica como una variable de salida con un valor NULL, **\@name_in_db** se establece en *login*. *name_in_db* no debe existir ya en la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_grantdbaccess** llama a Create User, que admite opciones adicionales. Para obtener información sobre cómo crear usuarios de base de datos, vea [Create User &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md). Para quitar un usuario de base de datos de una base de datos, utilice [Drop User](../../t-sql/statements/drop-user-transact-sql.md).  
  
 **sp_grantdbaccess** no se puede ejecutar en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos **db_owner** o al rol fijo de base de datos **db_accessadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `CREATE USER` para agregar un usuario de base de datos para el inicio de sesión de Windows `Edmonds\LolanSo` a la base de datos actual. El nuevo usuario se llama `Lolan`. Es el método preferido para crear un usuario de base de datos.  
  
```sql
CREATE USER Lolan FOR LOGIN [Edmonds\LolanSo];  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
