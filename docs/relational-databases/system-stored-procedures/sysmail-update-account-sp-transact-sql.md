---
title: sysmail_update_account_sp (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9a4771a0011f533be044384eac811c8e6de8ff17
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [ **@account_id** =] *account_id*  
 Identificador de la cuenta que se va a actualizar. *account_id* es **int**, su valor predeterminado es null. Al menos uno de *account_id* o *account_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre de la cuenta.  
  
 [ **@account_name** =] **'***account_name***'**  
 Nombre de la cuenta que se va a actualizar. *account_name* es **sysname**, su valor predeterminado es null. Al menos uno de *account_id* o *account_name* debe especificarse. Si se especifican los dos, el procedimiento cambia el nombre de la cuenta.  
  
 [ **@email_address** =] **'***email_address***'**  
 Es la nueva dirección de correo electrónico desde la que se envía el mensaje. Esta dirección debe ser una dirección de correo electrónico de Internet. El nombre de servidor de la dirección es el servidor que Database Mail utiliza para enviar correo de esta cuenta. *Email_Address* es **nvarchar (128)**, su valor predeterminado es null.  
  
 [ **@display_name** =] **'***display_name***'**  
 Nuevo nombre para mostrar que se utilizará en los mensajes de correo electrónico de esta cuenta. *display_name* es **nvarchar (128)**, no tiene ningún valor predeterminado.  
  
 [ **@replyto_address** =] **'***replyto_address***'**  
 Nueva dirección que se utilizará en el encabezado Responder a de los mensajes de correo electrónico de esta cuenta. *replyto_address* es **nvarchar (128)**, no tiene ningún valor predeterminado.  
  
 [ **@description** =] **'***descripción***'**  
 Nueva descripción de la cuenta. *descripción* es **nvarchar (256)**, su valor predeterminado es null.  
  
 [ **@mailserver_name** =] **'***nombre_servidor***'**  
 Es el nuevo nombre del servidor de correo SMTP que se debe utilizar para esta cuenta. El equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser capaz de resolver el *nombre_servidor* en una dirección IP. *nombre_servidor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@mailserver_type** =] **'***server_type***'**  
 Nuevo tipo del servidor de correo. *server_type* es **sysname**, no tiene ningún valor predeterminado. Solo un valor de **'SMTP'** se admite.  
  
 [ **@port** =] *número_puerto*  
 Nuevo número de puerto del servidor de correo. *número_puerto* es **int**, no tiene ningún valor predeterminado.  
  
 [ **@timeout** =] **'***tiempo de espera***'**  
 Parámetro Timeout para SmtpClient.Send de un único mensaje de correo electrónico. *Tiempo de espera* es **int** en segundos, no tiene ningún valor predeterminado.  
  
 [ **@username** =] **'***nombre de usuario***'**  
 Nuevo nombre de usuario que se utilizará para iniciar sesión en el servidor de correo. *Nombre de usuario* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@password** =] **'***contraseña***'**  
 Nueva contraseña que se utilizará para iniciar sesión en el servidor de correo. *contraseña* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@use_default_credentials** =] use_default_credentials  
 Especifica si se debe enviar el correo al servidor SMTP con las credenciales del servicio de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** es de tipo bit no tiene ningún valor predeterminado. Si el valor de este parámetro es 1, el Correo electrónico de base de datos usa las credenciales de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Si este parámetro es 0, el correo electrónico de base de datos utiliza el **@username** y **@password** para la autenticación en el servidor SMTP. Si **@username** y **@password** son NULL, a continuación, utiliza la autenticación anónima. Consulte con el administrador de SMTP antes de especificar este parámetro.  
  
 [ **@enable_ssl** =] enable_ssl  
 Especifica si el Correo electrónico de base de datos cifra la comunicación mediante Capa de sockets seguros (SSL). Utilice esta opción si se requiere SSL en el servidor SMTP. **enable_ssl** es de tipo bit no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Si se especifican el nombre y el Id. de cuenta, el procedimiento almacenado cambia el nombre de la cuenta además de actualizar su información. Cambiar el nombre de la cuenta puede ser útil para corregir errores en el nombre.  
  
 El procedimiento almacenado **sysmail_update_account_sp** está en el **msdb** la base de datos y es propiedad de la **dbo** esquema. El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permissions  
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
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. Cambio del nombre de una cuenta y de la información de una cuenta  
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
  
  
