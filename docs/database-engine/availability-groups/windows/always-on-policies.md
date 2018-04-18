---
title: Directivas de los grupos de disponibilidad Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26bf8f71-c2b8-45ef-b3a3-372b96c9e6e3
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: b3fbed9846f0b3c938279902fbd19483d442d392
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="always-on-availability-groups-policies"></a>Directivas de grupos de disponibilidad Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El panel de Always On utiliza las directivas del sistema de grupos de disponibilidad Always On para proporcionar información sobre el mantenimiento del grupo de disponibilidad para el usuario. Son muy útiles para solucionar los problemas de funcionamiento iniciales de un grupo de disponibilidad. Estas directivas se pueden ampliar y usar para personalizar el panel Always On o se pueden ejecutar al instante para notificar la información de mantenimiento deseada.  
  
 Hay 14 directivas del sistema para los grupos de disponibilidad. Para obtener información sobre cada directiva, consulte [Directivas de Always On para problemas operativos - Grupos de disponibilidad Always On (SQL Server)](always-on-policies-for-operational-issues-always-on-availability.md).  
  
## <a name="view-or-evaluate-availability-groups-system-policies"></a>Ver o evaluar las directivas de sistema de los grupos de disponibilidad  
 Para ver o ejecutar las directivas de sistema de los grupos de disponibilidad en SQL Server Management Studio (SSMS), haga lo siguiente:  
  
1.  En el **Explorador de objetos**, expanda **Administración**, **Administración de directivas**, **Directivas** y después **Directivas del sistema**.  
  
2.  Haga clic en una de las directivas y haga clic en **Evaluar**. Si quiere evaluar la directiva que ha seleccionado, ya ha terminado. Puede hacer clic en **Vista**, en el cuadro **Detalles del destino**, para ver los detalles de los resultados de evaluación.  
  
3.  Para consultar todas las directivas de sistema delos grupos de disponibilidad, en el panel **Seleccionar una página**, haga clic en **Selección de directiva**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [The Always On health model, part 2: Extending the health model](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx) (Modelo de mantenimiento de Always On, parte 2: extender el modelo de mantenimiento)  
  
  