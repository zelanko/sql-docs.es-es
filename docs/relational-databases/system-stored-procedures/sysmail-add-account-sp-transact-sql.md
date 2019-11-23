---
title: sysmail_add_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: stevestein
ms.author: sstein
ms.openlocfilehash: d382d8ee7a871244213467b7a46bdc5b864c55cb
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381900"
---
# <a name="sysmail_add_account_sp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crea una nueva cuenta de Correo electrónico de base de datos que contiene información sobre una cuenta SMTP.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @account_name = ] 'account_name'` el nombre de la cuenta que se va a agregar. *account_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @email_address = ] 'email_address'` la dirección de correo electrónico de la que se va a enviar el mensaje. Esta dirección debe ser una dirección de correo electrónico de Internet. *EMAIL_ADDRESS* es de tipo **nvarchar (128)** y no tiene ningún valor predeterminado. Por ejemplo, una cuenta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente puede enviar correo electrónico desde la dirección **SqlAgent\@Adventure-Works.com**.  
  
`[ @display_name = ] 'display_name'` el nombre para mostrar que se va a usar en los mensajes de correo electrónico de esta cuenta. *display_name* es de tipo **nvarchar (128)** y su valor predeterminado es NULL. Por ejemplo, una cuenta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente puede mostrar el nombre **Agente SQL Server el envío automático** de correo en los mensajes de correo electrónico.  
  
`[ @replyto_address = ] 'replyto_address'` la dirección a la que se envían las respuestas a los mensajes de esta cuenta. *replyto_address* es de tipo **nvarchar (128)** y su valor predeterminado es NULL. Por ejemplo, las respuestas a una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente pueden dirigirse al administrador de la base de datos, **danw\@Adventure-Works.com**.  
  
`[ @description = ] 'description'` es una descripción de la cuenta. la *Descripción* es de tipo **nvarchar (256)** y su valor predeterminado es NULL.  
  
`[ @mailserver_name = ] 'server_name'` el nombre o la dirección IP del servidor de correo SMTP que se va a usar para esta cuenta. El equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser capaz de resolver el *SERVER_NAME* en una dirección IP. *SERVER_NAME* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @mailserver_type = ] 'server_type'` el tipo de servidor de correo electrónico. *server_type* es de **tipo sysname y su**valor predeterminado es **"SMTP"** .  
  
`[ @port = ] port_number` el número de puerto del servidor de correo electrónico. *port_number* es de **tipo int**y su valor predeterminado es 25.  
  
`[ @username = ] 'username'` el nombre de usuario que se utilizará para iniciar sesión en el servidor de correo electrónico. *username* es de tipo **nvarchar (128)** y su valor predeterminado es NULL. Cuando este parámetro es NULL, el Correo electrónico de base de datos no utiliza la autenticación para esta cuenta. Si el servidor de correo no requiere autenticación, utilice NULL para el nombre de usuario.  
  
`[ @password = ] 'password'` la contraseña que se utilizará para iniciar sesión en el servidor de correo electrónico. *password* es de tipo **nvarchar (128)** y su valor predeterminado es NULL. No es necesario proporcionar una contraseña, a menos que se especifique un nombre de usuario.  
  
`[ @use_default_credentials = ] use_default_credentials` especifica si se debe enviar el correo al servidor SMTP con las credenciales de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** es de bit y su valor predeterminado es 0. Si el valor de este parámetro es 1, el Correo electrónico de base de datos usa las credenciales de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cuando este parámetro es 0, Correo electrónico de base de datos envía los parámetros **\@username** y **\@password** si están presentes; de lo contrario, envía correo sin **\@parámetros username** y **\@password** .  
  
`[ @enable_ssl = ] enable_ssl` especifica si Correo electrónico de base de datos cifra la comunicación mediante Capa de sockets seguros. **Enable_ssl** es de bit y su valor predeterminado es 0.  
  
`[ @account_id = ] account_id OUTPUT` devuelve el identificador de la cuenta nueva. *ACCOUNT_ID* es de **tipo int**y su valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Remarks  
 Correo electrónico de base de datos proporciona parámetros independientes para **\@EMAIL_ADDRESS**, **\@display_name** **y\@replyto_address.** La **\@EMAIL_ADDRESS** parámetro es la dirección desde la que se envía el mensaje. El **\@display_name** parámetro es el nombre que se muestra en el campo **de:** del mensaje de correo electrónico. El **\@replyto_address** parámetro es la dirección a la que se enviarán las respuestas al mensaje de correo electrónico. Por ejemplo, una cuenta utilizada para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede enviar mensajes de correo electrónico desde una dirección de correo que solo se utiliza para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los mensajes procedentes de esa dirección deberían mostrar un nombre descriptivo, de manera que los destinatarios puedan determinar fácilmente que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envió el mensaje. Si un destinatario responde al mensaje, la respuesta debería dirigirse al administrador de base de datos en lugar de a la dirección utilizada por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este escenario, la cuenta utiliza **SqlAgent@Adventure-Works.com** como dirección de correo electrónico. El nombre para mostrar está establecido en **Agente SQL Server Automated Mailer**. La cuenta usa **danw@Adventure-Works.com** como dirección de respuesta, por lo que las respuestas a los mensajes enviados desde esta cuenta van al administrador de bases de datos en lugar de a la dirección de correo electrónico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Al proporcionar valores independientes para estos tres parámetros, el Correo electrónico de base de datos le permite configurar los mensajes en función de sus necesidades.  
  
 El parámetro **mailserver_type de\@** admite el valor **' SMTP '** .  
  
 Cuando **\@use_default_credentials** es 1 el correo se envía al servidor SMTP con las credenciales de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Cuando **\@use_default_credentials** es 0 y se especifica un **nombre de usuario\@** y una **contraseña de\@** para una cuenta, la cuenta utiliza la autenticación SMTP. Los **\@nombre de usuario** y **\@contraseña** son las credenciales que utiliza la cuenta para el servidor SMTP, no las credenciales para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la red en la que se encuentra el equipo.  
  
 El procedimiento almacenado **sysmail_add_account_sp** está en la base de datos **msdb** y pertenece al esquema **DBO** . El procedimiento se debe ejecutar con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución para este procedimiento tienen como valor predeterminado los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una cuenta denominada `AdventureWorks Administrator`. Esta cuenta utiliza la dirección de correo electrónico `dba@Adventure-Works.com` y envía los mensajes al servidor de correo SMTP `smtp.Adventure-Works.com`. Los mensajes de correo electrónico enviados desde esta cuenta muestran `AdventureWorks Automated Mailer` en la línea **de:** del mensaje. Las respuestas a los mensajes se dirigen a `danw@Adventure-Works.com`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)   
 [Cree una cuenta de Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimientos &#40;almacenados de correo electrónico de base de datos TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
