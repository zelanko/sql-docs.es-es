---
title: Servicio web de MSRS 2011 de contadores de rendimiento, objetos de rendimiento | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-server
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance counters [Reporting Services]
- Report Server Web service, performance counters
- Reporting Services performance object
- RS Web Service performance object
- counters [Reporting Services]
- performance [Reporting Services]
ms.assetid: c642fc4f-8734-4626-a194-42ac9cd8e2ef
caps.latest.revision: "50"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4e159f7c4fa846e30fbd1ca8f43b5c18df44d4c5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="performance-counters-msrs-2011-web-service-performance-objects"></a>Servicio web de MSRS 2011 de contadores de rendimiento, objetos de rendimiento
  En este tema se describen los contadores de rendimiento para los objetos de rendimiento **MSRS 2011 Web Service** y **MSRS 2011 Windows Service** . Estos objetos son parte de una implementación de modo nativo de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
> [!NOTE]  
>  Estos objetos de rendimiento supervisan los eventos en el servidor de informes local. Si ejecuta un servidor de informes en una implementación escalada, los recuentos se aplican al servidor actual y no a la implementación escalada.  
  
 Los objetos de rendimiento están disponibles en el Monitor de rendimiento de Windows (**Perfmon.exe**). Para obtener más información, vea la documentación de Windows [Generar perfiles en tiempo de ejecución](http://msdn.microsoft.com/library/w4bz2147.aspx) (http://msdn.microsoft.com/library/w4bz2147.aspx).  
  
 Para obtener información relacionada con los contadores de rendimiento en modo de SharePoint, vea [Contadores de rendimiento para los objetos de rendimiento en modo SharePoint de MSRS 2011 Web Service y SharePoint de MSRS 2011 Windows Service &#40;modo SharePoint&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md).  
  
 En este tema:  
  
-   [Contadores de rendimiento de MSRS 2011 Web Service](#bkmk_webservice)  
  
-   [Contadores de rendimiento de MSRS 2011 Windows Service](#bkmk_windowsservice)  
  
-   [Usar cmdlets de PowerShell para devolver listas](#bkmk_powershell)  
  
##  <a name="bkmk_webservice"></a> Contadores de rendimiento de MSRS 2011 Web Service  
 El objeto de rendimiento **MSRS 2011 Web Service** supervisa el rendimiento del servidor de informes. Este objeto de rendimiento incluye una colección de contadores que se usan para realizar el seguimiento del procesamiento del servidor de informes que se suele iniciar mediante operaciones interactivas de visualización de informes. Cuando se configura este contador, se puede aplicar a todas las instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o se pueden seleccionar instancias concretas. Estos contadores se restablecen siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.  
  
 En la tabla siguiente se enumeran los contadores que se incluyen con el objeto de rendimiento **MSRS 2011 Web Service** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Sesiones activas**|Número de sesiones activas. Este contador proporciona un recuento acumulativo de todas las sesiones del explorador que se generan a partir de las ejecuciones de informes, independientemente de si todavía están o no activas.<br /><br /> El contador se reduce cuando se quitan registros de sesiones. De forma predeterminada, las sesiones se quitan después de diez minutos de inactividad.|  
|**Aciertos de caché por segundo**|Número de solicitudes por segundo para informes en memoria caché. Las solicitudes son para informes que se vuelven a representar, no de solicitudes para informes procesados directamente desde la memoria caché. (Vea **Total de aciertos de caché** más adelante en este tema).|  
|**Aciertos de caché por segundo (modelos semánticos)**|Número de solicitudes por segundo para el modelo en memoria caché. Las solicitudes para informes que se vuelven a representar, no de solicitudes para informes procesados directamente desde la memoria caché.|  
|**Errores de caché por segundo**|Número de solicitudes por segundo que no han podido devolver un informe de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|**Errores de caché por segundo (modelos semánticos)**|Número de solicitudes por segundo que no han podido devolver un modelo de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|**Solicitudes de primera sesión por segundo**|Número de nuevas sesiones de usuario que se inician desde la memoria caché del servidor de informes por segundo.|  
|**Aciertos de caché en memoria por segundo**|Número de veces por segundo que se recuperan informes de la memoria caché en memoria. La*caché en memoria* es una parte de la memoria caché que almacena informes en la memoria de la CPU. Cuando se usa la memoria caché en memoria, el servidor de informes no realiza una consulta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el contenido en memoria caché.|  
|**Errores de caché en memoria por segundo**|Número de veces por segundo que no se han podido recuperar informes de la memoria caché en memoria.|  
|**Solicitudes de siguiente sesión por segundo**|Número de solicitudes por segundo de informes que se abren en una sesión existente (como informes que se representan a partir de una instantánea de sesión).|  
|**Solicitudes de informe**|Número de informes actualmente activos que el servidor de informes administra.|  
|**Informes ejecutados por segundo**|Número de ejecuciones de informes logradas por segundo. Este contador proporciona estadísticas sobre el volumen de informes. Use este contador con **Solicitudes por segundo** para comparar la ejecución de informes con las solicitudes de informes que pueden devolverse desde la memoria caché.|  
|**Solicitudes por segundo**|Número de solicitudes por segundo realizadas al servidor de informes. Este contador realiza un seguimiento de todos los tipos de solicitudes que administra el servidor de informes.|  
|**Total de aciertos de caché**|Número total de solicitudes de informes de la memoria caché después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
|**Total de aciertos de caché (modelos semánticos)**|Número total de solicitudes del modelo de la memoria caché después del inicio del servicio. Este contador se restablece siempre que ASP.NET detiene el servicio web del servidor de informes.|  
|**Total de errores de caché**|Número total de veces que no se ha podido devolver un informe de la memoria caché después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes. Utilice este contador para determinar si el espacio en disco y la memoria son suficientes.|  
|**Total de errores de caché (modelos semánticos)**|Número total de veces que no se ha podido devolver un modelo de la memoria caché después del inicio del servicio. Este contador se restablece siempre que ASP.NET detiene el servicio web del servidor de informes. Utilice este contador para determinar si el espacio en disco y la memoria son suficientes.|  
|**Total de aciertos de caché en memoria**|Número total de informes en memoria caché devueltos desde la memoria caché en memoria después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes. La*caché en memoria* es una parte de la memoria caché que almacena informes en la memoria de la CPU. Cuando se usa la memoria caché en memoria, el servidor de informes no realiza una consulta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el contenido en memoria caché.|  
|**Total de errores de caché en memoria**|Número total de errores de memoria caché en la memoria caché en memoria después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
|**Total de errores de procesamiento**|Número de errores del procesamiento de la solicitud de servicio web del servidor de informes.|  
|**Total de subprocesos rechazados**|Número total de subprocesos rechazados para el procesamiento asincrónico y tratados posteriormente como procesos sincrónicos en el mismo subproceso. Cada origen de datos se procesa en un subproceso. Si el volumen de subprocesos es superior a la capacidad, se rechazan subprocesos para el procesamiento asincrónico y, a continuación, se procesan en serie.|  
|**Total de informes ejecutados**|Número total de informes que se han ejecutado correctamente después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
|**Total de solicitudes**|Número total de solicitudes efectuadas al servidor de informes después del inicio del servicio. Este contador se restablece siempre que [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] detiene el servicio web del servidor de informes.|  
  
##  <a name="bkmk_windowsservice"></a> Contadores de rendimiento de MSRS 2011 Windows Service  
 El objeto de rendimiento **MSRS 2011 Windows Service** supervisa el servicio servidor de informes de Windows. Este objeto de rendimiento incluye una colección de contadores que se usan para realizar el seguimiento del procesamiento de informes que se inicia mediante operaciones programadas. Entre las operaciones programadas se incluyen la suscripción y la entrega, las instantáneas de ejecución de informes y el historial del informe. Cuando se configura este contador, se puede aplicar a todas las instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o se pueden seleccionar instancias concretas.  
  
 En la tabla siguiente se enumeran los contadores que se incluyen con el objeto de rendimiento **MSRS 2011 Windows Service** .  
  
|Contador|Description|  
|-------------|-----------------|  
|**Sesiones activas**|Número de sesiones activas almacenadas en la base de datos del servidor de informes. Este contador proporciona un recuento acumulativo de todas las sesiones del explorador que se pueden utilizar generadas a partir de suscripciones de informes, independientemente de si todavía están o no activas.|  
|**Vaciados de caché por segundo**|Número de vaciados de memoria caché por segundo.|  
|**Aciertos de caché por segundo**|Número de solicitudes por segundo para informes en memoria caché. Las solicitudes son para informes que se vuelven a representar, no de solicitudes para informes procesados directamente desde la memoria caché. (Vea **Total de aciertos de caché** más adelante en este tema).|  
|**Aciertos de caché por segundo (modelos semánticos)**|Número de solicitudes por segundo para los modelos en memoria caché.|  
|**Errores de caché por segundo**|Número de solicitudes por segundo que no han podido devolver un informe de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|**Errores de caché por segundo (modelos semánticos)**|Número de solicitudes por segundo que no han podido devolver un modelo de memoria caché. Utilice este contador para averiguar si los recursos utilizados para el almacenamiento en caché (disco o memoria) son suficientes.|  
|**Entregas por segundo**|Número de entregas de informes por segundo, desde cualquier extensión de entrega.|  
|**Eventos por segundo**|Número de eventos procesados por segundo. Entre los eventos que se supervisan se incluyen **SnapshotUpdated** y **TimedSubscription**.|  
|**Solicitudes de primera sesión por segundo**|Número de nuevas sesiones de ejecución de informe creadas por segundo.|  
|**Aciertos de caché en memoria por segundo**|Número de veces por segundo que se recuperan informes de la memoria caché en memoria. La*caché en memoria* es una parte de la memoria caché que almacena informes en la memoria de la CPU. Cuando se usa la memoria caché en memoria, el servidor de informes no realiza una consulta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el contenido en memoria caché.|  
|**Errores de caché en memoria por segundo**|Número de veces por segundo que no se pueden recuperar informes de la memoria caché en memoria.|  
|**Solicitudes de siguiente sesión por segundo**|Número de solicitudes por segundo de informes que se abren en una sesión existente (como informes que se representan a partir de una instantánea de sesión).|  
|**Solicitudes de informe**|Número de informes actualmente activos que el servidor de informes administra. Utilice este contador para evaluar la estrategia de almacenamiento en memoria caché. Es posible que haya más solicitudes que informes generados.|  
|**Informes ejecutados por segundo**|Número de informes generados correctamente por segundo.|  
|**Solicitudes por segundo**|Número total de solicitudes correctas que el servicio del servidor de informes procesó por segundo.|  
|**Actualizaciones de instantánea por segundo**|Número total de actualizaciones de instantánea de ejecución de informes por segundo.|  
|**Total de reciclados de dominio de aplicación**|Número total de ciclos de dominio de aplicación después del inicio del servicio Windows del servidor de informes.|  
|**Total de vaciados de caché**|Número total de actualizaciones de memoria caché del servidor de informes después del inicio del servicio. Este contador se restablece tras los reciclamientos de dominio de aplicación. Consulte **Vaciados de caché por segundo**.|  
|**Total de aciertos de caché**|Número total de solicitudes de informes procesadas directamente desde la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación. Consulte **Aciertos de caché por segundo**.|  
|**Total de aciertos de caché (modelos semánticos)**|Número total de solicitudes de modelos procesadas directamente desde la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación. Consulte **Aciertos de caché por segundo**.|  
|**Total de errores de caché**|Número total de veces que no se ha podido devolver un informe de la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación. Consulte **Errores de caché por segundo**.|  
|**Total de errores de caché (modelos semánticos)**|Número total de veces que no se ha podido devolver un modelo de la memoria caché después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|**Total de entregas**|Número total de informes entregados a través del Procesador de entrega y programación para todas las extensiones de entrega. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|**N.º total de eventos**|Número total de eventos después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|**Total de aciertos de caché en memoria**|Número total de informes en memoria caché devueltos desde la memoria caché en memoria después del inicio del servicio Windows del servidor de informes. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|**Total de errores de caché en memoria**|Número total de errores de memoria caché en la memoria caché en memoria después del inicio del servicio. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|**Total de errores de procesamiento**|Número de errores del procesamiento de la solicitud de servicio Windows del servidor de informes.|  
|**Total de subprocesos rechazados**|Número total de subprocesos rechazados para el procesamiento asincrónico y tratados posteriormente como un proceso sincrónico en el mismo subproceso. Con carga moderada o sobrecarga, este contador aumenta regularmente.|  
|**Total de informes ejecutados**|Número total de informes ejecutados.|  
|**Total de solicitudes**|Número total de informes que se han ejecutado correctamente después del inicio del servicio. Este contador se restablece tras los reciclamientos de dominio de aplicación.|  
|**Total de actualizaciones de instantánea**|Número total de actualizaciones de instantánea de ejecución de informes.|  
  
##  <a name="bkmk_powershell"></a> Usar cmdlets de PowerShell para devolver listas  
 ![Contenido relacionado con PowerShell](../../analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")El siguiente script de Windows PowerShell devuelve los conjuntos de contadores en los que CounterSetName comienza con "msr":  
  
```  
get-counter -listset msr*  
```  
  
 El siguiente script de Windows PowerShell devuelve la lista de contadores de rendimiento para CounterSetName.  
  
```  
(get-counter -listset "MSRS 2011 Windows Service").paths  
```  
  
## <a name="see-also"></a>Ver también  
 [Supervisar el rendimiento del servidor de informes](../../reporting-services/report-server/monitoring-report-server-performance.md)   
 [Contadores de rendimiento para los objetos de rendimiento en modo SharePoint de MSRS 2011 Web Service y SharePoint de MSRS 2011 Windows Service &#40;modo SharePoint&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)   
 [Contadores de rendimiento de los objetos ReportServer:Service y ReportServerSharePoint:Service](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
  
  
