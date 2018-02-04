---
title: sp_notify_operator (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7683e0150c41810c14981e0c6b6364c59ae19ae3
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="spnotifyoperator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envía un mensaje de correo electrónico a un operador mediante el Correo electrónico de base de datos.  
  
 
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_name=** ] **'***profilename***'**  
 Nombre del perfil de Correo electrónico de base de datos que se va a utilizar para enviar el mensaje. *ProfileName* es **nvarchar (128)**. Si *profilename* no se especifica, se usa el perfil de correo electrónico de base de datos predeterminado.  
  
 [ **@id=** ] *id*  
 Identificador del operador al que se va a enviar el mensaje. *Id. de* es **int**, su valor predeterminado es null. Uno de *identificador* o *nombre* debe especificarse.  
  
 [  **@name=** ] **'***nombre***'**  
 Nombre del operador al que se va a enviar el mensaje. *nombre* es **nvarchar (128)**, su valor predeterminado es null. Uno de *identificador* o *nombre* debe especificarse.  
  
> **Nota:** una dirección de correo electrónico debe definirse para el operador para poder recibir mensajes.  
  
 [  **@subject=** ] **'***asunto***'**  
 El asunto del mensaje de correo electrónico. *asunto* es **nvarchar (256)** no tiene ningún valor predeterminado.  
  
 [  **@body=** ] **'***mensaje***'**  
 Cuerpo del mensaje de correo electrónico. *mensaje* es **nvarchar (max)** no tiene ningún valor predeterminado.  
  
 [  **@file_attachments=** ] **'***datos adjuntos***'**  
 Nombre de un archivo que se va a adjuntar al mensaje de correo electrónico. *datos adjuntos* es **nvarchar (512)**, no tiene ningún valor predeterminado.  
  
 [ **@mail_database=** ] **'***mail_host_database***'**  
 Especifica el nombre de la base de datos host de correo. *mail_host_database* is **nvarchar(128)**. Si no hay ningún *mail_host_database* se especifica, el **msdb** base de datos se utiliza de forma predeterminada.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Envía el mensaje especificado a la dirección de correo electrónico del operador especificado. Si el operador no tiene configurada una dirección de correo electrónico, generará un error.  
  
 El Correo electrónico de base de datos y la base de datos host de correo deben configurarse antes de que se pueda enviar una notificación al operador.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra cómo enviar una notificación de correo electrónico al operador `François Ajenstat` mediante el perfil de base de datos de correo electrónico de `AdventureWorks Administrator`. El asunto del mensaje de correo electrónico es `Test Notification`. El mensaje de correo electrónico indica que se trata de una notificación de prueba por correo electrónico.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Agente SQL Server almacena procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
