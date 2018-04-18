---
title: sp_changesubscriber_schedule (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9aa99834cda2085a60df8f148b457da52b33b6bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spchangesubscriberschedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la programación del Agente de distribución o del Agente de mezcla para un suscriptor. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@subscriber=**] **'***suscriptor***'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**. El nombre del suscriptor tiene que ser único en la base de datos, no puede existir previamente y no puede ser NULL.  
  
 [  **@agent_type=**] *tipo*  
 Es el tipo de agente. *tipo de* es **smallint**, su valor predeterminado es **0**. **0** indica un agente de distribución. **1** indica un agente de mezcla.  
  
 [  **@frequency_type=**] *frequency_type*  
 Es la frecuencia con que se programa la tarea de distribución. *frequency_type* es **int**, su valor predeterminado es **64**. Hay 10 columnas de programación.  
  
 [  **@frequency_interval=**] *frequency_interval*  
 Es el valor que se aplica a la frecuencia establecida *frequency_type*. *frequency_interval* es **int**, su valor predeterminado es **1**.  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 Es la fecha de la tarea de distribución. *frequency_relative_interval* es **int**, su valor predeterminado es **1**.  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es **0**.  
  
 [  **@frequency_subday=**] *frequency_subday*  
 Indica la frecuencia, en minutos, con que se reprograma durante el período definido. *frequency_subday* es **int**, su valor predeterminado es **4**.  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es **5**.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que la tarea de distribución se programa por primera vez. *active_start_time_of_day* es **int**, su valor predeterminado es **0**.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora del día en que la tarea de distribución deja de estar programada. *active_end_time_of_day* es **int**, su valor predeterminado es **235959**, lo que significa 11:59:59 p. M. en un reloj de 24 horas.  
  
 [  **@active_start_date=**] *active_start_date*  
 Es la fecha en que la tarea de distribución se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es **0**.  
  
 [  **@active_end_date=**] *active_end_date*  
 Es la fecha en la que la tarea de distribución deja de estar programada, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es **99991231**, lo que significa 31 de diciembre de 9999.  
  
 [ **@publisher**=] **'***publisher***'**  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse al cambiar las propiedades de artículo en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubscriber_schedule** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_changesubscriber_schedule**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addsubscriber_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
