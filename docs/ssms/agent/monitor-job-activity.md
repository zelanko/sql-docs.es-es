---
title: Supervisar la actividad de trabajos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, monitoring
- jobs [SQL Server Agent], monitoring
- monitoring [SQL Server], jobs
- activity monitoring [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- SQL Server Agent Job Activity Monitor
- SQL Server Agent jobs, monitoring
- performance [SQL Server], jobs
- current activity
ms.assetid: 71cb432b-631d-4b8b-9965-e731b3d8266d
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 762fd21319860bfe98fcbeeec5b777b62f54c533
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="monitor-job-activity"></a>Actividad de trabajos de monitor
Puede supervisar la actividad actual de todos los trabajos definidos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] mediante el Monitor de actividad de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="sql-server-agent-sessions"></a>Sesiones del Agente SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] El Agente crea una sesión cada vez que se inicia el servicio. Al crear una sesión, la tabla **sysjobactivity** de la base de datos **msdb** se rellena con todos los trabajos definidos existentes. Esta tabla mantiene la última actividad para los trabajos cuando se reinicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Cada sesión registra la actividad de trabajo normal del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] desde el inicio del trabajo hasta que termina. La información acerca de estas sesiones se almacena en la tabla **syssessions** de la base de datos **msdb** .  
  
## <a name="job-activity-monitor"></a>Monitor de actividad de trabajo  
El Monitor de actividad de trabajo permite ver la tabla **sysjobactivity** mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. Puede ver todos los trabajos del servidor, o bien puede definir filtros para limitar el número de trabajos mostrados. También puede ordenar la información sobre los trabajos haciendo clic en un encabezado de columna de la cuadrícula **Actividad de trabajo del agente** . Por ejemplo, al seleccionar el encabezado de columna **Última ejecución** , puede ver los trabajos en el orden en que se ejecutaron por última vez. Al volver a hacer clic en el encabezado de columna, el orden de los trabajos cambia entre ascendente y descendente basándose en la fecha en que se ejecutaron por última vez.  
  
El Monitor de actividad de trabajo le permite realizar las siguientes tareas:  
  
-   Iniciar y detener trabajos.  
  
-   Ver las propiedades del trabajo.  
  
-   Ver el historial de un determinado trabajo.  
  
-   Actualizar la información de la cuadrícula **Actividad de trabajo del agente** manualmente o establecer un intervalo de actualización automático haciendo clic en **Ver configuración de actualización**.  
  
Utilice el Monitor de actividad de trabajo cuando desee localizar los trabajos que están programados para su ejecución, el último resultado de los trabajos que se han ejecutado durante la sesión actual y localizar los trabajos que se están ejecutando actualmente o que están inactivos. Si el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tiene un error inesperado, puede determinar los trabajos que se estaban ejecutando buscando en la sesión anterior del Monitor de actividad de trabajo.  
  
Para abrir el Monitor de actividad de trabajo, expanda **Agente SQL Server** en el Explorador de objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] , haga clic con el botón derecho en **Monitor de actividad de trabajo**y haga clic en **Ver actividad de trabajo**.  
  
También puede ver la actividad de trabajo de la sesión actual mediante el procedimiento almacenado **sp_help_jobactivity**.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|||  
|-|-|  
|**Description**|**Tema**|  
|Describe cómo ver el estado de tiempo de ejecución de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .|[Ver actividad de trabajo](../../ssms/agent/view-job-activity.md)|  
  
## <a name="see-also"></a>Vea también  
[Ver actividad de trabajo](../../ssms/agent/view-job-activity.md)  
[sysjobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/fd17cac9-5d1f-4b44-b2dc-ee9346d8bf1e)  
[syssessions (Transact-SQL)](http://msdn.microsoft.com/en-us/187819b6-c7f4-4a26-b74c-0a89e96695cf)  
[sp_help_jobactivity (Transact-SQL)](http://msdn.microsoft.com/en-us/d344864f-b4d3-46b1-8933-b81dec71f511)  
  

