---
title: Contadores de rendimiento para el modo de SharePoint de MSRS 2014 Web Service y MSRS 2014 Windows Service SharePoint modo objetos de rendimiento (modo SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- counters [Reporting Services]
- Report Server Windows service, performance counters
- RS Windows Service performance object
- Scheduling and Delivery Processor performance object [Reporting Services]
- performance [Reporting Services]
ms.assetid: 70bf6980-7845-4ab5-8b2a-ebf526d811a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d994fa563870f01f4a9ca8824b5372587eca804b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103696"
---
# <a name="performance-counters-for-the-msrs-2014-web-service-sharepoint-mode-and-msrs-2014-windows-service-sharepoint-mode-performance-objects-sharepoint-mode"></a>Contadores de rendimiento para los objetos de rendimiento en modo SharePoint de MSRS 2014 Web Service y SharePoint de MSRS 2014 Windows Service (modo SharePoint)
  En este tema se describen los contadores de rendimiento para los objetos de rendimiento `MSRS 2014 Web Service SharePoint Mode` y `MSRS 2014 Windows Service SharePoint Mode` que forman parte de una implementación de modo [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] SharePoint.  
  
> [!NOTE]  
>  Estos objetos de rendimiento supervisan los eventos en el servidor de informes local. Si ejecuta un servidor de informes en una implementación escalada, los recuentos se aplican al servidor actual y no a la implementación escalada completa.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]  
  
 Los objetos de rendimiento están disponibles en el Monitor de rendimiento de Windows (**Perfmon.exe**). Para obtener más información, consulte la documentación de Windows. [Generar perfiles en tiempo de ejecución](https://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 **En este tema:**  
  
-   [Contadores de rendimiento del modo de SharePoint de MSRS 2014 Web Service](#bkmk_webservice)  
  
-   [Contadores de rendimiento del modo de SharePoint de MSRS 2014 Windows Service](#bkmk_windowsservice)  
  
-   [Usar cmdlets de PowerShell para devolver listas](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> Contadores de rendimiento del modo de SharePoint de MSRS 2014 Web Service  
 El objeto de rendimiento `MSRS 2014 Web Service SharePoint Mode` supervisa el rendimiento del servidor de informes. Este objeto de rendimiento incluye una colección de contadores que se usan para realizar el seguimiento del procesamiento del servidor de informes que se suele iniciar mediante operaciones interactivas de visualización de informes. Cuando se configura este contador, se puede aplicar a todas las instancias de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] o se pueden seleccionar instancias concretas. Estos contadores se restablecen siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.  
  
 En la tabla siguiente se enumeran los contadores que se incluyen con el objeto de rendimiento `MSRS 2014 Web Service SharePoint Mode`.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|`Active Sessions`|Número de sesiones activas. Este contador proporciona un recuento acumulativo de todas las sesiones del explorador que se generan a partir de las ejecuciones de informes, independientemente de si todavía están o no activas.<br /><br /> El contador se reduce cuando se quitan registros de sesiones. De forma predeterminada, las sesiones se quitan después de diez minutos de inactividad.|  
|`Cache Hits/Sec`|Número de solicitudes por segundo para informes en memoria caché. Se trata de solicitudes para informes que se vuelven a representar, no de solicitudes para informes procesados directamente desde la memoria caché. (Vea `Total Cache Hits` más adelante en este tema).|  
|`Cache Hits/Sec (Semantic Models)`|Número de solicitudes por segundo para el modelo en memoria caché. Se trata de solicitudes para informes que se vuelven a representar, no de solicitudes para informes procesados directamente desde la memoria caché.|  
|`Cache Misses/Sec`|Número de solicitudes por segundo que no han podido devolver un informe de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|`Cache Misses/Sec (Semantic Models)`|Número de solicitudes por segundo que no han podido devolver un modelo de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|`First Session Requests/Sec`|Número de nuevas sesiones de usuario que se inician desde la memoria caché del servidor de informes por segundo.|  
|`Memory Cache Hits/Sec`|Número de veces por segundo que se recuperan informes de la memoria caché en memoria. La*caché en memoria* es una parte de la memoria caché que almacena informes en la memoria de la CPU. Cuando se usa la memoria caché en memoria, el servidor de informes no realiza una consulta en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el contenido en memoria caché.|  
|`Memory Cache Misses/Sec`|Número de veces por segundo que no se han podido recuperar informes de la memoria caché en memoria.|  
|`Next Session Requests/Sec`|Número de solicitudes por segundo de informes que se abren en una sesión existente (como informes que se representan a partir de una instantánea de sesión).|  
|`Report Requests`|Número de informes actualmente activos que el servidor de informes está procesando.|  
|`Reports Executed/Sec`|Número de ejecuciones de informes logradas por segundo. Este contador proporciona estadísticas sobre el volumen de informes. Utilice este contador con `Request/Sec` para comparar la ejecución de informes con las solicitudes de informes que pueden devolverse desde la memoria caché.|  
|`Requests/Sec`|Número de solicitudes por segundo realizadas al servidor de informes. Este contador realiza un seguimiento de todos los tipos de solicitudes que procesa el servidor de informes.|  
|`Total Cache Hits`|Número total de solicitudes de informes de la memoria caché después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
|`Total Cache Hits (Semantic Models)`|Número total de solicitudes del modelo de la memoria caché después del inicio del servicio. Este contador se restablece siempre que ASP.NET detiene el servicio web del servidor de informes.|  
|`Total Cache Misses`|Número total de veces que no se ha podido devolver un informe de la memoria caché después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes. Utilice este contador para determinar si el espacio en disco y la memoria son suficientes.|  
|`Total Cache Misses (Semantic Models)`|Número total de veces que no se ha podido devolver un modelo de la memoria caché después del inicio del servicio. Este contador se restablece siempre que ASP.NET detiene el servicio web del servidor de informes. Utilice este contador para determinar si el espacio en disco y la memoria son suficientes.|  
|`Total Memory Cache Hits`|Número total de informes en memoria caché devueltos desde la memoria caché en memoria después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes. La*caché en memoria* es una parte de la memoria caché que almacena informes en la memoria de la CPU. Cuando se usa la memoria caché en memoria, el servidor de informes no realiza una consulta en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el contenido en memoria caché.|  
|`Total Memory Cache Misses`|Número total de errores de memoria caché en la memoria caché en memoria después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
|`Total Processing Failures`|Número de errores del procesamiento de la solicitud de servicio web del servidor de informes.|  
|`Total Rejected Threads`|Número total de subprocesos rechazados para el procesamiento asincrónico y tratados posteriormente como procesos sincrónicos en el mismo subproceso. Cada origen de datos se procesa en un subproceso. Si el volumen de subprocesos es superior a la capacidad, se rechazan subprocesos para el procesamiento asincrónico y, a continuación, se procesan en serie.|  
|`Total Reports Executed`|Número total de informes que se han ejecutado correctamente después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
|`Total Requests`|Número total de solicitudes efectuadas al servidor de informes después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
  
##  <a name="bkmk_windowsservice"></a> Contadores de rendimiento del modo de SharePoint de MSRS 2014 Windows Service  
 El objeto de rendimiento `MSRS 2014 Windows Service SharePoint Mode` se usa para supervisar el servicio Servidor de informes de Windows. Este objeto de rendimiento incluye una colección de contadores que se usan para realizar el seguimiento del procesamiento de informes que se inicia mediante operaciones programadas. Entre las operaciones programadas se incluyen la suscripción y la entrega, las instantáneas de ejecución de informes y el historial del informe. Cuando se configura este contador, se puede aplicar a todas las instancias de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] o se pueden seleccionar instancias concretas.  
  
 En la tabla siguiente se enumeran los contadores que se incluyen con el objeto de rendimiento `MSRS 2014 Windows Service SharePoint mode`.  
  
|Contador|Descripción|  
|-------------|-----------------|  
|`Active Sessions`|Número de sesiones activas almacenadas en la base de datos del servidor de informes. Este contador proporciona un recuento acumulativo de todas las sesiones del explorador que se pueden utilizar generadas a partir de suscripciones de informes, independientemente de si todavía están o no activas.|  
|`Alerting: event queue length`||  
|`Alerting: events processed - CreateSchedule`||  
|`Alerting: events processed - Delete schedule`||  
|`Alerting: events processed - DeliverAlert`||  
|`Alerting: events processed - FireAlert`||  
|`Alerting: events processed - FireSchedule`||  
|`Alerting: events processed - GenerateAlert`||  
|`Alerting: events processed - UpdateSchedule`||  
|`Cache Flushes/Sec`|Número de vaciados de memoria caché por segundo.|  
|`Cache Hits/Sec`|Número de solicitudes por segundo para informes en memoria caché. Se trata de solicitudes para informes que se vuelven a representar, no de solicitudes para informes procesados directamente desde la memoria caché. (Vea `Total Cache Hits` más adelante en este tema).|  
|`Cache Hits/Sec (Semantic Models)`|Número de solicitudes por segundo para los modelos en memoria caché.|  
|`Cache Misses/Sec`|Número de solicitudes por segundo que no han podido devolver un informe de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|`Cache Misses/Sec (Semantic Models)`|Número de solicitudes por segundo que no han podido devolver un modelo de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|`Delivers/Sec`|Número de entregas de informes por segundo, desde cualquier extensión de entrega.|  
|`Events/Sec`|Número de eventos procesados por segundo. Entre los eventos que se supervisan se incluyen `SnapshotUpdated` y `TimedSubscription`.|  
|`First Session Requests/Sec`|Número de nuevas sesiones de ejecución de informe creadas por segundo.|  
|`Memory Cache Hits/Sec`|Número de veces por segundo que se recuperan informes de la memoria caché en memoria. La*caché en memoria* es una parte de la memoria caché que almacena informes en la memoria de la CPU. Cuando se usa la memoria caché en memoria, el servidor de informes no realiza una consulta en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para el contenido en memoria caché.|  
|`Memory Cache Misses/Sec`|Número de veces por segundo que no se pueden recuperar informes de la memoria caché en memoria.|  
|`Next Session Requests/Sec`|Número de solicitudes por segundo de informes que se abren en una sesión existente (como informes que se representan a partir de una instantánea de sesión).|  
|`Report Requests`|Número de informes actualmente activos que el servidor de informes está procesando. Utilice este contador para evaluar la estrategia de almacenamiento en memoria caché. Es posible que haya bastantes más solicitudes que informes generados.|  
|`Reports Executed/Sec`|Número de informes generados correctamente por segundo.|  
|`Requests/Sec`|Número total de solicitudes correctas que el servicio del servidor de informes procesó por segundo.|  
|`Snapshot Updates/Sec`|Número total de actualizaciones de instantánea de ejecución de informes por segundo.|  
|`Total App Domain Recycles`|Número total de ciclos de dominio de aplicación después del inicio del servicio Windows del servidor de informes.|  
|**Total de vaciados de caché**|Número total de actualizaciones de memoria caché del servidor de informes después del inicio del servicio. Este contador se restablece tras los reciclamientos de dominio de aplicación. Vea `Cache Flushes/Sec`.|  
|`Total Cache Hits`|Número total de solicitudes de informes procesadas directamente desde la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación. Vea `Cache Hits/Sec`.|  
|`Total Cache Hits (Semantic Models)`|Número total de solicitudes de modelo procesadas directamente desde la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Cache Misses`|Número total de veces que no se ha podido devolver un informe de la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación. Vea `Cache Misses/Sec`.|  
|`Total Cache Misses (Semantic Models)`|Número total de veces que no se ha podido devolver un modelo de la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Deliveries`|Número total de informes entregados por el Procesador de entrega y programación para todas las extensiones de entrega. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Events`|Número total de eventos después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Memory Cache Hits`|Número total de informes en memoria caché devueltos desde la memoria caché en memoria después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Memory Cache Misses`|Número total de errores de memoria caché en la memoria caché en memoria después del inicio del servicio. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Processing Failures`|Número de errores del procesamiento de la solicitud de servicio Windows del servidor de informes.|  
|`Total Rejected Threads`|Número total de subprocesos rechazados para el procesamiento asincrónico y tratados posteriormente como un proceso sincrónico en el mismo subproceso. Con carga moderada o sobrecarga, este contador aumenta regularmente.|  
|`Total Reports Executed`|Número total de informes ejecutados.|  
|`Total Requests`|Número total de informes que se han ejecutado correctamente después del inicio del servicio. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|`Total Snapshot Updates`|Número total de actualizaciones de instantánea de ejecución de informes.|  
  
##  <a name="bkmk_powershell"></a> Usar cmdlets de PowerShell para devolver listas  
 ![Contenido relacionado con PowerShell](../media/rs-powershellicon.jpg "PowerShell related content")El script de Windows PowerShell siguiente devolverá los conjuntos de contadores en los que CounterSetName comienza con "msr".  
  
```  
get-counter -listset msr*  
Returns a list with the following information  
CounterSetName     : MSRS 2014 Windows Service SharePoint Mode  
CounterSetName     : MSRS 2014 Web Service SharePoint Mode  
```  
  
 El siguiente script de Windows PowerShell devolverá la lista de contadores de rendimiento para CounterSetName "MSRS 2014 Windows Service SharePoint Mode".  
  
```  
(get-counter -listset "MSRS 2014 Windows Service SharePoint Mode").paths  
```  
  
## <a name="see-also"></a>Vea también  
 [Supervisar el rendimiento del servidor de informes](monitoring-report-server-performance.md)   
 [Contadores de rendimiento para el servicio Web de MSRS 2014 y objetos de rendimiento de MSRS 2014 Windows Service &#40;modo nativo&#41;](../report-server/performance-counters-msrs-2011-web-service-performance-objects.md)  
  
  
