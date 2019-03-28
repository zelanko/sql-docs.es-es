---
title: sysmail_update_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 09af9a0190b8ba3b01c72cfa29e0647ad6d6b74d
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528437"
---
# <a name="sysmailupdateaccountsp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la información de una cuenta existente del Correo electrónico de base de datos.  
 
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @account_id = ] account_id` El identificador de cuenta para la actualización. *account_id* es **int**, su valor predeterminado es null. Al menos uno de *account_id* o *account_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre de la cuenta.  
  
`[ @account_name = ] 'account_name'` El nombre de la cuenta que desea actualizar. *account_name* es **sysname**, su valor predeterminado es null. Al menos uno de *account_id* o *account_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre de la cuenta.  
  
`[ @email_address = ] 'email_address'` La nueva dirección de correo electrónico para enviar el mensaje desde. Esta dirección debe ser una dirección de correo electrónico de Internet. El nombre de servidor de la dirección es el servidor que Database Mail utiliza para enviar correo de esta cuenta. *Email_Address* es **nvarchar (128)**, su valor predeterminado es null.  
  
`[ @display_name = ] 'display_name'` El nombre para mostrar nuevo para usar en los mensajes de correo electrónico desde esta cuenta. *display_name* es **nvarchar (128)**, no tiene ningún valor predeterminado.  
  
`[ @replyto_address = ] 'replyto_address'` La nueva dirección para usar en el encabezado responder a mensajes de correo electrónico desde esta cuenta. *replyto_address* es **nvarchar (128)**, no tiene ningún valor predeterminado.  
  
`[ @description = ] 'description'` La nueva descripción para la cuenta. *descripción* es **nvarchar (256)**, su valor predeterminado es null.  
  
`[ @mailserver_name = ] 'server_name'` El nuevo nombre del servidor de correo SMTP que se usará para esta cuenta. El equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser capaz de resolver el *nombre_servidor* en una dirección IP. *nombre_servidor* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @mailserver_type = ] 'server_type'` El nuevo tipo de servidor de correo. *server_type* es **sysname**, no tiene ningún valor predeterminado. Solo un valor de **'SMTP'** se admite.  
  
`[ @port = ] port_number` El nuevo número de puerto del servidor de correo. *número_puerto* es **int**, no tiene ningún valor predeterminado.  
  
`[ @timeout = ] 'timeout'` Parámetro Timeout para SmtpClient.Send de un mensaje de correo electrónico única. *Tiempo de espera* es **int** en segundos, no tiene ningún valor predeterminado.  
  
`[ @username = ] 'username'` Nuevo nombre de usuario que use para iniciar sesión en el servidor de correo. *Nombre de usuario* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @password = ] 'password'` La nueva contraseña para usarla para iniciar sesión en el servidor de correo. *contraseña* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @use_default_credentials = ] use_default_credentials` Especifica si se debe enviar el correo al servidor SMTP con las credenciales de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] service. **use_default_credentials** es de tipo bit, no tiene ningún valor predeterminado. Si el valor de este parámetro es 1, el Correo electrónico de base de datos usa las credenciales de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cuando este parámetro es 0, el correo electrónico de base de datos utiliza el **@username** y **@password** para la autenticación en el servidor SMTP. Si **@username** y **@password** son NULL, utiliza la autenticación anónima. Consulte con el administrador de SMTP antes de especificar este parámetro.  
  
`[ @enable_ssl = ] enable_ssl` Especifica si el correo de base de datos cifra la comunicación mediante capa de Sockets seguros (SSL). Utilice esta opción si se requiere SSL en el servidor SMTP. **enable_ssl** es de tipo bit, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Si se especifican el nombre y el Id. de cuenta, el procedimiento almacenado cambia el nombre de la cuenta además de actualizar su información. Cambiar el nombre de la cuenta puede ser útil para corregir errores en el nombre.  
  
 El procedimiento almacenado **sysmail_update_account_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-information-for-an-account"></a>A. Cambio de la información de una cuenta  
 En el ejemplo siguiente se actualiza la cuenta `AdventureWorks Administrator` en el **msdb** base de datos. La información de la cuenta se establece con los valores proporcionados.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>b. Cambio del nombre de una cuenta y de la información de una cuenta  
 En el ejemplo siguiente se cambia el nombre y se actualiza la información de la cuenta con el Id. de cuenta `125`. El nuevo nombre de la cuenta es `Backup Mail Server`.  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
