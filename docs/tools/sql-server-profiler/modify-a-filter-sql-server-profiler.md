---
title: Modificar un filtro (SQL Server Profiler) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 741d1558f4d3efae9cf0d4742ee0fcce6d15d6c2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="modify-a-filter-sql-server-profiler"></a>Modificar un filtro (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Agregar filtros a las plantillas de seguimiento, que contienen las definiciones de seguimiento, para limitar el número de eventos que se recopilan a través de un seguimiento. Esta limitación puede reducir las consecuencias sobre el rendimiento de las trazas. Si establece filtros para una plantilla de seguimiento y averigua que el seguimiento no recopila el tipo de información que necesita, puede modificar el filtro.  
  
### <a name="to-modify-a-filter"></a>Para modificar un filtro  
  
1.  En el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], abra la plantilla del filtro de seguimiento que desea modificar. En el menú **Archivo** , haga clic en **Plantillas**y, a continuación, elija **Editar plantilla**.  
  
2.  En la pestaña **General** del cuadro de diálogo **Propiedades de la plantilla de seguimiento** , seleccione una plantilla en la lista **Seleccionar nombre de plantilla** .  
  
3.  Haga clic en la pestaña **Selección de eventos** .  
  
     La pestaña **Selección de eventos** contiene un control de cuadrícula. El control de cuadrícula es una tabla que contiene todas las clases de eventos en las que se puede realizar un seguimiento. La tabla contiene una fila para cada clase de evento. Las clases de eventos pueden diferir ligeramente dependiendo del tipo y la versión del servidor al que esté conectado. Las clases de eventos se identifican en la columna **Events**de la cuadrícula y se agrupan por categorías de eventos. En las demás columnas se enumeran las columnas de datos que pueden devolverse para cada clase de evento.  
  
4.  Haga clic en **Filtros de columna**.  
  
5.  En el cuadro de diálogo **Editar filtro** , haga clic en el valor junto al operador de comparación que desea modificar y escriba el valor nuevo o elimine un valor. También puede agregar otros filtros.  
  
6.  Haga clic en **Aceptar** y guarde la plantilla.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
