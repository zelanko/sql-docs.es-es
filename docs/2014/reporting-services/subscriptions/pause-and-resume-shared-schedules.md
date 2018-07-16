---
title: Pausar y reanudar las programaciones compartidas| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services], resuming
- resuming schedules
- continuing schedules
- schedules [Reporting Services], resuming
- schedules [Reporting Services], pausing
ms.assetid: e416be75-5234-4aa6-a3de-77f60f25169a
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f83e1a89611e4d40e1d987e666d14b61f31f1e22
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255567"
---
# <a name="pause-and-resume-shared-schedules"></a>Pausar y reanudar las programaciones compartidas
  Existe la posibilidad de pausar y reanudar las programaciones compartidas en uso. Pausar una programación compartida es un modo de congelar temporalmente una programación que se emplea para desencadenar el procesamiento de los informes y las suscripciones. Solo es posible pausar y reanudar las programaciones compartidas. Las programaciones específicas del informe no admiten la operación de pausa.  
  
 Los procesos de los informes en curso no pueden pausarse ni reanudarse. Solo se pueden pausar y reanudar las programaciones de la cola de programación del Agente SQL Server. Los trabajos en curso quedan fuera del alcance del motor de programación. Para obtener más información, consulte [administrar un proceso en ejecución](manage-a-running-process.md)  
  
 Mientras una programación compartida está pausada, cualquier operación que hubiera tenido lugar puede detenerse. Una vez reanudada la programación compartida, el procesamiento de la suscripción y del informe se produce durante la siguiente programación (según la hora local del servidor). El servidor de informes en modo nativo o las aplicaciones de servicio de SharePoint no recuperan las operaciones programadas que se habrían realizado si la programación no se hubiera pausado.  
  
 En este tema:  
  
-   [Pausar y reanudar las programaciones compartidas (modo nativo)](#bkmk_native)  
  
-   [Pausar y reanudar las programaciones compartidas (modo de SharePoint)](#bkmk_sharepoint)  
  
##  <a name="bkmk_native"></a> Pausar y reanudar las programaciones compartidas (modo nativo)  
 Use la página Programaciones del Administrador de informes para pausar y reanudar una programación compartida. No puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ya que no proporciona las opciones necesarias para pausar y reanudar las programaciones. Para obtener más información, consulte [crear, modificar y eliminar programaciones](create-modify-and-delete-schedules.md).  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>Para pausar o reanudar una programación compartida  
  
1.  En el Administrador de informes, haga clic en **Configuración del sitio**.  
  
2.  Haga clic en **Programaciones**.  
  
3.  Seleccione la programación y haga clic en **Pausar** o **Reanudar** en la cinta de opciones. Si una programación está pausada actualmente, la columna **Estado** contendrá **En pausa**.  
  
##  <a name="bkmk_sharepoint"></a> Pausar y reanudar las programaciones compartidas (modo de SharePoint)  
 Para pausar y reanudar una programación compartida, use la página Configuración del sitio o PowerShell. Las programaciones se administran por sitio de SharePoint.  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>Para pausar o reanudar una programación compartida  
  
1.  Haga clic en **Acciones del sitio**.  
  
2.  Haga clic en **Configuración del sitio**.  
  
3.  En la sección Reporting Services, haga clic en **Administrar programaciones compartidas**.  
  
4.  Seleccione la programación y haga clic en **Pausar programaciones seleccionadas** o **Ejecutar programaciones seleccionadas**. Si una programación está pausada actualmente, la columna **Estado** contendrá **En pausa**.  
  
## <a name="see-also"></a>Vea también  
 [Programaciones](schedules.md)   
 [Crear, modificar y eliminar programaciones](create-modify-and-delete-schedules.md)   
 [Cambiar las zonas horarias y la configuración del reloj en un servidor de informes](change-time-zones-and-clock-settings-on-a-report-server.md)   
 [Administración de un proceso en ejecución](manage-a-running-process.md)  
  
  
