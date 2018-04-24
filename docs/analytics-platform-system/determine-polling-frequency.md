---
title: 'Determinar la frecuencia de sondeo: Analytics Platform System | Documentos de Microsoft'
description: En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de dispositivo de sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e8e2a1ccf469e6c587870c0d5921014d797f87d1
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="determine-polling-frequency"></a>Determinar la frecuencia de sondeo
En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de dispositivo de sistema de la plataforma de análisis.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar la frecuencia de sondeo  
Puesto que PDW no admite actualmente notificaciones de automático cuando se produzcan alertas, la solución de supervisión debe sondear continuamente la DLL de la aplicación.  Internamente, PDW sondea los componentes a intervalos diferentes:  
  
-   Clúster: 60 segundos  
  
-   Latido: 60 segundos  
  
-   Todos los demás componentes – cinco minutos  
  
-   Contadores de rendimiento: tres segundos  
  
Es un intervalo común a sondear en busca de alertas, que también se usa System Center, **cada 15 minutos**.  Naturalmente, podría consultar mayor o menor frecuencia, pero no se recomienda para sondear inferior a cada seis horas.  
  
Con más frecuencia de sondeo es aceptable, pero con demasiada frecuencia de sondeo puede desordenar la [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV.  Con demasiada frecuencia de sondeo puede ser difícil para que los usuarios diagnosticar el rendimiento de las consultas problemas cuando sus rápidamente pone fuera de la vista.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión de dispositivo &#40;sistema de la plataforma de análisis&#41;](appliance-monitoring.md)  
  
