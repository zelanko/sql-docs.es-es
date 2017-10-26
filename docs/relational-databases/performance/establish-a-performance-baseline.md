---
title: "Establecer una línea base del rendimiento | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6d1c546387df6352a1eb59b0c0310d86a630a342
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="establish-a-performance-baseline"></a>Establecer una línea base del rendimiento
  Para determinar si el sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciona de forma óptima, tome medidas del rendimiento a intervalos regulares, incluso cuando no existan problemas, para establecer una línea base del rendimiento del servidor. Compare cada conjunto de medidas nuevo con las medidas tomadas anteriormente.  
  
 Las áreas siguientes afectan al rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Recursos del sistema (hardware)  
  
-   Arquitectura de red  
  
-   Sistema operativo  
  
-   Aplicaciones de bases de datos  
  
-   Aplicaciones cliente  
  
 Como mínimo, utilice las medidas de línea base para determinar:  
  
-   Las horas con el máximo y el mínimo nivel de funcionamiento.  
  
-   Tiempos de respuesta de comandos de procesamiento por lotes o consultas de producción.  
  
-   Tiempos de finalización de operaciones de copias de seguridad y restauración de bases de datos  
  
 Cuando haya establecido la línea base para el rendimiento del servidor, compare las estadísticas de la línea base con el rendimiento actual del servidor. Unas cifras demasiado elevadas o demasiado reducidas con respecto a la línea base indican que hay que realizar una investigación más detallada. Pueden indicar áreas que hay que optimizar o volver a configurar. Por ejemplo, si aumenta el tiempo necesario para ejecutar un conjunto de consultas, examine las consultas para determinar si puede volver a escribirlas o si es necesario agregar estadísticas de columnas u otros índices.  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

