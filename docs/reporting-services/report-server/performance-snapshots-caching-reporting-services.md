---
title: "Rendimiento, instantáneas, almacenamiento en caché (Reporting Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
caps.latest.revision: "20"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 90444a549b665fb1577b829df3ddae46687565fa
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="performance-snapshots-caching-reporting-services"></a>Rendimiento, instantáneas, almacenamiento en caché (Reporting Services)
  El rendimiento del servidor de informes se ve afectado por una combinación de factores entre los que se incluyen el hardware, el número de usuarios simultáneos que tienen acceso a los informes, la cantidad de datos de un informe y el formato de salida. Para entender los factores de rendimiento específicos de su instalación y qué remedios generarán los resultados que desea, necesitará obtener datos de línea base y ejecutar pruebas. Para obtener más información sobre herramientas e instrucciones, vea las publicaciones siguientes en MSDN: [Optimización del rendimiento de Reporting Services](http://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) y [Usar Visual Studio 2005 para realizar pruebas de carga en un servidor de informes de SQL Server 2005 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=77519).  
  
 Entre los principios generales que hay que tener en cuenta se incluyen los siguientes:  
  
-   La representación y el procesamiento de informes consumen mucha memoria. Cuando sea posible, elija un equipo que tenga mucha memoria.  
  
-   Hospedar el servidor de informes y la base de datos del servidor de informes en equipos independientes suele generar mejor rendimiento que hospedarlos en un único equipo de tecnología avanzada.  
  
-   Si todos los informes se procesan despacio, piense en una implementación escalada donde varias instancias del servidor de informes admitan una única base de datos del servidor de informes. Para obtener mejores resultados, use el software de equilibrio de carga para distribuir solicitudes de forma uniforme en la implementación.  
  
-   Si un solo informe se procesa con lentitud, ajuste las consultas del conjunto de datos del informe si este debe ejecutarse a petición. También podría considerar usar conjuntos de datos compartidos que pueda almacenar en memoria caché, almacenar en memoria caché el informe o ejecutarlo como una instantánea.  
  
-   Si todos los informes se procesan en un formato concreto (por ejemplo, al representarse en PDF), piense en la entrega a recursos compartidos de archivos, en agregar más memoria o en elegir un formato diferente.  
  
-   Para averiguar cuánto tiempo se tarda en procesar un informe y otras métricas de uso, revise el registro de ejecución del servidor de informes. Para más información, vea [Registro de ejecución del servidor de informes y la vista ExecutionLog3](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
-   Para más información sobre cómo reducir los problemas de rendimiento con la configuración de la administración de la memoria, vea [Configurar la memoria disponible para aplicaciones del servidor de informes](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Supervisar el rendimiento del servidor de informes](../../reporting-services/report-server/monitoring-report-server-performance.md)  
 Describe los objetos de rendimiento que puede usar para realizar un seguimiento de la carga de procesamiento en su servidor.  
  
 [Establecer las propiedades del procesamiento de informes](../../reporting-services/report-server/set-report-processing-properties.md)  
 Describe los modos de configuración de un informe para ejecutarlo a petición, desde la memoria caché, o en función de una programación como una instantánea de informe.  
  
 [Configurar la memoria disponible para aplicaciones del servidor de informes](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
 Describe cómo puede invalidar el comportamiento predeterminado de administración de memoria.  
  
 [Informes almacenados en caché &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 Describe el comportamiento del almacenamiento en caché de los informes de un servidor de informes.  
  
 [Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
 Describe el comportamiento del almacenamiento en caché de conjuntos de datos compartidos en un servidor de informes.  
  
 [Procesar informes grandes](../../reporting-services/report-server/process-large-reports.md)  
 Proporciona recomendaciones sobre cómo configurar y distribuir un informe de gran tamaño.  
  
 [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 Explica cómo establecer los tiempos de espera para el procesamiento de informes y de consultas.  
  
## <a name="see-also"></a>Ver también  
 [Administrar un proceso en ejecución](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [Verificación de la ejecución de un informe](../../reporting-services/report-server/verifying-a-report-run.md)  
  
  
