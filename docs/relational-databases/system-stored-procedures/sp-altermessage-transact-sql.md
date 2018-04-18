---
title: sp_altermessage (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
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
- sp_altermessage_TSQL
- sp_altermessage
dev_langs:
- TSQL
helpviewer_keywords:
- sp_altermessage
ms.assetid: 1b28f280-8ef9-48e9-bd99-ec14d79abaca
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 969713a50ccb6b495c191f4262f6a6c837617bc2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spaltermessage-transact-sql"></a>sp_altermessage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica el estado de los mensajes definidos por el usuario o del sistema en una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Mensajes definidos por el usuario pueden verse mediante la **sys.messages** vista de catálogo.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_altermessage [ @message_id = ] message_number   ,[ @parameter = ]'write_to_log'  
   ,[ @parameter_value = ]'value'   
```  
  
## <a name="arguments"></a>Argumentos  
 [**@message_id =** ] *message_number*  
 Es el número de error del mensaje que se va a modificar desde **sys.messages**. *message_number* es **int** con ningún valor predeterminado.  
  
 [ **@parameter =** ] **'***write_to_log*'  
 Se utiliza con **@parameter_value** para indicar que el mensaje se escribirá en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] el registro de aplicación de Windows. *write_to_log* es **sysname** con ningún valor predeterminado. *write_to_log* se debe establecer en WITH_LOG o NULL. Si *write_to_log* se establece en WITH_LOG o NULL y el valor de **@parameter_value** es **true**, el mensaje se escribe en el registro de aplicación de Windows. Si *write_to_log* se establece en WITH_LOG o NULL y el valor de **@parameter_value** es **false**, el mensaje no siempre se escribe en el registro de aplicación de Windows, pero puede ser escribir en función de cómo se haya producido el error. Si *write_to_log* se especifica, el valor de **@parameter_value** también debe especificarse.  
  
> [!NOTE]  
>  Si se escribe un mensaje en el registro de aplicación Windows, también se escribe en el archivo de registro de errores del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 [ **@parameter_value =** ]**'***value*'  
 Se utiliza con **@parameter** para indicar que es el error se escriban en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] el registro de aplicación de Windows. *valor* es **varchar (5)**, sin valor predeterminado. Si **true**, el error siempre se escribe en el registro de aplicación de Windows. Si **false**, el error no siempre se escribe en el registro de aplicación de Windows, pero puede escribir en función de cómo se haya producido el error. Si *valor* se especifica, *write_to_log* para **@parameter** también debe especificarse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 El efecto de **sp_altermessage** con el WITH_LOG es similar del parámetro RAISERROR WITH LOG, salvo que opción **sp_altermessage** cambia el comportamiento de registro de un mensaje existente. Si se ha modificado un mensaje para que sea WITH_LOG, siempre se escribe en el registro de aplicación Windows, independientemente de cómo el usuario invoque el error. Aunque se ejecute RAISERROR sin la opción WITH_LOG, el error se escribe en el registro de aplicaciones de Windows.  
  
 Mensajes del sistema pueden modificarse mediante el uso de **sp_altermessage**.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **serveradmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se hace que el mensaje `55001` existente se registre en el registro de aplicación Windows.  
  
```  
EXECUTE sp_altermessage 55001, 'WITH_LOG', 'true';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
