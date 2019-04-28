---
title: sp_changesubscriber (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f31a00e0c42bc56dffac191ff9a934bb77b95df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62997803"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las opciones de un suscriptor. Se actualizan todas las tareas de distribución de los suscriptores de este publicador. Este procedimiento almacenado se escribe en el **MSsubscriber_info** tabla en la base de datos de distribución. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @subscriber = ] 'subscriber'` Es el nombre del suscriptor en el que se va a cambiar las opciones. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @type = ] type` Es el tipo de suscriptor. *tipo* es **tinyint**, su valor predeterminado es null. **0** indica un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptor. **1** especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otro servidor de origen de datos ODBC suscriptor.  
  
`[ @login = ] 'login'` Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Id. de inicio de sesión de autenticación. *login* es de tipo **sysname** y su valor predeterminado es NULL.  
  
`[ @password = ] 'password'` Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contraseña de autenticación. *contraseña* es **sysname**, su valor predeterminado es **%**. **%** indica que no hay ningún cambio en la propiedad de contraseña.  
  
`[ @commit_batch_size = ] commit_batch_size` Se admiten por razones de compatibilidad.  
  
`[ @status_batch_size = ] status_batch_size` Se admiten por razones de compatibilidad.  
  
`[ @flush_frequency = ] flush_frequency` Se admiten por razones de compatibilidad.  
  
`[ @frequency_type = ] frequency_type` Es la frecuencia con que se programa la tarea de distribución. *frequency_type* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
  
`[ @frequency_interval = ] frequency_interval` Es el intervalo de *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es null.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` Es la fecha de la tarea de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Es con qué frecuencia debe repetirse la tarea de distribución durante la definido *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
`[ @frequency_subday = ] frequency_subday` Es la frecuencia con la que volver a programar durante el período definido. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` Es el intervalo de *frequence_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` Es la hora del día en la tarea de distribución se primer programa, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` Es la hora del día en que la tarea de distribución deja de estar programado, con el formato HHMMSS. *active_end_time_of_day*es **int**, su valor predeterminado es null.  
  
`[ @active_start_date = ] active_start_date` Es la fecha en la tarea de distribución programada, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
`[ @active_end_date = ] active_end_date` Es la fecha en la tarea de distribución deja de estar programado, con el formato AAAAMMDD. *active_end_date*es **int**, su valor predeterminado es null.  
  
`[ @description = ] 'description'` Es una descripción opcional. *descripción* es **nvarchar (255)**, su valor predeterminado es null.  
  
`[ @security_mode = ] security_mode` Es el modo de seguridad implementado. *security_mode* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticación|  
|**1**|Autenticación de Windows|  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse cuando se cambia las propiedades del artículo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubscriber** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_changesubscriber**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
