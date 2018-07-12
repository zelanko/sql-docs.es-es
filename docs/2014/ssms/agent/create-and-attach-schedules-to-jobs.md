---
title: Crear y adjuntar programaciones a trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server]
- scheduling jobs [SQL Server]
- jobs [SQL Server], scheduling
- CPU [SQL Server], idle conditions
- automatic job processing
- SQL Server Agent jobs, scheduling
- idle time [SQL Server]
ms.assetid: 079c2984-0052-4a37-a2b8-4ece56e6b6b5
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f85e651f67b6553f597fab920bde7cc05ca37167
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192875"
---
# <a name="create-and-attach-schedules-to-jobs"></a>Crear y adjuntar programaciones a trabajos
  La programación de trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste en definir las condiciones que provocan el inicio de la ejecución de los trabajos sin intervención del usuario. Puede programar que un trabajo se ejecute automáticamente creando una nueva programación para el trabajo, o adjuntando una programación existente al trabajo.  
  
 Hay dos maneras de crear una programación:  
  
-   Crear la programación mientras se está creando un trabajo.  
  
-   Crear la programación en el Explorador de objetos.  
  
 Una vez creada una programación, puede adjuntarla a varios trabajos, aun cuando la programación se haya creado para un trabajo concreto. También puede separar las programaciones de los trabajos.  
  
 Una programación puede basarse en tiempo o en un evento. Por ejemplo, puede programar un trabajo para que se ejecute en los momentos siguientes:  
  
-   Cuando se inicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Cuando el uso de la CPU del equipo se encuentre en un nivel que se haya definido como inactivo.  
  
-   Una vez, a una hora y una fecha específicas.  
  
-   Periódicamente.  
  
 Como alternativa a las programaciones de trabajo, también puede crear una alerta que responda a un evento ejecutando un trabajo.  
  
> [!NOTE]  
>  Solo se puede ejecutar una instancia del trabajo cada vez. Si intenta ejecutar un trabajo manualmente mientras se está ejecutando en el momento programado, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechazará la solicitud.  
  
 Para impedir que un trabajo programado se ejecute, debe realizar una de las siguientes acciones:  
  
-   Deshabilitar la programación.  
  
-   Deshabilitar el trabajo.  
  
-   Separar la programación del trabajo.  
  
-   Detener el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Eliminar la programación.  
  
 Aunque no esté habilitada la programación, se puede ejecutar el trabajo en respuesta a una alerta o cuando un usuario lo ejecute manualmente. Si no está habilitada una programación de trabajo, no estará habilitada para ningún trabajo que la utilice.  
  
 Las programaciones deshabilitadas se deben volver a habilitar de manera explícita. La modificación de una programación no la vuelve a habilitar automáticamente.  
  
## <a name="scheduling-start-dates"></a>Programar fechas de inicio  
 La fecha de inicio de una programación debe ser mayor o igual que 19900101.  
  
 Al adjuntar una programación a un trabajo, se debe revisar la fecha de inicio que usa la programación para ejecutar por primera vez el trabajo. La fecha de inicio depende del día y la hora en que se adjunte la programación al trabajo. Por ejemplo, si se crea una programación que se ejecuta cada dos lunes a las 8:00 a.m. Si se crea un trabajo a las 10:00 a.m. del lunes 3 de marzo de 2008, la fecha de inicio de la programación será lunes 17 de marzo de 2008. Si se crea otro trabajo el martes 4 de marzo de 2008, la fecha de inicio de la programación será lunes 10 de marzo de 2008.  
  
 Puede cambiar la fecha de inicio de la programación después de adjuntar la programación a un trabajo.  
  
## <a name="cpu-idle-schedules"></a>Programaciones de inactividad de CPU  
 Para maximizar los recursos de CPU, puede definir una condición de CPU inactiva para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente usa la configuración de la condición de CPU inactiva para determinar el momento más conveniente para ejecutar trabajos. Por ejemplo, puede programar la ejecución de un trabajo de generación de índices durante el tiempo de inactividad de CPU y en periodos de baja producción.  
  
 Antes de definir trabajos para que se ejecuten durante el tiempo de inactividad de CPU, determine la carga de la CPU durante el procesamiento normal. Para ello, utilice el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o el Monitor de rendimiento para supervisar el tráfico del servidor y obtener estadísticas. La información que obtenga puede utilizarla para establecer el porcentaje y la duración del tiempo de inactividad de CPU.  
  
 Defina la condición de CPU inactiva como un porcentaje por debajo del cual el uso de CPU debe permanecer durante un intervalo de tiempo especificado. A continuación, establezca la duración. Cuando el uso de CPU esté por debajo del porcentaje especificado para el tiempo determinado, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciará todos los trabajos que tengan una programación de tiempo de inactividad de CPU. Para obtener más información sobre el uso de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o el Monitor de rendimiento para supervisar el uso de CPU, consulte [supervisar el uso de CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe cómo crear una programación para un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Create a Schedule](create-a-schedule.md)|  
|Describe cómo programar un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Programar un trabajo](schedule-a-job.md)|  
|Explica cómo definir la condición de inactividad de la CPU para el servidor.|[Establecer la duración y el tiempo de inactividad de la CPU &#40;SQL Server Management Studio&#41;](set-cpu-idle-time-and-duration-sql-server-management-studio.md)|  
  
## <a name="see-also"></a>Vea también  
 [sp_help_jobschedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobschedule-transact-sql)   
 [dbo.sysjobschedules &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobschedules-transact-sql)  
  
  
