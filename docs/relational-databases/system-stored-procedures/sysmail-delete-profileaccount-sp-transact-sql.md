---
title: sysmail_delete_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4395114f266345cb7583c45285366c5bd2b7afff
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537137"
---
# <a name="sysmaildeleteprofileaccountsp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una cuenta de un perfil del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` El identificador de perfil del perfil va a eliminar. *profile_id* es **int**, su valor predeterminado es null. Ya sea el *profile_id* o *profile_name* se puede especificar.  
  
`[ @profile_name = ] 'profile_name'` El nombre del perfil del perfil que desea eliminar. *nombre_perfil* es **sysname**, su valor predeterminado es null. Ya sea el *profile_id* o *profile_name* se puede especificar.  
  
`[ @account_id = ] account_id` El identificador de cuenta va a eliminar. *account_id* es **int**, su valor predeterminado es null. Ya sea el *account_id* o *account_name* se puede especificar.  
  
`[ @account_name = ] 'account_name'` El nombre de la cuenta que desea eliminar. *account_name* es **sysname**, su valor predeterminado es null. Ya sea el *account_id* o *account_name* se puede especificar.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Devuelve un error si la cuenta especificada no está asociada al perfil especificado.  
  
 Cuando se especifica una cuenta pero no se especifica ningún perfil, este procedimiento almacenado quita la cuenta especificada de todos los perfiles. Por ejemplo, si está preparando el apagado de un servidor SMTP, quita las cuentas que utiliza el servidor SMTP de todos los perfiles, en lugar de quitar cada cuenta de cada perfil.  
  
 Cuando se especifica un perfil pero no se especifica ninguna cuenta, este procedimiento almacenado quita todas las cuentas del perfil especificado. Por ejemplo, si va a cambiar los servidores SMTP que utiliza un perfil, puede ser conveniente quitar todas las cuentas del perfil y agregar después cuentas nuevas según sea necesario.  
  
 El procedimiento almacenado **sysmail_delete_profileaccount_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra cómo se quita la cuenta `Audit Account` del perfil `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
