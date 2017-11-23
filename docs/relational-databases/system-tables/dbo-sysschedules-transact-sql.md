---
title: dbo.sysschedules (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs: TSQL
helpviewer_keywords: sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6d97d48155a5f9ff41ee8255e9a28a8c1c82443d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre las programaciones de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en la **msdb** base de datos.  
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|Id. de la programación de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**valor schedule_uid**|**uniqueidentifier**|Identificador único de la programación de trabajo. Este valor se utiliza para identificar una programación de trabajos distribuidos.|  
|**originating_server_id**|**int**|Id. del servidor maestro del que procede la programación de trabajo.|  
|**Nombre**|**sysname (nvarchar(128))**|Nombre de la programación de trabajo definido por el usuario. Este nombre debe ser único en un trabajo.|  
|**owner_sid**|**varbinary (85)**|Microsoft Windows *security_identifier* del usuario o grupo que posee la programación de trabajo.|  
|**habilitado**|**int**|Estado de la programación de trabajo:<br /><br /> **0** = no habilitado.<br /><br /> **1** = habilitado.<br /><br /> Si la programación no está habilitada, no se ejecutarán trabajos en la programación.|  
|**freq_type**|**int**|Frecuencia con la que un trabajo se ejecuta para esta programación.<br /><br /> **1** = una sola vez<br /><br /> **4** = diariamente<br /><br /> **8** = semanalmente<br /><br /> **16** = mensualmente<br /><br /> **32** = mensualmente, relativo a **freq_interval**<br /><br /> **64** = se ejecuta al iniciar el servicio Agente SQL Server<br /><br /> **128** = se ejecuta cuando el equipo está inactivo|  
|**freq_interval**|**int**|Días en que se ejecuta el trabajo. Depende del valor de **freq_type**. El valor predeterminado es **0**, lo que indica que **freq_interval** no se utiliza. Consulte la tabla siguiente para los valores posibles y sus efectos.|  
|**freq_subday_type**|**int**|Unidades para el **freq_subday_interval**. Éstos son los valores posibles y sus descripciones.<br /><br /> <br /><br /> **1** : a la hora especificada<br /><br /> **2** : segundos<br /><br /> **4** : minutos<br /><br /> **8** : horas|  
|**freq_subday_interval**|**int**|Número de **freq_subday_type** períodos que transcurren entre cada ejecución del trabajo.|  
|**freq_relative_interval**|**int**|Cuando **freq_interval** se produce en cada mes, si **freq_interval** es **32** (relativo mensual). Puede ser uno de los siguientes valores:<br /><br /> **0** = **freq_relative_interval** no se utiliza<br /><br /> **1** = primero<br /><br /> **2** = segundo<br /><br /> **4** = tercero<br /><br /> **8** = cuarto<br /><br /> **16** = último|  
|**freq_recurrence_**<br /><br /> **factor de**|**int**|Número de semanas o meses entre las ejecuciones programadas de un trabajo. **freq_recurrence_factor** solo se utiliza si **freq_type** es **8**, **16**, o **32**. Si esta columna contiene **0**, **freq_recurrence_factor** no se utiliza.|  
|**active_start_date**|**int**|Fecha en la que puede comenzar la ejecución de un trabajo. La fecha tiene el formato AAAAMMDD. NULL indica la fecha actual.|  
|**active_end_date**|**int**|Fecha en la que puede detenerse la ejecución de un trabajo. La fecha tiene el formato AAAAMMDD.|  
|**active_start_time**|**int**|Hora de un día entre **active_start_date** y **active_end_date** ese trabajo empieza a ejecutarse. La hora tiene el formato HHMMSS y se utiliza el reloj de 24 horas.|  
|**active_end_time**|**int**|Hora de un día entre **active_start_date** y **active_end_date** ese trabajo deja de ejecutarse. La hora tiene el formato HHMMSS y se utiliza el reloj de 24 horas.|  
|**Date_Created**|**datetime**|Fecha y hora en que se creó la programación.|  
|**DATE_MODIFIED**|**datetime**|Fecha y hora en que se modificó la programación por última vez.|  
|**version_number**|**int**|Número de versión actual de la programación. Por ejemplo, si una programación se ha modificado 10 veces, la **version_number** es 10.|  
  
|Valor de freq_type|Efecto en freq_interval|  
|-------------------------|------------------------------|  
|**1** (una vez)|**freq_interval** no se utiliza (**0**)|  
|**4** (diariamente)|Cada **freq_interval** días|  
|**8** (semanalmente)|**freq_interval** es uno o más de las siguientes acciones:<br /><br /> **1** = el domingo<br /><br /> **2** = el lunes<br /><br /> **4** = el martes<br /><br /> **8** = el miércoles<br /><br /> **16** = el jueves<br /><br /> **32** = el viernes<br /><br /> **64** = el sábado|  
|**16** (mensualmente)|En el **freq_interval** día del mes|  
|**32** (mensualmente, relativo)|**freq_interval** es uno de los siguientes:<br /><br /> **1** = el domingo<br /><br /> **2** = el lunes<br /><br /> **3** = el martes<br /><br /> **4** = el miércoles<br /><br /> **5** = el jueves<br /><br /> **6** = el viernes<br /><br /> **7** = el sábado<br /><br /> **8** = día<br /><br /> **9** = día de la semana<br /><br /> **10** = día del fin de semana|  
|**64** (se inicia cuando se inicia el servicio Agente SQL Server)|**freq_interval** no se utiliza (**0**)|  
|**128** (se ejecuta cuando el equipo está inactivo)|**freq_interval** no se utiliza (**0**)|  
  
## <a name="see-also"></a>Vea también  
 [dbo.sysjobschedules &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
