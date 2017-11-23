---
title: xp_revokelogin (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
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
- xp_revokelogin
- xp_revokelogin_TSQL
dev_langs: TSQL
helpviewer_keywords: xp_revokelogin
ms.assetid: b3fa7678-dba4-4537-be94-5ae63ca11f81
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc77efcdd8bf82873be018c0e54681c3f32e78dd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="xprevokelogin-transact-sql"></a>xp_revokelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoca el acceso de un usuario o un grupo de Windows a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md) en su lugar.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
xp_revokelogin {[@loginame=] 'login'}  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame =** ] **'***inicio de sesión***'**  
 Es el nombre del usuario o grupo de Windows del que se va a revocar el acceso. *inicio de sesión* debe incluir el nombre de dominio, por ejemplo **[ADVWKS\sylvester1]**. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 En su lugar, use DROP LOGIN.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [sp_denylogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Extendidos generales procedimientos almacenados &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
