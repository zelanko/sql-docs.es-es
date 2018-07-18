---
title: PDW de servicios de estado - Analytics Platform System | Microsoft Docs
description: Estado de servicios de almacenamiento de datos paralelos (PDW) de Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6892bfcca05e0f85039dddee65a54b485a7ed433
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909895"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Estado de servicios de almacenamiento de datos paralelos de Analytics Platform System
El almacenamiento de datos paralelos **estado Services** página en Microsoft Analytics Platform System Configuration Manager muestra el estado actual de todos los servicios de PDW de SQL Server y proporciona la capacidad para detener e iniciar los servicios PDW. Este es el único método admitido para iniciar y detener los servicios PDW. Tenga en cuenta que los componentes individuales o servicios no puede iniciarse por separado.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar o detener los servicios del dispositivo  
  
1.  Para iniciar los servicios del dispositivo, haga clic en **dispositivo inicie**.  
  
2.  Para detener los servicios del dispositivo, haga clic en **detener dispositivo**.  
  
No es necesario hacer clic en **aplicar** al iniciar y detener los servicios del dispositivo mediante el uso de **dispositivo inicie** y **detener dispositivo**.  
  
![Servicios PDW del dispositivo DWConfig](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Detención de la región de PDW, también detiene al agente PDW (sqldwagent) en los nodos. El agente PDW requiere que el nodo de control PDW para notificar la supervisión de estado.  
  
## <a name="see-also"></a>Vea también  
[Activar o desactivar de energía del dispositivo APS &#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
