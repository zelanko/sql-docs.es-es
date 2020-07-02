---
title: xp_grantlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_grantlogin
- xp_grantlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- xp_grantlogin
ms.assetid: c851c1ab-3b29-4b99-9902-78c2665a844b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 81237214608b6fb0c04fa0857203d0488db375ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85633544"
---
# <a name="xp_grantlogin-transact-sql"></a>xp_grantlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Concede acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usuarios o grupos de Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilice [Create login](../../t-sql/statements/create-login-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_grantlogin {[@loginame = ] 'login'} [,[@logintype = ] 'logintype']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'`Es el nombre del usuario o grupo de Windows que se va a agregar. El usuario o grupo de Windows se debe calificar con un nombre de dominio de Windows con el formato *dominio* \\ *usuario*. *login* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @logintype = ] 'logintype'`Es el nivel de seguridad del inicio de sesión al que se concede acceso. *LoginType* es de tipo **VARCHAR (5)** y su valor predeterminado es NULL. Solo se puede especificar **admin** . Si se especifica **admin** , se concede al *Inicio de sesión* acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se agrega como miembro del rol fijo de servidor **sysadmin** .  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Observaciones  
 **xp_grantlogin** es ahora un procedimiento almacenado del sistema en lugar de un procedimiento almacenado extendido. **xp_grantlogin** llama a **sp_grantlogin** y **sp_addsrvrolemember**.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **securityadmin** . Al cambiar *LoginType*, es necesario pertenecer al rol fijo de servidor **sysadmin** .  
  
## <a name="see-also"></a>Consulte también  
 [sp_denylogin &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados extendidos generales &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_enumgroups &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/xp-enumgroups-transact-sql.md)   
 [xp_loginconfig &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)  
  
  
