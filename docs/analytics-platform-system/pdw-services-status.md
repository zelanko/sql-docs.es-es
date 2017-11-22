---
title: Estado de los servicios PDW (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fc9bee2-c372-4c4a-956c-fb54215d8918
caps.latest.revision: "14"
ms.openlocfilehash: 252a18f85d86129aa9f1916a224048b7e4b03f30
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="pdw-services-status"></a>Estado de los servicios PDW
El almacenamiento de datos paralelos **estado de los servicios** página en Microsoft Analytics Platform System Configuration Manager muestra el estado actual de todos los servicios de SQL Server PDW y proporciona la capacidad para detener e iniciar los servicios PDW. Este es el único método admitido para iniciar y detener los servicios PDW. Tenga en cuenta que los componentes individuales o los servicios no puede iniciarse por separado.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar o detener los servicios del dispositivo  
  
1.  Para iniciar los servicios del dispositivo, haga clic en **dispositivo iniciar**.  
  
2.  Para detener los servicios del dispositivo, haga clic en **detener dispositivo**.  
  
No es necesario hacer clic en **aplicar** al iniciar y detener los servicios del dispositivo mediante el uso de **dispositivo iniciar** y **detener dispositivo**.  
  
![Servicios PDW del dispositivo DWConfig](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Detención de la región de PDW, también detiene al agente PDW (sqldwagent) en los nodos de la HDInsight región. La HDInsight región todavía es funcional, sin embargo, la supervisión de estado no estará disponible. (El agente PDW requiere el nodo de control PDW para informar de supervisión de estado).  
  
## <a name="see-also"></a>Vea también  
[Energía de la aplicación de puntos de acceso o desactivar &#40; Sistema de la plataforma de análisis &#41;](power-the-aps-appliance-on-or-off.md)  
  
