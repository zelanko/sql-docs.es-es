---
title: Determinar la frecuencia de sondeo
description: En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de la aplicación Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafd18a7701ed5de5018a3e8dc23bc8d5d9640fa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767044"
---
# <a name="determine-polling-frequency"></a>Determinar la frecuencia de sondeo
En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de la aplicación Analytics Platform System.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar la frecuencia de sondeo  
Como PDW no admite actualmente notificaciones proactivas cuando se producen alertas, la solución de supervisión debe sondear continuamente los archivos dll de la aplicación.  Internamente, PDW sondea los componentes en diferentes intervalos:  
  
-   Clúster: 60 segundos  
  
-   Latido: 60 segundos  
  
-   Todos los demás componentes: cinco minutos  
  
-   Contadores de rendimiento: tres segundos  
  
Un intervalo común para sondear las alertas, que también usa System Center, es **cada 15 minutos**.  Obviamente, podría consultar más o menos con frecuencia, pero no se recomienda realizar un sondeo inferior a cada seis horas.  
  
El sondeo más frecuente es aceptable, pero el sondeo con demasiada frecuencia puede abarrotar la DMV [Sys. dm_pdw_nodes_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md?view=sql-server-ver15) .  El sondeo con demasiada frecuencia puede dificultar a los usuarios el diagnóstico de los problemas de rendimiento de las consultas cuando se despliegan rápidamente.  
  
## <a name="see-also"></a>Consulte también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión de dispositivos &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
