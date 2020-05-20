---
title: sp_defaultlanguage (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_defaultlanguage
- sp_defaultlanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_defaultlanguage
ms.assetid: 908d01cc-e704-45d9-9e85-d2df6da3e6f5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7c06f03af5ab9cc8d06b8d7d0f87208895c1fc33
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826165"
---
# <a name="sp_defaultlanguage-transact-sql"></a>sp_defaultlanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el idioma predeterminado de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Utilice [ALTER login](../../t-sql/statements/alter-login-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_defaultlanguage [ @loginame = ] 'login'   
     [ , [ @language = ] 'language' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login'`Es el nombre de inicio de sesión. *login* es de **tipo sysname**y no tiene ningún valor predeterminado. el *Inicio de sesión* puede ser un inicio de sesión existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un usuario o grupo de Windows.  
  
`[ @language = ] 'language'`Es el idioma predeterminado del inicio de sesión. *Language* es de **tipo sysname y su**valor predeterminado es NULL. *Language* debe ser un idioma válido en el servidor. Si no se especifica *Language* , *Language* se establece en el idioma predeterminado del servidor; el idioma predeterminado se define mediante el **idioma predeterminado**de la variable de configuración **sp_configure** . El cambio del idioma predeterminado del servidor no cambia el idioma predeterminado de los inicios de sesión existentes.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_defaultlanguage** llama a Alter login, que admite opciones adicionales. Para obtener información sobre cómo cambiar otros valores predeterminados de inicio de sesión, vea [ALTER login &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md).  
  
 Use la instrucción SET LANGUAGE para cambiar el idioma de la sesión actual. Use la @LANGUAGE función @ para mostrar la configuración de idioma actual.  
  
 Si el idioma predeterminado de un inicio de sesión se quita del servidor, el inicio de sesión adquiere el idioma predeterminado del servidor. **sp_defaultlanguage** no se puede ejecutar en una transacción definida por el usuario.  
  
 La información sobre los idiomas instalados en el servidor es visible en la vista de catálogo **Sys. syslanguages** .  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso ALTER ANY LOGIN.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `ALTER LOGIN` para cambiar el idioma predeterminado del inicio de sesión `Fathima` a Árabe. Este es el método preferido.  
  
```  
ALTER LOGIN Fathima WITH DEFAULT_LANGUAGE = Arabic;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Sys. syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
