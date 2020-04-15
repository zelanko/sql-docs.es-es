---
title: sysmail_update_account_sp (Transact-SQL) Microsoft Docs
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
ms.openlocfilehash: 3dd772a1519ea856cac0302d31be9eb7d0f9d782
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283231"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
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
`[ @account_id = ] account_id`El ID de cuenta que se debe actualizar. *account_id* es **int**, con un valor predeterminado de NULL. Debe especificarse al menos una de *account_id* o *account_name.* Si se especifican los dos, el procedimiento cambia el nombre de la cuenta.  
  
`[ @account_name = ] 'account_name'`El nombre de la cuenta que se desea actualizar. *account_name* es **sysname**, con un valor predeterminado de NULL. Debe especificarse al menos una de *account_id* o *account_name.* Si se especifican los dos, el procedimiento cambia el nombre de la cuenta.  
  
`[ @email_address = ] 'email_address'`La nueva dirección de correo electrónico desde la que enviar el mensaje. Esta dirección debe ser una dirección de correo electrónico de Internet. El nombre de servidor de la dirección es el servidor que Database Mail utiliza para enviar correo de esta cuenta. *email_address* es **nvarchar(128)**, con un valor predeterminado de NULL.  
  
`[ @display_name = ] 'display_name'`El nuevo nombre para mostrar que se usará en los mensajes de correo electrónico de esta cuenta. *display_name* es **nvarchar(128)**, sin valor predeterminado.  
  
`[ @replyto_address = ] 'replyto_address'`La nueva dirección que se usará en el encabezado Responder a de los mensajes de correo electrónico de esta cuenta. *replyto_address* es **nvarchar(128)**, sin valor predeterminado.  
  
`[ @description = ] 'description'`La nueva descripción de la cuenta. *description* es **nvarchar(256)**, con un valor predeterminado de NULL.  
  
`[ @mailserver_name = ] 'server_name'`El nuevo nombre del servidor de correo SMTP que se usará para esta cuenta. El equipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta debe ser capaz de resolver el *server_name* en una dirección IP. *server_name* es **sysname**, sin valor predeterminado.  
  
`[ @mailserver_type = ] 'server_type'`El nuevo tipo del servidor de correo. *server_type* es **sysname**, sin valor predeterminado. Solo se admite un valor de **'SMTP'.**  
  
`[ @port = ] port_number`El nuevo número de puerto del servidor de correo. *port_number* es **int**, sin valor predeterminado.  
  
`[ @timeout = ] 'timeout'`Parámetro de tiempo de espera para SmtpClient.Send de un único mensaje de correo electrónico. *El tiempo de espera* es **int** en segundos, sin valor predeterminado.  
  
`[ @username = ] 'username'`El nuevo nombre de usuario que se usará para iniciar sesión en el servidor de correo. *El nombre* de usuario es **sysname**, sin valor predeterminado.  
  
`[ @password = ] 'password'`La nueva contraseña que se usará para iniciar sesión en el servidor de correo. *contraseña* es **sysname**, sin valor predeterminado.  
  
`[ @use_default_credentials = ] use_default_credentials`Especifica si se debe enviar el correo al servidor [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] SMTP con las credenciales del servicio. **use_default_credentials** es bit, sin valor predeterminado. Si el valor de este parámetro es 1, el Correo electrónico de base de datos usa las credenciales de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cuando este parámetro es 0, Correo electrónico de base de datos utiliza el ** \@nombre de usuario** y ** \@** la contraseña para la autenticación en el servidor SMTP. Si ** \@el nombre de usuario** y ** \@** la contraseña son NULL, entonces usará la autenticación anónima. Consulte con el administrador de SMTP antes de especificar este parámetro.  
  
`[ @enable_ssl = ] enable_ssl`Especifica si Correo electrónico de base de datos cifra la comunicación mediante Seguridad de la capa de transporte (TLS), anteriormente conocida como Capa de sockets seguros (SSL). Utilice esta opción si se requiere TLS en el servidor SMTP. **enable_ssl** es bit, sin valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (éxito) o **1** (fallo)  
  
## <a name="remarks"></a>Observaciones  
 Si se especifican el nombre y el Id. de cuenta, el procedimiento almacenado cambia el nombre de la cuenta además de actualizar su información. Cambiar el nombre de la cuenta puede ser útil para corregir errores en el nombre.  
  
 El procedimiento almacenado **sysmail_update_account_sp** está en la base de datos **msdb** y es propiedad del esquema **dbo.** El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-information-for-an-account"></a>A. Cambio de la información de una cuenta  
 En el ejemplo `AdventureWorks Administrator` siguiente se actualiza la cuenta en la base de datos **msdb.** La información de la cuenta se establece con los valores proporcionados.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Correo de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Crear una cuenta de correo de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimientos almacenados del correo electrónico de base de datos &#40;&#41;de Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
