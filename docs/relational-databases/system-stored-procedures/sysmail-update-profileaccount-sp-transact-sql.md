---
title: sysmail_update_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 96dc0a33c15f1547088c3fe7c79824da55cd1d35
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538127"
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza el número de secuencia de una cuenta de un perfil del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` El identificador de perfil del perfil para la actualización. *profile_id* es **int**, su valor predeterminado es null. Ya sea el *profile_id* o *profile_name* debe especificarse.  
  
`[ @profile_name = ] 'profile_name'` El nombre del perfil del perfil que desea actualizar. *nombre_perfil* es **sysname**, su valor predeterminado es null. Ya sea el *profile_id* o *profile_name* debe especificarse.  
  
`[ @account_id = ] account_id` El identificador de cuenta para la actualización. *account_id* es **int**, su valor predeterminado es null. Ya sea el *account_id* o *account_name* debe especificarse.  
  
`[ @account_name = ] 'account_name'` El nombre de la cuenta que desea actualizar. *account_name* es **sysname**, su valor predeterminado es null. Ya sea el *account_id* o *account_name* debe especificarse.  
  
`[ @sequence_number = ] sequence_number` El nuevo número de secuencia para la cuenta. *sequence_number* es **int**, no tiene ningún valor predeterminado. El número de secuencia determina el orden en que las cuentas se utilizan en el perfil.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Devuelve un error si la cuenta especificada no está asociada al perfil especificado.  
  
 El número de secuencia determina el orden en que el Correo electrónico de base de datos utiliza las cuentas en el perfil. En el caso de un mensaje de correo electrónico nuevo, el Correo electrónico de base de datos se inicia con la cuenta con el número de secuencia más bajo. Si la cuenta genera un error, el Correo electrónico de base de datos utiliza la cuenta con el siguiente número de secuencia superior y así sucesivamente hasta que el Correo electrónico de base de datos envía el mensaje correctamente o la cuenta con el número de secuencia superior genera un error. Si la cuenta con el número de secuencia superior genera un error, el mensaje de correo electrónico también genera un error.  
  
 Si hay más de una cuenta con el mismo número de secuencia, el Correo electrónico de base de datos solo utiliza una de estas cuentas para un mensaje de correo electrónico determinado. En este caso, el Correo electrónico de base de datos no confirma qué cuenta se va a usar para el número de secuencia o que se vaya a usar la misma cuenta de un mensaje a otro.  
  
 El procedimiento almacenado **sysmail_update_profileaccount_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el número de secuencia de la cuenta `Admin-BackupServer` dentro del perfil `AdventureWorks Administrator` en el **msdb** base de datos. Tras ejecutar este código, el número de secuencia para la cuenta es `3`, lo que indica que se va a probar si las dos primeras cuentas generan un error.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
