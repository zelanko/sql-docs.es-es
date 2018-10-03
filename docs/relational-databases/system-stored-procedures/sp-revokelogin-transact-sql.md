---
title: sp_revokelogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_revokelogin_TSQL
- sp_revokelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revokelogin
ms.assetid: cb1ab102-1ae0-4811-9144-9a8121ef2d7e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 57c7ef9242b6c974c8043f8f6ab237b0fbe07941
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706662"
---
# <a name="sprevokelogin-transact-sql"></a>sp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita las entradas de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para un usuario de Windows o un grupo creado mediante CREATE LOGIN, **sp_grantlogin**, o **sp_denylogin**.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_revokelogin [ @loginame= ] 'login'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame=**] **'***inicio de sesión***'**  
 Es el nombre del usuario o grupo de Windows. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* puede ser cualquier nombre de usuario de Windows existente o un grupo en el formulario *nombre_equipo*\\*usuario o dominio*\\*usuario*.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_revokelogin** deshabilita las conexiones mediante la cuenta especificada por el *inicio de sesión* parámetro. Los usuarios de Windows que tienen acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por medio de su pertenencia a un grupo de Windows, pueden seguir conectándose como parte del grupo aunque se les deniegue el acceso individual. De forma similar, si la *inicio de sesión* parámetro especifica el nombre de un grupo de Windows, los miembros de ese grupo que han sido por separado conceden acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podrán conectarse.  
  
 Por ejemplo, si el usuario de Windows **ADVWORKS\john** es un miembro del grupo de Windows **ADVWORKS\Admins**, y **sp_revokelogin** revoca el acceso de `ADVWORKS\john`:  
  
```  
sp_revokelogin [ADVWORKS\john]  
```  
  
 Usuario **ADVWORKS\john** todavía puede conectarse si **ADVWORKS\Admins** se ha concedido acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. De forma similar, si el grupo de Windows **ADVWORKS\Admins** tiene su acceso revocado pero **ADVWORKS\john** se le concede acceso, **ADVWORKS\john** todavía puede conectarse.  
  
 Use **sp_denylogin** evitar explícitamente que los usuarios conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de su pertenencia a grupos de Windows.  
  
 **sp_revokelogin** no se puede ejecutar dentro de una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY LOGIN en el servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita las entradas de inicio de sesión del usuario de Windows `Corporate\MollyA`.  
  
```  
EXEC sp_revokelogin 'Corporate\MollyA';  
```  
  
 o bien  
  
```  
EXEC sp_revokelogin [Corporate\MollyA];  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
