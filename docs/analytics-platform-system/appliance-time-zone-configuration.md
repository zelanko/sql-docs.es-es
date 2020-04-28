---
title: Configurar zona horaria
description: La página zona horaria le permite establecer la zona horaria para todos los nodos del dispositivo de Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401390"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configuración de zona horaria del dispositivo: Analytics Platform System
La página **zona horaria** le permite establecer la zona horaria para todos los nodos del dispositivo de Analytics Platform System (APS).  
  
## <a name="to-set-the-time-zone"></a>Para establecer la zona horaria  
  
1.  Inicie el Configuration Manager. Para obtener más información, consulte [Inicio del&#41;de &#40;de Configuration Manager de la plataforma de análisis ](launch-the-configuration-manager.md).  
  
2.  Detenga los servicios del dispositivo mediante la página estado de los **servicios** en el Configuration Manager. Consulte el estado de los [servicios de PDW &#40;Analytics Platform System&#41;](pdw-services-status.md) para obtener instrucciones.  
  
3.  En el panel izquierdo del Configuration Manager, haga clic en **zona horaria**. Seleccione la zona horaria deseada en el menú desplegable **zona horaria** . En función de su ubicación, también puede activar la casilla situada junto a **ajustar automáticamente el reloj al horario de verano**.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
5.  Reinicie los servicios del dispositivo mediante la página estado de los **servicios** en el Configuration Manager. Si también tiene previsto cambiar los privilegios, puede hacerlo antes de reiniciar el dispositivo.  
  
![Tiempo del dispositivo de DWConfig](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Consulte también  
[Inicie el sistema de Configuration Manager &#40;Analytics Platform&#41;](launch-the-configuration-manager.md)  
  
