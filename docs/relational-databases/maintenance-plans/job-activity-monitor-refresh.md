---
title: Actualización del Monitor de actividad de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f6e370ce717190b6f7a14b6eaf354c7c5321a011
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68115766"
---
# <a name="job-activity-monitor-refresh"></a>Actualizar el Monitor de actividad de trabajo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice el cuadro de diálogo **Actualizar configuración** para configurar la frecuencia con la que el Monitor de actividad de trabajo obtiene información nueva sobre la actividad del servidor. El Monitor de actividad debe ejecutar consultas en el servidor supervisado para obtener información sobre la cuadrícula Monitor de actividad de trabajo. Cuando el intervalo de actualización automática se establece en un valor inferior a 30 segundos, el tiempo usado para ejecutar estas consultas puede afectar al rendimiento del servidor.  
  
 Para abrir este cuadro de diálogo, haga clic en **Ver configuración de actualización**, en la sección **Estado** del Monitor de actividad de trabajo.  
  
## <a name="options"></a>Opciones  
 **Actualizar automáticamente cada**  
 Realiza comprobaciones para iniciar la actualización automática de la información del Monitor de actividad. Esta opción está desactivada de forma predeterminada.  
  
 **segundos**  
 Número de segundos entre los distintos intentos de actualización automática. El valor predeterminado es 60 segundos. Realiza actualizaciones cada 5 segundos cuando se establece en 5 o en un valor inferior.  
  
## <a name="see-also"></a>Consulte también  
 [Actividad de trabajos de monitor](../../ssms/agent/monitor-job-activity.md)  
  
  
