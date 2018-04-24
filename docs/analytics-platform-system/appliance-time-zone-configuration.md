---
title: 'Configurar la zona horaria: Analytics Platform System | Documentos de Microsoft'
description: La página de zona horaria permite establecer la zona horaria para todos los nodos en el dispositivo Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6a17ef4e77f9703a285f1e232077582e4441f293
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configuración de zona horaria del dispositivo - Analytics Platform System
El **zona horaria** página le permite establecer la zona horaria para todos los nodos en el dispositivo Analytics Platform System (APS).  
  
## <a name="to-set-the-time-zone"></a>Para establecer la zona horaria  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  Detener los servicios del dispositivo mediante el **estado de los servicios** en el Administrador de configuración de página. Vea [estado de los servicios PDW &#40;Analytics Platform System&#41; ](pdw-services-status.md) para obtener instrucciones.  
  
3.  En el panel izquierdo del Administrador de configuración, haga clic en **zona horaria**. Seleccione la zona horaria deseada de la **zona horaria** menú desplegable. Dependiendo de su ubicación, también puede activar la casilla junto a **ajustar el reloj automáticamente al horario de verano**.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
5.  Reiniciar los servicios del dispositivo mediante el **estado de los servicios** en el Administrador de configuración de página. Si también va a cambiar los privilegios, puede hacerlo antes de reiniciar el dispositivo.  
  
![Hora del dispositivo DWConfig](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40;sistema de la plataforma de análisis&#41;](launch-the-configuration-manager.md)  
  
