---
title: Filtrar eventos en un seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
- traces [SQL Server], events
ms.assetid: 0fd63573-3b35-4f67-9e1e-ed9aabee11a8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb6b2a2d579391fd5c8849e4251864da69e3b543
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097815"
---
# <a name="filter-events-in-a-trace-sql-server-profiler"></a>Filtrar eventos en un seguimiento (SQL Server Profiler)
  Los filtros limitan los eventos que se recopilan en el seguimiento. Si no se establece un filtro, se devolverán todos los eventos de las clases de eventos seleccionadas en el resultado del seguimiento. No es obligatorio establecer un filtro para un seguimiento. Sin embargo, un filtro minimiza la sobrecarga que comporta una traza.  
  
 Para agregar filtros a las definiciones de seguimiento, utilice la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades de seguimiento** o **Propiedades de la plantilla de seguimiento** .  
  
### <a name="to-filter-events-in-a-trace"></a>Para filtrar los eventos de un seguimiento  
  
1.  En el cuadro de diálogo **Propiedades de seguimiento** o **Propiedades de la plantilla de seguimiento** , haga clic en la pestaña **Selección de eventos** .  
  
     La pestaña **Selección de eventos** contiene un control de cuadrícula. El control de cuadrícula es una tabla que contiene todas las clases de eventos en las que se puede realizar un seguimiento. La tabla contiene una fila para cada clase de evento. Las clases de eventos pueden diferir ligeramente dependiendo del tipo y la versión del servidor al que esté conectado. Las clases de eventos se identifican en la columna **Events**de la cuadrícula y se agrupan por categorías de eventos. En las demás columnas se enumeran las columnas de datos que pueden devolverse para cada clase de evento.  
  
2.  Haga clic en **Filtros de columna.**  
  
     La pestaña **Editar filtro**. La pestaña **Editar filtro**incluye una lista de operadores de comparación que se pueden utilizar para filtrar los eventos en un seguimiento.  
  
3.  Para aplicar un filtro, haga clic en el operador de comparación y escriba un valor para utilizarlo con el filtro.  
  
4.  Haga clic en **Aceptar**.  
  
 **Consideraciones:**  
  
-   Si establece condiciones de filtro en las columnas de datos **StartTime** y **EndTime** de la pestaña Selección de eventos, asegúrese de lo siguiente:  
  
    -   La fecha especificada tiene el formato `YYYY/MM/DD HH:mm:sec`.  
  
         -O bien-  
  
    -   Se ha seleccionado la opción**Usar la configuración regional para mostrar valores de fecha y hora** del cuadro de diálogo **Opciones generales** . Para ver el cuadro de diálogo **Opciones generales** , en el menú [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **del** , haga clic en **Opción**.  
  
         Y  
  
    -   La fecha especificada se encuentra entre el 1 de enero de 1753 y el 31 de diciembre de 9999.  
  
-   Si se realiza un seguimiento de los eventos con la utilidad **osql** o **sqlcmd** , agregue siempre **%** a los filtros de la columna de datos **TextData** .  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
