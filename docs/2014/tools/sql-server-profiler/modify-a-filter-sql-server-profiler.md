---
title: Modificar un filtro (SQL Server Profiler) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], modifying
- modifying filters, modifying
- filters [SQL Server], traces
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cf53cb678e4069a6efe02719c3e03b47489b9e57
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106001"
---
# <a name="modify-a-filter-sql-server-profiler"></a>Modificar un filtro (SQL Server Profiler)
  Se agregan filtros a las plantillas de seguimiento, que contienen las definiciones de los seguimiento, para limitar el número de eventos que recopila un seguimiento. Esta limitación puede reducir las consecuencias sobre el rendimiento de las trazas. Si establece filtros para una plantilla de seguimiento y averigua que el seguimiento no recopila el tipo de información que necesita, puede modificar el filtro.  
  
### <a name="to-modify-a-filter"></a>Para modificar un filtro  
  
1.  En el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], abra la plantilla del filtro de seguimiento que desea modificar. En el menú **Archivo** , haga clic en **Plantillas**y, a continuación, elija **Editar plantilla**.  
  
2.  En la pestaña **General** del cuadro de diálogo **Propiedades de la plantilla de seguimiento** , seleccione una plantilla en la lista **Seleccionar nombre de plantilla** .  
  
3.  Haga clic en la pestaña **Selección de eventos** .  
  
     La pestaña **Selección de eventos** contiene un control de cuadrícula. El control de cuadrícula es una tabla que contiene todas las clases de eventos en las que se puede realizar un seguimiento. La tabla contiene una fila para cada clase de evento. Las clases de eventos pueden diferir ligeramente dependiendo del tipo y la versión del servidor al que esté conectado. Las clases de eventos se identifican en la columna **Events**de la cuadrícula y se agrupan por categorías de eventos. En las demás columnas se enumeran las columnas de datos que pueden devolverse para cada clase de evento.  
  
4.  Haga clic en **Filtros de columna**.  
  
5.  En el cuadro de diálogo **Editar filtro** , haga clic en el valor junto al operador de comparación que desea modificar y escriba el valor nuevo o elimine un valor. También puede agregar otros filtros.  
  
6.  Haga clic en **Aceptar** y guarde la plantilla.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  