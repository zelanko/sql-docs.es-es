---
title: Determinar la frecuencia de sondeo - Analytics Platform System | Microsoft Docs
description: En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de Analytics Platform System appliance.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6b838766e7a6d6bfb9a68bb832cd7a8feb3c9960
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696623"
---
# <a name="determine-polling-frequency"></a>Determinar la frecuencia de sondeo
En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de Analytics Platform System appliance.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar la frecuencia de sondeo  
Puesto que PDW no admite actualmente notificaciones proactivas cuando se produzcan alertas, la solución de supervisión debe sondear continuamente la aplicación DLL.  Internamente, PDW sondea los componentes en intervalos diferentes:  
  
-   Clúster: 60 segundos  
  
-   Latido: 60 segundos  
  
-   Todos los demás componentes – cinco minutos  
  
-   Contadores de rendimiento: tres segundos  
  
Es un intervalo comunes para sondear en busca de alertas, que también se usa System Center, **cada 15 minutos**.  Obviamente, puede consultar mayor o menor frecuencia, pero no se recomienda para sondear menos cada seis horas.  
  
Con más frecuencia de sondeo es aceptable, pero el sondeo demasiado frecuente puede provocar un desorden el [sys.dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV.  Sondeo demasiado frecuente puede hacer difícil para que los usuarios diagnosticar el rendimiento de las consultas problemas cuando sus rápidamente pone fuera de la vista.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión del dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
