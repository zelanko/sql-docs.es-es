---
title: Configurar la zona horaria - Analytics Platform System | Microsoft Docs
description: La página de la zona horaria permite establecer la zona horaria para todos los nodos en el dispositivo de Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6a17ef4e77f9703a285f1e232077582e4441f293
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63276000"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configuración de zona horaria del dispositivo: Analytics Platform System
El **zona horaria** página permite establecer la zona horaria para todos los nodos en el dispositivo de Analytics Platform System (APS).  
  
## <a name="to-set-the-time-zone"></a>Para establecer la zona horaria  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  Detenga los servicios de dispositivo mediante el **estado Services** página del Administrador de configuración. Consulte [estado de servicios de PDW &#40;Analytics Platform System&#41; ](pdw-services-status.md) para obtener instrucciones.  
  
3.  En el panel izquierdo del Administrador de configuración, haga clic en **zona horaria**. Seleccione la zona horaria deseada desde la **zona horaria** menú desplegable. Dependiendo de su ubicación, también puede activar la casilla junto a **ajustar el reloj automáticamente al horario de verano**.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
5.  Reiniciar los servicios de dispositivo mediante el **estado Services** página del Administrador de configuración. Si también va a cambiar los privilegios, puede hacerlo antes de reiniciar el dispositivo.  
  
![Hora del dispositivo DWConfig](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
