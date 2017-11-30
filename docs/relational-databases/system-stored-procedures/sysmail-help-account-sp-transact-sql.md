---
title: sysmail_help_account_sp (Transact-SQL) | Documentos de Microsoft
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
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs: TSQL
helpviewer_keywords: sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
caps.latest.revision: "48"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfc032a279abad7949e67f4c232cbe30219baa30
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysmailhelpaccountsp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información (excepto contraseñas) sobre las cuentas del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@account_id**  =] *account_id*  
 Id. de la cuenta para la que se va a mostrar información. *account_id* es **int**, su valor predeterminado es null.  
  
 [  **@account_name**  =] **'***account_name***'**  
 Nombre de la cuenta para la que se va a mostrar información. *account_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados que contiene las columnas que se indican a continuación.  
  
||||  
|-|-|-|  
|Nombre de columna|Tipo de datos|Description|  
|**account_id**|**int**|Id. de la cuenta.|  
|**Nombre**|**sysname**|El nombre de la cuenta.|  
|**Descripción**|**nvarchar(256)**|Descripción de la cuenta.|  
|**Email_Address**|**nvarchar (128)**|Dirección de correo electrónico desde la que se envían los mensajes.|  
|**display_name**|**nvarchar (128)**|El nombre para mostrar de la cuenta.|  
|**replyto_address**|**nvarchar (128)**|La dirección donde se envían las respuestas a los mensajes desde esta cuenta.|  
|**ServerType**|**sysname**|Tipo de servidor de correo electrónico para la cuenta.|  
|**ServerName**|**sysname**|Nombre del servidor de correo electrónico para la cuenta.|  
|**port**|**int**|Número de puerto que utiliza el servidor de correo electrónico.|  
|**nombre de usuario**|**nvarchar (128)**|Nombre de usuario que se utiliza para iniciar sesión en el servidor de correo electrónico si éste utiliza autenticación. Cuando **nombre de usuario** es NULL, correo electrónico de base de datos no usa la autenticación para esta cuenta.|  
|**use_default_credentials**|**bit**|Especifica si se debe enviar el correo al servidor SMTP con las credenciales de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** es de tipo bit no tiene ningún valor predeterminado. Si el valor de este parámetro es 1, el Correo electrónico de base de datos utiliza las credenciales del servicio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Si este parámetro es 0, el correo electrónico de base de datos utiliza el  **@username**  y  **@password**  para la autenticación en el servidor SMTP. Si  **@username**  y  **@password**  son NULL, correo electrónico de base de datos utiliza la autenticación anónima. Consulte al administrador de SMTP antes de especificar este parámetro.|  
|**enable_ssl**|**bit**|Especifica si el Correo electrónico de base de datos cifra la comunicación mediante Capa de sockets seguros (SSL). Utilice esta opción si se requiere SSL en el servidor SMTP. **enable_ssl** es de tipo bit no tiene ningún valor predeterminado. El valor 1 indica que el Correo electrónico de base de datos cifra la comunicación mediante SSL. El valor 0 indica que el Correo electrónico de base de datos envía el correo sin cifrado SSL.|  
  
## <a name="remarks"></a>Comentarios  
 Si no *account_id* o *account_name* se proporciona, **sysmail_help_account** muestra información en todas las cuentas de correo electrónico de base de datos en la instancia de Microsoft SQL Server.  
  
 El procedimiento almacenado **sysmail_help_account_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 **A. Mostrar información para todas las cuentas**  
  
 En el siguiente ejemplo se muestra la información de cuenta para todas las cuentas de la instancia.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B. Mostrar información para una cuenta específica**  
  
 En el siguiente ejemplo se muestra la información de cuenta para la cuenta llamada `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 El siguiente es un conjunto de resultados de ejemplo con la longitud de línea editada:  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Correo electrónico de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
