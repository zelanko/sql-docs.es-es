---
title: Estado de los servicios de PDW
description: Estado de los servicios de almacenamiento de datos paralelos (PDW) de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400854"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Estado de los servicios de almacenamiento de datos paralelos de Analytics Platform System
La página estado de los **servicios** de almacenamiento de datos paralelos del Microsoft Analytics Platform System Configuration Manager muestra el estado actual de todos los servicios de PDW de SQL Server y permite detener e iniciar los servicios de PDW. Este es el único método admitido para iniciar y detener los servicios de PDW. Tenga en cuenta que los componentes o servicios individuales no se pueden iniciar de forma independiente.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar o detener los servicios del dispositivo  
  
1.  Para iniciar los servicios del dispositivo, haga clic en **iniciar dispositivo**.  
  
2.  Para detener los servicios del dispositivo, haga clic en **detener dispositivo**.  
  
No es necesario hacer clic en **aplicar** al iniciar y detener los servicios del dispositivo mediante **iniciar dispositivo** y **detener dispositivo**.  
  
![Servicios PDW del dispositivo DWConfig](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Detener la región PDW también detiene el agente PDW (sqldwagent) en los nodos. El agente de PDW requiere que el nodo de control de PDW informe de la supervisión de estado.  
  
## <a name="see-also"></a>Consulte también  
[Encienda o desactive el dispositivo APS &#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
