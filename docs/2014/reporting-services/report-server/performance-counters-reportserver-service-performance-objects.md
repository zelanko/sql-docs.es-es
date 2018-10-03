---
title: 'Contadores de rendimiento para los objetos de rendimiento de ReportServer: Service y reportserversharepoint: Service | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Server service, performance counters
ms.assetid: 2bcacab2-3a4f-4aae-b123-19d756b9b9ed
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d7acb87440377516e287e8ba077242953f13adc3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48141715"
---
# <a name="performance-counters-for-the-reportserverservice--and-reportserversharepointservice-performance-objects"></a>Contadores de rendimiento de los objetos ReportServer:Service y ReportServerSharePoint:Service
  En este tema se describen los contadores de rendimiento para los siguientes objetos de rendimiento [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:  
  
-   `ReportServer:Service`  
  
-   `ReportServerSharePoint:Service`  
  
> [!NOTE]  
>  Los objetos de rendimiento se utilizan para supervisar eventos en el servidor de informes local. Si ejecuta un servidor de informes en una implementación escalada, los recuentos se aplican al servidor actual y no a la implementación escalada completa.  
  
 Los objetos de rendimiento están disponibles en el Monitor de rendimiento de Windows (**Perfmon.exe**). Para obtener más información, consulte la documentación de Windows. [Generar perfiles en tiempo de ejecución](http://msdn.microsoft.com/library/w4bz2147.aspx) (http://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 En este tema:  
  
-   [Contadores de rendimiento de ReportServer:Service (servidor de informes de modo nativo)](#bkmk_ReportServer)  
  
-   [ReportServerSharePoint:Service (servidor de informes en modo de SharePoint)](#bkmk_ReportServerSharePoint)  
  
-   [Usar cmdlets de PowerShell para devolver listas](#bkmk_powershell)  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] El modo de SharePoint | Modo nativo.  
  
##  <a name="bkmk_ReportServer"></a> Contadores de rendimiento de ReportServer:Service (servidor de informes de modo nativo)  
 El objeto de rendimiento `ReportServer:Service` incluye una colección de contadores para realizar el seguimiento de eventos relacionados con HTTP y eventos relacionados con memoria para una instancia del servidor de informes. Este objeto de rendimiento aparece una vez por cada [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] instancia en el equipo, por lo que puede agregar o quitar contadores del objeto de rendimiento para cada instancia. Los contadores de la instancia predeterminada aparecen con el formato `ReportServer:Service`. Los contadores de las instancias con nombre aparecen con el formato `ReportServer$<` *instance_name*`>:Service`.  
  
 El `ReportServer:Service` era nuevo en el objeto de rendimiento [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], y proporciona un subconjunto de contadores que se incluyeron con Internet Information Services (IIS) y [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] en versiones anteriores de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Estos nuevos contadores son específicos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y realizan el seguimiento de los eventos relacionados con HTTP para el servidor de informes, como solicitudes, conexiones e intentos de inicio de sesión. Además, este objeto de rendimiento incluye los contadores para realizar el seguimiento de los eventos de administración de memoria.  
  
 En la tabla siguiente se enumera los contadores que se incluyen en el `ReportServer:Service` objeto de rendimiento.  
  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") El siguiente script de Windows PowerShell devolverá la lista de contadores de rendimiento de CounterSetName  
  
```  
(get-counter -listset "ReportServer:Service").paths  
```  
  
|Contador|Descripción|  
|-------------|-----------------|  
|`Active connections`|El número de conexiones actualmente activas en el servidor.|  
|`Bytes Received Total`|Número de bytes recibidos por el servidor. Este contador cuenta los bytes sin formato recibidos en total por el Administrador de informes y el servidor de informes.|  
|`Bytes Received/sec`|El número de bytes recibidos por segundo por el servidor. Este contador solamente está actualizado cuando se completa una transferencia. Esto significa que el contador permanece en 0 y a continuación, el valor aumenta después de que una transferencia haya finalizado.|  
|`Bytes Sent Total`|El número de bytes enviado desde el servidor. Este contador cuenta los bytes sin formato enviados en total por el Administrador de informes y el servidor de informes.|  
|`Bytes Sent/sec`|El número de bytes enviado por segundo desde el servidor. Este contador solamente está actualizado cuando se completa una transferencia. Esto significa que el contador permanece en 0 y a continuación, el valor aumenta después de que una transferencia haya finalizado.|  
|`Errors Total`|El número total de errores no controlados que ocurrieron durante el procesamiento de solicitudes HTTP. Estos errores incluyen los códigos de estado HTTP en los 400s y 500s.|  
|`Errors/sec`|El número total de errores que ocurren por segundo durante el procesamiento de solicitudes HTTP. Estos errores incluyen los códigos de estado HTTP en los 400s y 500s.|  
|`Logon Attempts Total`|El número de intentos de inicio de sesión realizados desde los tipos de autenticación de RSWindows. Los tipos de autenticación de RSWindows incluyen RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos y RSWindowsB asic. El valor cero (0) representa la autenticación personalizada.|  
|`Logon Attempts/sec`|La tasa de intentos de inicio de sesión.|  
|`Logon Successes Total`|El número de inicios de sesión correctos para los tipos de autenticación de RSWindows. Los tipos de autenticación de RSWindows incluyen RSWindowsNegotiate, RSWindowsNTLM, RSWindowsKerberos y RSWindowsB asic. El valor cero (0) representa la autenticación personalizada.|  
|`Logon Successes/sec`|La tasa de inicio de sesión correctos.|  
|`Memory Pressure State`|Uno de los números siguientes, del 1 al 5, que indican el estado de la memoria actual del servidor:<br /><br /> 1: Ninguna presión<br /><br /> 2: Baja presión<br /><br /> 3: Presión media<br /><br /> 4: Alta presión<br /><br /> 5: Presión superada|  
|`Memory Shrink Amount`|El número de bytes que el servidor solicitó reducir la memoria en uso.|  
|`Memory Shrink Notifications/sec`|El número de notificaciones que el servidor emitió en el último segundo para reducir la memoria en uso. Este valor indica la frecuencia con la que el servidor experimenta la presión de memoria.|  
|`Requests Disconnected`|El número de solicitudes que se han desconectado debido a errores en la comunicación.|  
|`Requests Executing`|El número de solicitudes que están procesando actualmente.|  
|`Requests Not Authorized`|El número de solicitudes ejecutadas incorrectamente con un código de estado 401.|  
|`Requests Rejected`|El número total de solicitudes no ejecutadas debido a que no hay suficientes recursos en el servidor para procesarlas. Este contador representa el número de solicitudes que encuentran el código de estado 503 HTTP, que indica que el servidor está ocupado.|  
|`Requests Total`|El número total de solicitudes que son recibidas por el servicio del servidor de informes desde el inicio. Este contador cuenta solicitudes que se envían al Administrador de informes y solicitudes que se envían desde el Administrador de informes al servidor de informes.|  
|`Requests/sec`|El número de solicitudes que se procesan por segundo. Este valor representa el rendimiento actual de la aplicación.|  
|`Tasks Queued`|El número de tareas que están esperando para que un subproceso esté disponible para su proceso. Cada solicitud realizada al servidor de informes corresponde a una o más tareas. Este contador representa únicamente el número de tareas listas para su procesamiento; no incluye el número de tareas que se está ejecutando actualmente.|  
  
##  <a name="bkmk_ReportServerSharePoint"></a> ReportServerSharePoint:Service (servidor de informes en modo de SharePoint)  
 El `ReportServerSharePoint:Service` se agregó el objeto de rendimiento en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") El siguiente script de Windows PowerShell devolverá la lista de contadores de rendimiento de CounterSetName  
  
```  
(get-counter -listset "ReportServerSharePoint:Service").paths  
```  
  
|Contador|  
|-------------|  
|`Memory Pressure State`|  
|`Memory Shrink Amount`|  
|`Memory Shrink Notifications/Sec`|  
  
##  <a name="bkmk_powershell"></a> Usar cmdlets de PowerShell para devolver listas  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "Contenido relacionado con PowerShell") El siguiente script de Windows PowerShell devolverá la lista de contadores de rendimiento de CounterSetName "ReportServerSharePoint:Service":  
  
```  
(get-counter -listset "ReportServerSharePoint:Service").paths  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el rendimiento del servidor de informes](monitoring-report-server-performance.md)   
 [Contadores de rendimiento para el servicio Web de MSRS 2014 y objetos de rendimiento de MSRS 2014 Windows Service &#40;modo nativo&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)   
 [Los contadores de rendimiento para el modo de SharePoint de MSRS 2014 Web Service y los objetos de rendimiento del modo de SharePoint de MSRS 2014 Windows Service &#40;el modo de SharePoint&#41;]... / performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
  
  
