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
ms.openlocfilehash: eec9e3e211c68b7f56fe6829a70064317b96e646
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519573"
---
# <a name="determine-polling-frequency"></a>Determinar la frecuencia de sondeo
En este artículo se explica cómo determinar la frecuencia de sondeo para las alertas de Analytics Platform System appliance.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar la frecuencia de sondeo  
Puesto que PDW no admite actualmente notificaciones proactivas cuando se produzcan alertas, la solución de supervisión debe sondear continuamente la aplicación DLL.  Internamente, PDW sondea los componentes en intervalos diferentes:  
  
-   Clúster - 60 segundos  
  
-   Latido - 60 segundos  
  
-   Todos los demás componentes - cinco minutos  
  
-   Contadores de rendimiento - tres segundos  
  
Es un intervalo comunes para sondear en busca de alertas, que también se usa System Center, **cada 15 minutos**.  Obviamente, puede consultar mayor o menor frecuencia, pero no se recomienda para sondear menos cada seis horas.  
  
Con más frecuencia de sondeo es aceptable, pero el sondeo demasiado frecuente puede provocar un desorden el [sys.dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV.  Sondeo demasiado frecuente puede hacer difícil para que los usuarios diagnosticar el rendimiento de las consultas problemas cuando sus rápidamente pone fuera de la vista.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Supervisión del dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
