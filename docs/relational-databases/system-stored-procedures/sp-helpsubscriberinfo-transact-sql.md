---
title: sp_helpsubscriberinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriberinfo
- sp_helpsubscriberinfo_TSQL
helpviewer_keywords:
- sp_helpsubscriberinfo
ms.assetid: fbabe1ec-57cf-425c-bae7-af7f5d3198fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14ab67bb9d69272960bbce3e1a7cfa059c609e3f
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53589809"
---
# <a name="sphelpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Presenta información acerca de un suscriptor. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@subscriber =** ] **'**_suscriptor_**'**  
 Es el nombre del suscriptor. *suscriptor* es **sysname**, su valor predeterminado es **%**, que devuelve toda la información.  
  
 [  **@publisher =** ] **'**_publisher_**'**  
 Es el nombre del publicador. *publicador* es **sysname**y el valor predeterminado es el nombre del servidor actual.  
  
> [!NOTE]  
>  *publicador* no debe especificarse, excepto cuando es un publicador de Oracle.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|Nombre del publicador.|  
|**suscriptor**|**sysname**|Nombre del suscriptor.|  
|**Tipo**|**tinyint**|Tipo de suscriptor:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos **1** = origen de datos ODBC|  
|**inicio de sesión**|**sysname**|Id. de inicio de sesión para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**sysname**|Contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**commit_batch_size**|**int**|No compatible.|  
|**status_batch_size**|**int**|No compatible.|  
|**flush_frequency**|**int**|No compatible.|  
|**frequency_type**|**int**|Frecuencia de ejecución del agente de distribución:<br /><br /> **1** = una vez<br /><br /> **2** = a petición<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente relativa<br /><br /> **64** = inicio automático<br /><br /> **128** = periódica|  
|**frequency_interval**|**int**|Valor que se aplica a la frecuencia establecida por *frequency_type*.|  
|**frequency_relative_interval**|**int**|Fecha del agente de distribución utilizada cuando *frequency_type* está establecido en **32** (mensual relativa):<br /><br /> **1** = primero<br /><br /> **2** = segundo<br /><br /> **4** = tercero<br /><br /> **8** = cuarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor**|**int**|Factor de periodicidad utilizado por *frequency_type*.|  
|**frequency_subday**|**int**|Frecuencia de repetición de la programación durante el periodo definido:<br /><br /> **1** = una vez<br /><br /> **2** = segundo<br /><br /> **4** = minuto<br /><br /> **8** = hora|  
|**frequency_subday_interval**|**int**|Intervalo para *frequency_subday*.|  
|**active_start_time_of_day**|**int**|Hora del día en que el agente de distribución se programa por primera vez, con el formato HHMMSS.|  
|**active_end_time_of_day**|**int**|Hora del día en que el agente de distribución deja de estar programado, con el formato HHMMSS.|  
|**active_start_date**|**int**|Fecha en que el agente de distribución se programa por primera vez, con el formato AAAAMMDD.|  
|**active_end_date**|**int**|Fecha en la que el agente de distribución deja de estar programado, con el formato AAAAMMDD.|  
|**retryattempt**|**int**|No compatible.|  
|**retryDelay**|**int**|No compatible.|  
|**description**|**nvarchar(255)**|Descripción del suscriptor.|  
|**security_mode**|**int**|Modo de seguridad implementado.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de Windows|  
|**frequency_type2**|**int**|Frecuencia de ejecución del Agente de mezcla:<br /><br /> **1** = una vez<br /><br /> **2** = a petición<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente relativa<br /><br /> **64** = inicio automático<br /><br /> **128** = periódica|  
|**frequency_interval2**|**int**|Valor que se aplica a la frecuencia establecida por *frequency_type*.|  
|**frequency_relative_interval2**|**int**|Fecha del agente de mezcla utiliza cuando *frequency_type* está establecido en 32 (mensual relativa):<br /><br /> **1** = primero<br /><br /> **2** = segundo<br /><br /> **4** = tercero<br /><br /> **8** = cuarto<br /><br /> **16** = último|  
|**frequency_recurrence_factor2**|**int**|Factor de periodicidad utilizado por *frequency_type **.*|  
|**frequency_subday2**|**int**|Frecuencia de repetición de la programación durante el periodo definido:<br /><br /> **1** = una vez<br /><br /> **2** = segundo<br /><br /> **4** = minuto<br /><br /> **8** = hora|  
|**frequency_subday_interval2**|**int**|Intervalo para *frequency_subday*.|  
|**active_start_time_of_day2**|**int**|Hora del día en que el Agente de mezcla se programa por primera vez, con el formato HHMMSS.|  
|**active_end_time_of_day2**|**int**|Hora del día en que el Agente de mezcla deja de estar programado, con el formato HHMMSS.|  
|**active_start_date2**|**int**|Fecha en que el Agente de mezcla se programa por primera vez, con el formato AAAAMMDD.|  
|**active_end_date2**|**int**|Fecha en la que el Agente de mezcla deja de estar programado, con el formato AAAAMMDD.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpsubscriberinfo** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos o la lista de acceso de publicación para la publicación puede ejecutar **sp_helpsubscriberinfo**.  
  
## <a name="see-also"></a>Vea también  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
