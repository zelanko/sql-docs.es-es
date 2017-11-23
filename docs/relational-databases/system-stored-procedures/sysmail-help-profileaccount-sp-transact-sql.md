---
title: sysmail_help_profileaccount_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
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
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
caps.latest.revision: "43"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 30af309db029d4d969fe39eb87e15503b590dfae
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysmailhelpprofileaccountsp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra las cuentas asociadas con uno o varios perfiles del Correo electrónico de base de datos.  
    
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id**  =] *profile_id*  
 Es el identificador de perfil del perfil a la lista. *profile_id* es **int**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* debe especificarse.  
  
 [  **@profile_name**  =] **'***profile_name***'**  
 Es el nombre del perfil que se va a mostrar. *profile_name* es **sysname**, su valor predeterminado es null. Cualquier *profile_id* o *profile_name* debe especificarse.  
  
 [  **@account_id**  =] *account_id*  
 Es el identificador de la cuenta que se va a mostrar. *account_id* es **int**, su valor predeterminado es null. Cuando *account_id* y *account_name* son NULL, enumera todas las cuentas en el perfil.  
  
 [  **@account_name**  =] **'***account_name***'**  
 Es el nombre de la cuenta que se va a mostrar. *account_name* es **sysname**, su valor predeterminado es null. Cuando *account_id* y *account_name* son NULL, enumera todas las cuentas en el perfil.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados con las columnas siguientes:  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Description|  
|**profile_id**|**int**|Id. de perfil del perfil.|  
|**profile_name**|**sysname**|El nombre del perfil.|  
|**account_id**|**int**|Id. de cuenta de la cuenta.|  
|**account_name**|**sysname**|El nombre de la cuenta.|  
|**sequence_number**|**int**|Número de secuencia de la cuenta en el perfil.|  
  
## <a name="remarks"></a>Comentarios  
 Si no *profile_id* o *profile_name* se especifica, este procedimiento almacenado devuelve información para todos los perfiles de la instancia.  
  
 El procedimiento almacenado **sysmail_help_profileaccount_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Mostrar las cuentas de un perfil específico por nombre**  
  
 En el ejemplo siguiente se indica cómo mostrar la información del perfil `AdventureWorks Administrator` especificando el nombre de perfil.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **B. Mostrar las cuentas de un identificador de perfil por perfil específico**  
  
 En el ejemplo siguiente se indica cómo mostrar la información del perfil `AdventureWorks Administrator` especificando el Id. del perfil.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **C. Mostrar las cuentas de todos los perfiles**  
  
 En el ejemplo siguiente se indica cómo mostrar las cuentas de todos los perfiles de la instancia.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Objetos de configuración de correo electrónico de base de datos](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Correo electrónico de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
