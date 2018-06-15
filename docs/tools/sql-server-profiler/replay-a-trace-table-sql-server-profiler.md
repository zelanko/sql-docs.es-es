---
title: Reproducir una tabla de seguimiento (SQL Server Profiler) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.suite: sql
ms.technology: profiler
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 6a0ad817-3d8d-4495-889d-c66a7ef9e8bb
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f4498980615096326288559221d3ee2f4f4a1870
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076568"
---
# <a name="replay-a-trace-table-sql-server-profiler"></a>Reproducir una tabla de seguimiento (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La reproducción es la capacidad de abrir un seguimiento guardado y reproducirlo más tarde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] incluye un motor de reproducción de varios subprocesos que puede simular conexiones de usuario y la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La reproducción es útil para solucionar problemas de aplicaciones o procesos. Cuando identifique el problema e implemente las acciones para corregirlo, ejecute el seguimiento que encontró el posible problema en la aplicación o proceso corregido. A continuación, reproduzca el seguimiento original y compare los resultados.  
  
 Además de otras clases de eventos que desee supervisar, debe capturar clases de eventos específicas para habilitar la reproducción: Estos eventos se capturan de forma predeterminada si se usa la plantilla de seguimiento **TSQL_Replay** . Para más información, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
### <a name="to-replay-a-trace-table"></a>Para reproducir una tabla de seguimiento  
  
1.  Abra una tabla de seguimiento que contenga las clases de eventos necesarias para la reproducción.  
  
2.  En el menú **Reproducir** , haga clic en **Iniciar**y conéctese a la instancia del servidor en la que desee reproducir el seguimiento.  
  
3.  En el cuadro de diálogo **Configuración de reproducción** , en la pestaña **Opciones básicas de reproducción** , especifique **Servidor de reproducción**. Haga clic en **Cambiar** para cambiar el servidor que aparece en el cuadro **Servidor de reproducción** .  
  
4.  Opcionalmente, seleccione uno de los siguientes destinos para guardar la reproducción:  
  
    -   **Guardar en el archivo,** que especifica un archivo en el que se guardará la reproducción.  
  
    -   **Guardar en la tabla**, que especifica una tabla de base de datos en la que se guardará la reproducción.  
  
5.  Elija **Reproducir eventos en el oden de seguimiento**o **Reproducir eventos mediante múltiples subprocesos**. En la tabla siguiente se explica la diferencia entre estas opciones.  
  
    |Opción|Description|  
    |------------|-----------------|  
    |**Reproducir eventos en el orden del seguimiento**|Reproduce los eventos en el orden en que se registraron. Esta opción habilita la depuración.|  
    |**Reproducir eventos mediante múltiples subprocesos**|Esta opción utiliza varios subprocesos para reproducir cada evento, independientemente de la secuencia. Esta opción optimiza el rendimiento.|  
  
6.  Seleccione **Mostrar resultados de la reproducción** para ver la reproducción mientras se ejecuta.  
  
7.  Opcionalmente, haga clic en la pestaña **Opciones avanzadas de reproducción**para especificar las siguientes opciones:  
  
    -   Para reproducir todos los identificadores de proceso de servidor (SPID), seleccione **Reproducir los SPID del sistema**.  
  
    -   Para limitar la reproducción a los procesos que pertenecen a un determinado SPID, seleccione **Reproducir solo un SPID**. En el cuadro de diálogo **SPID para reproducir**escriba el SPID.  
  
    -   Para reproducir eventos producidos durante un determinado periodo, seleccione **Limitar reproducción por fecha y hora**. Seleccione una fecha y una hora en **Hora de inicio**y **Hora de finalización**para especificar el periodo que se incluirá en la reproducción.  
  
    -   Para controlar el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra los procesos durante la reproducción, configure **Opciones del monitor de estado**.  
  
## <a name="see-also"></a>Ver también  
 [Permisos necesarios para ejecutar SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Reproducir seguimientos](../../tools/sql-server-profiler/replay-traces.md)   
 [Abrir una tabla de seguimiento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-table-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
