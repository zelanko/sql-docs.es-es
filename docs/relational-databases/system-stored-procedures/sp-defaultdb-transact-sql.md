---
title: sp_defaultdb (Transact-SQL) | Documentos de Microsoft
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
- sp_defaultdb_TSQL
- sp_defaultdb
dev_langs: TSQL
helpviewer_keywords: sp_defaultdb
ms.assetid: 663b859f-c6da-4942-95a6-60b93d05654e
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c44a3f1f26861e3e78e936aeb642e33ead4a4786
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spdefaultdb-transact-sql"></a>sp_defaultdb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la base de datos predeterminada para un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_defaultdb [ @loginame = ] 'login', [ @defdb = ] 'database'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@loginame=**] **'***inicio de sesión***'**  
 Es el nombre de inicio de sesión. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* puede ser una existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o un grupo o usuario de Windows. Si un inicio de sesión del usuario o grupo de Windows no existe en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se agrega automáticamente.  
  
 [  **@defdb=**] **'***base de datos***'**  
 Es el nombre de la nueva base de datos predeterminada. *base de datos* es **sysname**, no tiene ningún valor predeterminado. *base de datos* ya debe existir.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_defaultdb** llama a ALTER LOGIN. Esta instrucción admite opciones adicionales. Para obtener información acerca de cómo cambiar la base de datos predeterminada, vea [ALTER LOGIN &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-login-transact-sql.md).  
  
 **sp_defaultdb** no puede ejecutarse en una transacción definida por el usuario.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se establece [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] como la base de datos predeterminada para el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Victoria`.  
  
```  
EXEC sp_defaultdb 'Victoria', 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguridad almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
