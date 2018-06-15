---
title: sp_defaultlanguage (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a382ceab3491cfbcd1b8d6dad564f6d8826c2d13
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33246206"
---
# <a name="spdefaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el idioma predeterminado de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@loginame =** ] **'***login***'**  
 Es el nombre de inicio de sesión. *inicio de sesión* es **sysname**, no tiene ningún valor predeterminado. *inicio de sesión* puede ser una existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión o un grupo o usuario de Windows.  
  
 [  **@language =** ] **'***lenguaje***'**  
 Es el idioma predeterminado del inicio de sesión. *idioma* es **sysname**, su valor predeterminado es null. *idioma* debe ser un idioma válido en el servidor. Si *lenguaje* no se especifica, *lenguaje* se establece en el idioma predeterminado del servidor; idioma predeterminado está definido por el **sp_configure** variable de configuración **idioma predeterminado**. El cambio del idioma predeterminado del servidor no cambia el idioma predeterminado de los inicios de sesión existentes.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_defaultlanguage** llama a ALTER LOGIN, que admite opciones adicionales. Para obtener información acerca de cómo cambiar otros valores predeterminados de inicio de sesión, vea [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Use la instrucción SET LANGUAGE para cambiar el idioma de la sesión actual. Use el @@LANGUAGE función para mostrar la configuración de idioma actual.  
  
 Si el idioma predeterminado de un inicio de sesión se quita del servidor, el inicio de sesión adquiere el idioma predeterminado del servidor. **sp_defaultlanguage** no puede ejecutarse en una transacción definida por el usuario.  
  
 Información acerca de los idiomas instalados en el servidor está visible en el **sys.syslanguages** vista de catálogo.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY LOGIN.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `ALTER LOGIN` para cambiar el idioma predeterminado del inicio de sesión `Fathima` a Árabe. Éste es el método preferido.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
