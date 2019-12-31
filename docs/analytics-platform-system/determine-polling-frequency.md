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
ms.openlocfilehash: 005fe3d14a7314f7339157064b248a81044a1dfb
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401213"
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
  
El sondeo más frecuente es aceptable, pero el sondeo con demasiada frecuencia puede abarrotar la DMV [Sys. dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) .  El sondeo con demasiada frecuencia puede dificultar a los usuarios el diagnóstico de los problemas de rendimiento de las consultas cuando se despliegan rápidamente.  
  
## <a name="see-also"></a>Véase también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión de dispositivos &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
