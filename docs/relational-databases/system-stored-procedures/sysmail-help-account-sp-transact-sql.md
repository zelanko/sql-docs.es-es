---
title: sysmail_help_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fb61b115689472c5be3ec14de2e7387de3317d4d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82814149"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información (excepto contraseñas) sobre las cuentas del Correo electrónico de base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @account_id = ] account_id`IDENTIFICADOR de cuenta de la cuenta para la que se va a mostrar información. *ACCOUNT_ID* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @account_name = ] 'account_name'`Nombre de la cuenta para la que se va a mostrar información. *account_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Devuelve un conjunto de resultados que contiene las columnas que se indican a continuación.  
  
||||  
|-|-|-|  
|Nombre de la columna|Tipo de datos|Descripción|  
|**account_id**|**int**|Id. de la cuenta.|  
|**name**|**sysname**|El nombre de la cuenta.|  
|**denominación**|**nvarchar(256)**|Descripción de la cuenta.|  
|**email_address**|**nvarchar(128)**|Dirección de correo electrónico desde la que se envían los mensajes.|  
|**display_name**|**nvarchar(128)**|El nombre para mostrar de la cuenta.|  
|**replyto_address**|**nvarchar(128)**|La dirección a la que se envían las respuestas a los mensajes de esta cuenta.|  
|**ServerType**|**sysname**|Tipo de servidor de correo electrónico para la cuenta.|  
|**ServerName**|**sysname**|Nombre del servidor de correo electrónico para la cuenta.|  
|**port**|**int**|Número de puerto que utiliza el servidor de correo electrónico.|  
|**username**|**nvarchar(128)**|Nombre de usuario que se utiliza para iniciar sesión en el servidor de correo electrónico si éste utiliza autenticación. Cuando el **nombre de usuario** es NULL, correo electrónico de base de datos no utiliza la autenticación para esta cuenta.|  
|**use_default_credentials**|**bit**|Especifica si se debe enviar el correo al servidor SMTP con las credenciales de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** es de bits y no tiene ningún valor predeterminado. Si el valor de este parámetro es 1, el Correo electrónico de base de datos utiliza las credenciales del servicio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Cuando este parámetro es 0, Correo electrónico de base de datos usa el ** \@ nombre de usuario** y la ** \@ contraseña** para la autenticación en el servidor SMTP. Si el ** \@ nombre de usuario** y la ** \@ contraseña** son NULL, correo electrónico de base de datos usa la autenticación anónima. Consulte al administrador de SMTP antes de especificar este parámetro.|  
|**enable_ssl**|**bit**|Especifica si Correo electrónico de base de datos cifra la comunicación mediante la seguridad de la capa de transporte (TLS), conocida anteriormente como Capa de sockets seguros (SSL). Utilice esta opción si se requiere TLS en el servidor SMTP. **enable_ssl** es de bits y no tiene ningún valor predeterminado. 1 indica Correo electrónico de base de datos cifra la comunicación mediante TLS. 0 indica Correo electrónico de base de datos envía el correo sin cifrado TLS.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando no se proporciona ningún *ACCOUNT_ID* o *account_name* , **sysmail_help_account** muestra información sobre todas las cuentas de correo electrónico de base de datos en la instancia de Microsoft SQL Server.  
  
 El procedimiento almacenado **sysmail_help_account_sp** está en la base de datos **msdb** y pertenece al esquema **DBO** . El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución para este procedimiento tienen como valor predeterminado los miembros del rol fijo de servidor **sysadmin** .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Creación de una cuenta de Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Correo electrónico de base de datos procedimientos almacenados &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
