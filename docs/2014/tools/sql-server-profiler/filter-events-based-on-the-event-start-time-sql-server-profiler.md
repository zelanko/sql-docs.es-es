---
title: Filtrar eventos basándose en la hora de inicio del evento (SQL Server Profiler) | Microsoft Docs
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
- event start times [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: e965579e-d006-41a3-89ec-cfd5398c67d2
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f52726d45b27dfc9a4a7f86f4a0261219e26c7e6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105727"
---
# <a name="filter-events-based-on-the-event-start-time-sql-server-profiler"></a>Filtrar eventos basándose en la hora de inicio del evento (SQL Server Profiler)
  En este tema se describe el modo de filtrar eventos de seguimiento basándose en la hora de inicio del evento mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-filter-an-event-based-on-the-event-start-time"></a>Para filtrar un evento en función de la hora de inicio del evento  
  
1.  En el menú **Archivo** , haga clic en **Nuevo seguimiento**y conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Aparecerá el cuadro de diálogo **Propiedades de seguimiento**.  
  
    > [!NOTE]  
    >  Si se selecciona **Iniciar el seguimiento inmediatamente tras realizar la conexión**, el cuadro de diálogo **Propiedades de seguimiento**no aparecerá y, en su lugar, se iniciará el seguimiento. Para desactivar esta configuración, en el menú **Herramientas**, haga clic en **Opciones**y desactive la casilla **Iniciar el seguimiento inmediatamente tras realizar la conexión** .  
  
2.  En el cuadro **Nombre de seguimiento** , escriba un nombre para el seguimiento.  
  
3.  En el cuadro **Use the template**(Usar la plantilla), seleccione una plantilla de seguimiento.  
  
4.  Opcionalmente, especifique un destino para los resultados del seguimiento.  
  
5.  En el menú **Selección de eventos**, haga clic en el encabezado de columna **StartTime** . También puede hacer clic con el botón derecho en el encabezado de la columna y hacer clic en **Editar filtro de columna** para abrir el cuadro de diálogo **Editar filtro** .  
  
6.  Expanda **mayor** o **inferior a**y, a continuación, escriba un `datetime` valor en el campo que aparece debajo del operador de comparación.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  