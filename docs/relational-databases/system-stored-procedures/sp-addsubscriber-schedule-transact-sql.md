---
title: sp_addsubscriber_schedule (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber_schedule_TSQL
- sp_addsubscriber_schedule
helpviewer_keywords:
- sp_addsubscriber_schedule
ms.assetid: a6225033-5c3b-452f-ae52-79890a3590ed
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fb643c0be953bcff19341f681654f2565be3d9e0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716374"
---
# <a name="sp_addsubscriber_schedule-transact-sql"></a>sp_addsubscriber_schedule (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Agrega una programación para el Agente de distribución y el Agente de mezcla. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addsubscriber_schedule [ @subscriber = ] 'subscriber'  
    [ , [ @agent_type = ] agent_type ]  
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
`[ @subscriber = ] 'subscriber'`Es el nombre del suscriptor. el *suscriptor* es de **tipo sysname**. El nombre del suscriptor tiene que ser único en la base de datos, no puede existir previamente y no puede ser NULL.  
  
`[ @agent_type = ] agent_type`Es el tipo de agente. *agent_type* es **smallint**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Agente de distribución|  
|**1**|Agente de mezcla|  
  
`[ @frequency_type = ] frequency_type`Es la frecuencia con la que se programa el Agente de distribución. *frequency_type* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Diario|  
|**8**|Cada semana|  
|**16**|Mensual|  
|**32**|Mensualmente relativa|  
|**64** (valor predeterminado)|Iniciar automáticamente|  
|**128**|Periódica|  
  
`[ @frequency_interval = ] frequency_interval`Es el valor que se va a aplicar a la frecuencia establecida por *frequency_type*. *frequency_interval* es de **tipo int**y su valor predeterminado es **1**.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`Es la fecha del Agente de distribución. Este parámetro se utiliza cuando *frequency_type* se establece en **32** (relativo mensual). *frequency_relative_interval* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1** (predeterminado)|First|  
|**2**|Second|  
|**4**|Tercero|  
|**8**|Cuarto|  
|**16**|Último|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @frequency_subday = ] frequency_subday`Es la frecuencia con que se vuelve a programar durante el período definido. *frequency_subday* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una sola vez|  
|**2**|Second|  
|**4** (valor predeterminado)|Minute|  
|**8**|Hora|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`Es el intervalo de *frequency_subday*. *frequency_subday_interval* es de **tipo int**y su valor predeterminado es **5**.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`Es la hora del día a la que se programa el Agente de distribución por primera vez, con el formato HHMMSS. *active_start_time_of_day* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`Es la hora del día en que el Agente de distribución deja de estar programado, con el formato HHMMSS. *active_end_time_of_day*es de **tipo int**y su valor predeterminado es 235959, lo que significa 11:59:59 P.M. tal y como se mide en un reloj de 24 horas.  
  
`[ @active_start_date = ] active_start_date`Es la fecha en la que se programa el Agente de distribución por primera vez, con el formato AAAAMMDD. *active_start_date* es de **tipo int**y su valor predeterminado es **0**.  
  
`[ @active_end_date = ] active_end_date`Es la fecha en la que el Agente de distribución deja de estar programado, con el formato AAAAMMDD. *active_end_date* es de **tipo int**, con un valor predeterminado de 99991231, que significa el 31 de diciembre de 9999.  
  
`[ @publisher = ] 'publisher'`Especifica un publicador que no es de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *Publisher* es de **tipo sysname y su**valor predeterminado es NULL.  
  
> [!NOTE]  
>  no se debe especificar el *publicador* para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addsubscriber_schedule** se utiliza en la replicación de instantáneas, la replicación transaccional y la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_addsubscriber_schedule**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_changesubscriber_schedule &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changesubscriber-schedule-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
