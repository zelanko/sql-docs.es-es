---
title: Determinar la frecuencia de sondeo (Analytics Platform System)
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
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: "7"
ms.openlocfilehash: fb32abc38a90cd7450dc310a9f73eb7a5d72b5fb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="determine-polling-frequency"></a>Determinar la frecuencia de sondeo
Este tema explica cómo determinar la frecuencia de sondeo para las alertas de dispositivo PDW de SQL Server.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar la frecuencia de sondeo  
Puesto que PDW no admite actualmente notificaciones de automático cuando se produzcan alertas, la solución de supervisión debe sondear continuamente la DLL de la aplicación.  Internamente, PDW sondea los componentes a intervalos diferentes:  
  
-   Clúster: 60 segundos  
  
-   Latido: 60 segundos  
  
-   Todos los demás componentes: 5 minutos  
  
-   Contadores de rendimiento: 3 segundos  
  
Es un intervalo común a sondear en busca de alertas, que también se usa System Center, **cada 15 minutos**.  Naturalmente, podría consultar mayor o menor frecuencia, pero no se recomienda para sondear inferior a cada 6 horas.  
  
Con más frecuencia de sondeo es aceptable, pero con demasiada frecuencia de sondeo puede desordenar la [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV.  Esto puede que sea difícil para los usuarios diagnosticar problemas de rendimiento de consultas si hay consultas más rápidamente pone fuera de la vista.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-monitoring.md)  
  
