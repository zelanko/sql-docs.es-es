---
title: Modificar un filtro (SQL Server Profiler) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2bc42acf774fb9f9b25147998a604e9afa7565eb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="modify-a-filter-sql-server-profiler"></a>Modificar un filtro (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Se agregan filtros a las plantillas de seguimiento, que contienen las definiciones de los seguimiento, para limitar el número de eventos que recopila un seguimiento. Esta limitación puede reducir las consecuencias sobre el rendimiento de las trazas. Si establece filtros para una plantilla de seguimiento y averigua que el seguimiento no recopila el tipo de información que necesita, puede modificar el filtro.  
  
### <a name="to-modify-a-filter"></a>Para modificar un filtro  
  
1.  En el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], abra la plantilla del filtro de seguimiento que desea modificar. En el menú **Archivo** , haga clic en **Plantillas**y, a continuación, elija **Editar plantilla**.  
  
2.  En la pestaña **General** del cuadro de diálogo **Propiedades de la plantilla de seguimiento** , seleccione una plantilla en la lista **Seleccionar nombre de plantilla** .  
  
3.  Haga clic en la pestaña **Selección de eventos** .  
  
     La pestaña **Selección de eventos** contiene un control de cuadrícula. El control de cuadrícula es una tabla que contiene todas las clases de eventos en las que se puede realizar un seguimiento. La tabla contiene una fila para cada clase de evento. Las clases de eventos pueden diferir ligeramente dependiendo del tipo y la versión del servidor al que esté conectado. Las clases de eventos se identifican en la columna **Events**de la cuadrícula y se agrupan por categorías de eventos. En las demás columnas se enumeran las columnas de datos que pueden devolverse para cada clase de evento.  
  
4.  Haga clic en **Filtros de columna**.  
  
5.  En el cuadro de diálogo **Editar filtro** , haga clic en el valor junto al operador de comparación que desea modificar y escriba el valor nuevo o elimine un valor. También puede agregar otros filtros.  
  
6.  Haga clic en **Aceptar** y guarde la plantilla.  
  
## <a name="see-also"></a>Ver también  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
