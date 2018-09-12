---
title: Monitor de actividad de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.ACTIVITYMON.F1
- sql12.ag.jobactivitymonitor.alljobs.f1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d185f8c5e74359ac8f8dfa0a2673da603e611414
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814341"
---
# <a name="job-activity-monitor"></a>Monitor de actividad de trabajo
  Utilice esta página para ver la actividad actual de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Haga clic en **Filtro** para limitar el número de trabajos mostrados. La cuadrícula **Actividad de trabajo del agente** es de solo lectura. Haga clic en los encabezados de columna para ordenar la cuadrícula. Si desea modificar un trabajo, haga doble clic en el trabajo para abrir el cuadro de diálogo **Propiedades del trabajo** . Haga clic con el botón secundario en un trabajo de la cuadrícula para que comiencen a ejecutarse todos los pasos del trabajo, para iniciar un paso del trabajo determinado, deshabilitar o habilitar el trabajo, actualizarlo, eliminarlo, ver su historial o ver sus propiedades. Haga clic en **Actualizar** para actualizar la cuadrícula con información actual.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Nombre del trabajo.  
  
 **Enabled**  
 Indica si el trabajo está habilitado (**sí**) o no (**no**).  
  
 **Estado** <sup>1</sup>  
 Estado actual del trabajo.  
  
 **Resultado de la última ejecución**  
 Estado del trabajo cuando se ejecutó por última vez.  
  
 **Última ejecución**  
 Fecha y hora en que se ejecutó el trabajo por última vez con la fecha y hora locales del servidor.  
  
 **A continuación ejecute** <sup>1</sup>  
 Fecha y hora en que se ha programado la próxima ejecución del trabajo con la fecha y hora locales del servidor.  
  
 **Categoría**  
 Categoría asignada al trabajo.  
  
 **Ejecutable**  
 **Sí** si el trabajo puede ejecutarse; **No** si el trabajo no puede ejecutarse. No puede ejecutarse un trabajo que no disponga de pasos o de un servidor de destino.  
  
 **Programado**  
 **Sí** si se ha asignado el trabajo a una programación de trabajo; **No** si el trabajo no tiene ninguna programación.  
  
 <sup>1</sup>sólo los miembros de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fijo sysadmin rol de servidor y los administradores de servidor, puede ver el grupo de valores en esta columna. Los miembros del rol SQLAgentOperatorRole no pueden ver los valores en esta columna.  
  
#### <a name="to-open-the-job-activity-monitor"></a>Para abrir el Monitor de actividad de trabajo  
  
-   En el **Explorador de objetos**, expanda su servidor, expanda **Agente SQL Server**, haga clic con el botón derecho en **Monitor de actividad de trabajo**y, luego, haga clic en **Ver actividad de trabajo**.  
  
## <a name="see-also"></a>Vea también  
 [Actividad de trabajos de monitor](monitor-job-activity.md)  
  
  
