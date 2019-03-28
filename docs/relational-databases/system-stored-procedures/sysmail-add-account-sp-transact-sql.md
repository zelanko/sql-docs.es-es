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
manager: craigg
ms.openlocfilehash: 3b41b0c0ae805923a10d0ee9c4fd066b1202fa94
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537897"
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una nueva cuenta de Correo electrónico de base de datos que contiene información sobre una cuenta SMTP.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @account_name = ] 'account_name'` El nombre de la cuenta para agregar. *account_name* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @email_address = ] 'email_address'` La dirección de correo electrónico para enviar el mensaje desde. Esta dirección debe ser una dirección de correo electrónico de Internet. *Email_Address* es **nvarchar (128)**, no tiene ningún valor predeterminado. Por ejemplo, una cuenta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente puede enviar correo electrónico desde la dirección **SqlAgent@Adventure-Works.com**.  
  
`[ @display_name = ] 'display_name'` El nombre para mostrar que utilizará en los mensajes de correo electrónico desde esta cuenta. *display_name* es **nvarchar (128)**, su valor predeterminado es null. Por ejemplo, una cuenta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente puede mostrar el nombre **SQL Server Agent Automated Mailer** en mensajes de correo electrónico.  
  
`[ @replyto_address = ] 'replyto_address'` La dirección que se envían las respuestas a los mensajes desde esta cuenta. *replyto_address* es **nvarchar (128)**, su valor predeterminado es null. Por ejemplo, las respuestas a una cuenta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente pueden dirigirse al administrador de la base de datos, **danw@Adventure-Works.com**.  
  
`[ @description = ] 'description'` Es una descripción para la cuenta. *descripción* es **nvarchar (256)**, su valor predeterminado es null.  
  
`[ @mailserver_name = ] 'server_name'` El nombre o dirección IP del servidor de correo SMTP que se usará para esta cuenta. El equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser capaz de resolver el *nombre_servidor* en una dirección IP. *nombre_servidor* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @mailserver_type = ] 'server_type'` El tipo de servidor de correo electrónico. *server_type* es **sysname**, su valor predeterminado es **'SMTP'**...  
  
`[ @port = ] port_number` El número de puerto para el servidor de correo electrónico. *número_puerto* es **int**, su valor predeterminado es 25.  
  
`[ @username = ] 'username'` Nombre de usuario que se va a usar para iniciar sesión en el servidor de correo electrónico. *nombre de usuario* es **nvarchar (128)**, su valor predeterminado es null. Cuando este parámetro es NULL, el Correo electrónico de base de datos no utiliza la autenticación para esta cuenta. Si el servidor de correo no requiere autenticación, utilice NULL para el nombre de usuario.  
  
`[ @password = ] 'password'` La contraseña que se utilizará para iniciar sesión en el servidor de correo electrónico. *contraseña* es **nvarchar (128)**, su valor predeterminado es null. No es necesario proporcionar una contraseña, a menos que se especifique un nombre de usuario.  
  
`[ @use_default_credentials = ] use_default_credentials` Especifica si se debe enviar el correo al servidor SMTP con las credenciales de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. **use_default_credentials** es bit y su valor predeterminado es 0. Si el valor de este parámetro es 1, el Correo electrónico de base de datos usa las credenciales de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cuando este parámetro es 0, correo electrónico de base de datos envía el **@username** y **@password** parámetros si está presente, de lo contrario envía correo sin **@username**y **@password** parámetros.  
  
`[ @enable_ssl = ] enable_ssl` Especifica si se cifra la comunicación mediante capa de Sockets seguros de correo electrónico de base de datos. **Enable_ssl** es bit y su valor predeterminado es 0.  
  
`[ @account_id = ] account_id OUTPUT` Devuelve el identificador de cuenta para la nueva cuenta. *account_id* es **int**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Correo electrónico de base de datos proporciona parámetros distintos para **@email_address**, **@display_name**, y **@replyto_address**. El **@email_address** parámetro es la dirección desde la que se envía el mensaje. El **@display_name** parámetro es el nombre que se muestra en el **desde:** campo de mensaje de correo electrónico. El **@replyto_address** parámetro es la dirección donde se enviarán las respuestas al mensaje de correo electrónico. Por ejemplo, una cuenta utilizada para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede enviar mensajes de correo electrónico desde una dirección de correo que solo se utiliza para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los mensajes procedentes de esa dirección deberían mostrar un nombre descriptivo, de manera que los destinatarios puedan determinar fácilmente que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envió el mensaje. Si un destinatario responde al mensaje, la respuesta debería dirigirse al administrador de base de datos en lugar de a la dirección utilizada por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En este escenario, se usa la cuenta **SqlAgent@Adventure-Works.com** como la dirección de correo electrónico. El nombre para mostrar se establece en **SQL Server Agent Automated Mailer**. La cuenta utiliza **danw@Adventure-Works.com** como la dirección de respuesta, por lo que las respuestas a los mensajes enviados desde esta cuenta Ir al administrador de base de datos en lugar de la dirección de correo electrónico [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Al proporcionar valores independientes para estos tres parámetros, el Correo electrónico de base de datos le permite configurar los mensajes en función de sus necesidades.  
  
 El **@mailserver_type** parámetro admite el valor **'SMTP'**.  
  
 Cuando **@use_default_credentials** es 1, el correo se envía al servidor SMTP con las credenciales de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Cuando **@use_default_credentials** es 0 y un **@username** y **@password** se especifican para una cuenta, la cuenta utiliza la autenticación SMTP. El **@username** y **@password** son las credenciales de la cuenta se usa para el servidor SMTP, no las credenciales para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la red que el equipo esté encendido.  
  
 El procedimiento almacenado **sysmail_add_account_sp** está en el **msdb** de base de datos y que pertenece el **dbo** esquema. El procedimiento debe ejecutarse con un nombre de tres partes si la base de datos actual no es **msdb**.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de este procedimiento de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una cuenta denominada `AdventureWorks Administrator`. Esta cuenta utiliza la dirección de correo electrónico `dba@Adventure-Works.com` y envía los mensajes al servidor de correo SMTP `smtp.Adventure-Works.com`. Los mensajes enviados desde esta cuenta muestran `AdventureWorks Automated Mailer` en el **desde:** línea del mensaje. Las respuestas a los mensajes se dirigen a `danw@Adventure-Works.com`.  
  
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
 [Crear una cuenta de correo electrónico de base de datos](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
