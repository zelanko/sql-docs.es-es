---
title: Página Progreso (asistentes para grupos de disponibilidad AlwaysOn) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.addreplicawizard.progress.f1
- sql12.swb.newagwizard.progress.f1
- sql11.swb.failoverwizard.progress.f1
- sql11.swb.adddatabasewizard.progress.f1
- sql11.swb.addreplicawizard.progress.f1
- sql11.swb.newagwizard.progress.f1
- sql12.swb.adddatabasewizard.progress.f1
- sql12.swb.failoverwixard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 92a1adb3921b8daf0a2692ad840bf30af6561cf8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202563"
---
# <a name="progress-page-alwayson-availability-group-wizards"></a>Página Progreso (asistentes para grupos de disponibilidad AlwaysOn)
  Utilice este cuadro de diálogo para ver el progreso del asistente de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] que esté ejecutando en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. La barra de progreso indica el progreso relativo de los pasos que el asistente realiza.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Más detalles**  
 Haga clic en la flecha abajo para mostrar una cuadrícula de progreso que enumera los pasos completados, en orden, seguida de la operación en curso actual. La cuadrícula contiene las columnas siguientes:  
  
 **Nombre**  
 Muestra una frase que describe un paso concreto.  
  
 **Estado**  
 Indica el resultado de los pasos completados y el porcentaje de finalización del paso actual, del siguiente modo:  
  
|Resultado|Descripción|  
|------------|-----------------|  
|**Error**|Indica que la operación para este paso ha experimentado un error. Haga clic en el vínculo para mostrar un cuadro de diálogo de mensaje que describe el error.|  
|**En curso (** *porcentaje completado* **)**|Indica que la operación se está produciendo ahora y calcula el porcentaje completado de este paso.|  
|**Correcto**|Indica que la operación correspondiente a este paso se ha completado correctamente.|  
  
 **Menos detalles**  
 Haga clic para ocultar la cuadrícula de progreso.  
  
 **Cancelar**  
 Haga clic para omitir las operaciones restantes y salir del asistente.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una base de datos al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
-   [Usar el Asistente para grupo de disponibilidad de conmutación por error &#40;SQL Server Management Studio&#41;](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  