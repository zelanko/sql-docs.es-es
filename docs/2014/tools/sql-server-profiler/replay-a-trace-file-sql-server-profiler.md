---
title: Reproducir un archivo de seguimiento (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 9e361275-c8fd-4499-8389-242cf8e27415
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 503f7a3eeeeeee36893231c48b330a099a5adc61
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63240499"
---
# <a name="replay-a-trace-file-sql-server-profiler"></a>Reproducir un archivo de seguimiento (SQL Server Profiler)
  La reproducción es la capacidad de abrir un seguimiento guardado y reproducirlo más tarde. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] incluye un motor de reproducción de varios subprocesos que puede simular conexiones de usuario y la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La reproducción es útil para solucionar problemas de aplicaciones o procesos. Cuando identifique el problema e implemente las acciones para corregirlo, ejecute el seguimiento que encontró el posible problema en la aplicación o proceso corregido. A continuación, reproduzca el seguimiento original y compare los resultados.  
  
 Además de otras clases de eventos que desee supervisar, debe capturar clases de eventos específicas para habilitar la reproducción: Estos eventos se capturan de forma predeterminada si se usa la plantilla de seguimiento **TSQL_Replay** . Para más información, consulte [Replay Requirements](replay-requirements.md).  
  
### <a name="to-replay-a-trace-file"></a>Para reproducir un archivo de seguimiento  
  
1.  En el menú **Archivo** , seleccione **Abrir**y, a continuación, haga clic en **Archivo de seguimiento**. Seleccione un archivo de seguimiento que contenga las clases de eventos necesarias para la reproducción.  
  
2.  En el menú **Reproducir** , haga clic en **Iniciar**y conéctese a la instancia del servidor en la que desee reproducir el seguimiento.  
  
3.  En el cuadro de diálogo **Configuración de reproducción** , en la pestaña **Opciones básicas de reproducción** , especifique **Servidor de reproducción**. Haga clic en **Cambiar** para cambiar el servidor visualizado en el cuadro **Servidor de reproducción** .  
  
4.  Opcionalmente, seleccione uno de los siguientes destinos para guardar la reproducción:  
  
    -   **Guardar en el archivo**, que especifica un archivo en el que se guardará la reproducción.  
  
    -   **Guardar en la tabla**, que especifica una tabla de base de datos en la que se guardará la reproducción.  
  
5.  Elija **Reproducir eventos en el oden de seguimiento**o **Reproducir eventos mediante múltiples subprocesos**. En la tabla siguiente se explica la diferencia entre estas opciones.  
  
    |Opción|Descripción|  
    |------------|-----------------|  
    |**Reproducir eventos en el orden del seguimiento**|Reproduce los eventos en el orden en que se registraron. Esta opción habilita la depuración.|  
    |**Reproducir eventos mediante múltiples subprocesos**|Esta opción utiliza varios subprocesos para reproducir cada evento, independientemente de la secuencia. Esta opción optimiza el rendimiento.|  
  
6.  Seleccione **Mostrar resultados de la reproducción** para ver la reproducción mientras se ejecuta.  
  
7.  Si lo desea, haga clic en la pestaña **Opciones avanzadas de reproducción**para configurar las siguientes opciones:  
  
    -   Para reproducir todos los identificadores de proceso de servidor (SPID), seleccione **Reproducir los SPID del sistema**.  
  
    -   Para limitar la reproducción a los procesos que pertenecen a un determinado SPID, seleccione **Reproducir solo un SPID**. En el cuadro **SPID para reproducir** , escriba el SPID.  
  
    -   Para reproducir eventos producidos durante un determinado periodo, seleccione **Limitar reproducción por fecha y hora**. Seleccione una fecha y una hora en **Hora de inicio**y **Hora de finalización**para especificar el periodo que se incluirá en la reproducción.  
  
    -   Para controlar el modo en que SQL Server administra los procesos durante la reproducción, configure **Opciones del monitor de estado**.  
  
## <a name="see-also"></a>Consulte también  
 [Permisos necesarios para ejecutar SQL Server Profiler](sql-server-profiler.md)   
 [Reproducir seguimientos](replay-traces.md)   
 [Abrir un archivo de seguimiento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
