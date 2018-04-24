---
title: PDW de servicios de estado - Analytics Platform System | Documentos de Microsoft
description: Almacenamiento de datos paralelo (PDW) estado de los servicios de sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e2252bb821f9522515f1625b0fc118323cb50d1f
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Estado de los servicios de almacenamiento de datos paralelo de sistema de la plataforma de análisis
El almacenamiento de datos paralelos **estado de los servicios** página en Microsoft Analytics Platform System Configuration Manager muestra el estado actual de todos los servicios de SQL Server PDW y proporciona la capacidad para detener e iniciar los servicios PDW. Este es el único método admitido para iniciar y detener los servicios PDW. Tenga en cuenta que los componentes individuales o los servicios no puede iniciarse por separado.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar o detener los servicios del dispositivo  
  
1.  Para iniciar los servicios del dispositivo, haga clic en **dispositivo iniciar**.  
  
2.  Para detener los servicios del dispositivo, haga clic en **detener dispositivo**.  
  
No es necesario hacer clic en **aplicar** al iniciar y detener los servicios del dispositivo mediante el uso de **dispositivo iniciar** y **detener dispositivo**.  
  
![Servicios PDW del dispositivo DWConfig](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Detención de la región de PDW, también detiene al agente PDW (sqldwagent) en los nodos de la HDInsight región. La HDInsight región todavía es funcional, sin embargo, la supervisión de estado no estará disponible. (El agente PDW requiere el nodo de control PDW para informar de supervisión de estado).  
  
## <a name="see-also"></a>Vea también  
[Encender el dispositivo de APS o apagar &#40;sistema de la plataforma de análisis&#41;](power-the-aps-appliance-on-or-off.md)  
  
