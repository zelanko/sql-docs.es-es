---
title: sysmail_delete_log_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_log_sp_TSQL
- sysmail_delete_log_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_log_sp
ms.assetid: e94b37a1-70ad-46a5-86c0-721892156f7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb2db3e60d416324a413bf9d6eb69f6125bc00b5
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53588468"
---
# <a name="sysmaildeletelogsp-transact-sql"></a>sysmail_delete_log_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina eventos del registro del Correo electrónico de base de datos. Elimina todos los eventos del registro o los que cumplen criterios de fecha o tipo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_delete_log_sp  [ [ @logged_before = ] 'logged_before' ]  
    [, [ @event_type = ] 'event_type' ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@logged_before** =] **'**_logged_before_**'**  
 Elimina las entradas hasta la fecha y hora especificadas por el *logged_before* argumento. *logged_before* es **datetime** con NULL como valor predeterminado. NULL indica todas las fechas.  
  
 [ **@event_type** =] **'**_event_type_**'**  
 Elimina las entradas del tipo especificado como registro el *event_type*. *event_type* es **varchar (15)** no tiene ningún valor predeterminado. Las entradas válidas son **éxito**, **advertencia**, **error**, y **informativo**. NULL indica todos los tipos de evento.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Use la **sysmail_delete_log_sp** para eliminar permanentemente las entradas del registro de correo electrónico de base de datos de procedimiento almacenado. Un argumento opcional permite eliminar solo los registros antiguos indicando la fecha y la hora. Se eliminarán los eventos anteriores a ese argumento. Un argumento opcional permite eliminar solo los eventos de un tipo determinado, especificado como el **event_type** argumento.  
  
 Al eliminar entradas del registro del Correo electrónico de base de datos no se eliminan las entradas de mensajes de correo electrónico de las tablas del Correo electrónico de base de datos. Use [sysmail_delete_mailitems_sp](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md) para eliminar correo electrónico de las tablas del correo electrónico de base de datos.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede tener acceso a este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-deleting-all-events"></a>A. Eliminar todos los eventos  
 En el ejemplo siguiente se eliminan todos los eventos del registro del Correo electrónico de base de datos.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp ;  
GO  
```  
  
### <a name="b-deleting-the-oldest-events"></a>b. Eliminar los eventos más antiguos  
 En el ejemplo siguiente se eliminan los eventos del registro del Correo electrónico de base de datos anteriores al 9 de octubre de 2005.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @logged_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-events-of-a-certain-type"></a>C. Eliminar todos los eventos de un tipo determinado  
 En el ejemplo siguiente se eliminan los mensajes de operación correcta del registro del Correo electrónico de base de datos.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_log_sp  
    @event_type = 'success' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)   
 [Crear un trabajo del Agente SQL Server para archivar mensajes y registros de eventos del Correo electrónico de base de datos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
