---
title: Actualización del Monitor de actividad de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14e4e42f4f756a7a63f4c0dfa17845c606233148
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059065"
---
# <a name="job-activity-monitor-refresh"></a>Actualizar el Monitor de actividad de trabajo
  Utilice el cuadro de diálogo **Actualizar configuración** para configurar la frecuencia con la que el Monitor de actividad de trabajo obtiene información nueva sobre la actividad del servidor. El Monitor de actividad debe ejecutar consultas en el servidor supervisado para obtener información sobre la cuadrícula Monitor de actividad de trabajo. Cuando el intervalo de actualización automática se establece en un valor inferior a 30 segundos, el tiempo usado para ejecutar estas consultas puede afectar al rendimiento del servidor.  
  
 Para abrir este cuadro de diálogo, haga clic en **Ver configuración de actualización**, en la sección **Estado** del Monitor de actividad de trabajo.  
  
## <a name="options"></a>Opciones  
 **Actualizar automáticamente cada**  
 Realiza comprobaciones para iniciar la actualización automática de la información del Monitor de actividad. Esta opción está desactivada de forma predeterminada.  
  
 **segundos**  
 Número de segundos entre los distintos intentos de actualización automática. El valor predeterminado es 60 segundos. Realiza actualizaciones cada 5 segundos cuando se establece en 5 o en un valor inferior.  
  
## <a name="see-also"></a>Vea también  
 [Actividad de trabajos de monitor](../../ssms/agent/monitor-job-activity.md)  
  
  
