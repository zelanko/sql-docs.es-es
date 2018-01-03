---
title: "Configuración de zona horaria del dispositivo (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cea9eeb9-fe05-4e65-b229-539de02ab20a
caps.latest.revision: "18"
ms.openlocfilehash: 0dc20594fa45375fe07b4ec374da9c752d3cc8b0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="appliance-time-zone-configuration"></a>Configuración de zona horaria del dispositivo
El **zona horaria** página le permite establecer la zona horaria para todos los nodos en el dispositivo PDW de SQL Server.  
  
## <a name="to-set-the-time-zone"></a>Para establecer la zona horaria  
  
1.  Inicie el Administrador de configuración. Para obtener más información, vea [iniciar el Administrador de configuración &#40; Sistema de la plataforma de análisis &#41; ](launch-the-configuration-manager.md).  
  
2.  Detener los servicios del dispositivo mediante el **estado de los servicios** en el Administrador de configuración de página. Vea [PDW de servicios de estado &#40; Sistema de la plataforma de análisis &#41; ](pdw-services-status.md) para obtener instrucciones.  
  
3.  En el panel izquierdo del Administrador de configuración, haga clic en **zona horaria**. Seleccione la zona horaria deseada de la **zona horaria** menú desplegable. Dependiendo de su ubicación, también puede activar la casilla junto a **ajustar el reloj automáticamente al horario de verano**.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
5.  Reiniciar los servicios del dispositivo mediante el **estado de los servicios** en el Administrador de configuración de página. Si también va a cambiar los privilegios, puede hacerlo antes de reiniciar el dispositivo.  
  
![Hora del dispositivo DWConfig](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40; Sistema de la plataforma de análisis &#41;](launch-the-configuration-manager.md)  
  
