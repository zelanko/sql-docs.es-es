---
title: sp_changesubscriber (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c2cb0047dd66b0c3fd96d399e404b801401d202a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las opciones de un suscriptor. Se actualizan todas las tareas de distribución de los suscriptores de este publicador. Este procedimiento almacenado escribe en el **MSsubscriber_info** tabla en la base de datos de distribución. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
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
 [  **@subscriber=**] **'***suscriptor***'**  
 Es el nombre del suscriptor donde se van a cambiar las opciones. *suscriptor* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@type=**] *tipo*  
 Es el tipo de suscriptor. *tipo de* es **tinyint**, su valor predeterminado es null. **0** indica un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptor. **1** especifica no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u otro servidor de origen de datos ODBC suscriptor.  
  
 [  **@login=**] **'***inicio de sesión***'**  
 Es el identificador de inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *login* es de tipo **sysname** y su valor predeterminado es NULL.  
  
 [  **@password=**] **'***contraseña***'**  
 Es el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contraseña de autenticación. *contraseña* es **sysname**, su valor predeterminado es **%**. **%** indica que no hay ningún cambio en la propiedad de contraseña.  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 Se admite únicamente por compatibilidad con versiones anteriores.  
  
 [  **@status_batch_size=**] *status_batch_size*  
 Se admite únicamente por compatibilidad con versiones anteriores.  
  
 [  **@flush_frequency=**] *flush_frequency*  
 Se admite únicamente por compatibilidad con versiones anteriores.  
  
 [  **@frequency_type=**] *frequency_type*  
 Es la frecuencia con que se programa la tarea de distribución. *frequency_type* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 Es el intervalo de *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Es la fecha de la tarea de distribución. Este parámetro se utiliza cuando *frequency_type* está establecido en **32** (relativo mensual). *frequency_relative_interval* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Primero|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Es la frecuencia con la tarea de distribución se repetirá periódicamente durante las personalizaciones definidas *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Es la frecuencia de repetición de la programación durante el periodo definido. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es el intervalo de *frequence_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que la tarea de distribución se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora del día en que la tarea de distribución deja de estar programada, con el formato HHMMSS. *active_end_time_of_day*es **int**, su valor predeterminado es null.  
  
 [  **@active_start_date=**] *active_start_date*  
 Es la fecha en que la tarea de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_date=**] *active_end_date*  
 Es la fecha en la que la tarea de distribución deja de estar programada, con el formato AAAAMMDD. *active_end_date*es **int**, su valor predeterminado es null.  
  
 [  **@description=**] **'***descripción***'**  
 Es una descripción opcional. *descripción* es **nvarchar (255)**, su valor predeterminado es null.  
  
 [  **@security_mode=**] *security_mode*  
 Es el modo de seguridad implementado. *security_mode* es **int**, y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticación|  
|**1**|Autenticación de Windows|  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica un publicador que no es de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse al cambiar las propiedades de artículo en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubscriber** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_changesubscriber**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
