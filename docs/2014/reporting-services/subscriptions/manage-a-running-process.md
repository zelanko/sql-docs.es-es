---
title: Administrar un proceso en ejecución | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report processing [Reporting Services], status information
- jobs [Reporting Services]
- viewing jobs
- canceling jobs
- user jobs [Reporting Services]
- system jobs [Reporting Services]
- report processing [Reporting Services], managing running processes
- processes [Reporting Services]
- scanning processes [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services]
- canceling subscriptions
- report servers [Reporting Services], jobs
- data-driven subscriptions
- displaying jobs
- subscriptions [Reporting Services], running processes
ms.assetid: 473e574e-f1ff-4ef9-bda6-7028b357ac42
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 12fa851a8f524bae83017042d01a7c7733225fd7
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59962521"
---
# <a name="manage-a-running-process"></a>Administrar un proceso en ejecución
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supervisa el estado de los trabajos que se ejecutan en el servidor de informes. Periódicamente, el servidor de informes realiza un recorrido de los trabajos en curso y escribe la información sobre su estado en su propia base de datos o en las bases de datos de aplicación de servicio para el modo de SharePoint. Un trabajo está en curso si se está llevando a cabo alguno de los siguientes procesos: ejecución de consultas en un servidor de bases de datos remoto o local, procesamiento de informes o representación de informes.  
  
 Se pueden administrar *trabajos de usuario* y *trabajos del sistema*.  
  
-   Los trabajos de usuario puede iniciarlos un usuario individual o una suscripción. Estos trabajos incluyen ejecutar un informe a petición, solicitar una instantánea de historial del informe, crear manualmente una instantánea de informe y procesar una suscripción estándar.  
  
-   Los trabajos del sistema los inicia el servidor de informes. Los trabajos del sistema incluyen instantáneas de ejecución de informe o de historial de informe programadas y suscripciones controladas por datos.  
  
 El tiempo de procesamiento del informe y el uso de recursos varía considerablemente dependiendo del informe, de la complejidad de la consulta, de la cantidad de datos y del formato de representación que se especifica para el informe. Los informes que contienen consultas sencillas con un origen de datos local normalmente se completan en milisegundos y no requieren administración ni optimización. Por el contrario, un informe grande que se representa en formato PDF o Excel podría requerir un tiempo de procesamiento considerable, dependiendo de los recursos de hardware, de las opciones de entrega y de si hay otros procesos en ejecución simultáneamente. En un servidor de informes, la mayoría de los procesos de larga duración son operaciones de representación de informes y procesos que esperan la finalización del procesamiento de una consulta. En ocasiones, es necesario cancelar un proceso de un informe si se desea poner un equipo en modo sin conexión o detener un trabajo en ejecución que está tardando demasiado en completarse.  
  
 Se pueden cancelar los procesos siguientes:  
  
-   Procesamiento de informes a petición.  
  
-   Procesamiento de informes programados.  
  
-   Suscripciones estándar propiedad de usuarios individuales.  
  
 Cuando se cancela un trabajo, únicamente se cancelan los procesos que están en ejecución en el servidor de informes. Dado que el servidor de informes no administra el procesamiento de datos que se produce en otros equipos, se deben cancelar manualmente los procesos de consulta que quedan huérfanos posteriormente en otros sistemas. Es aconsejable especificar valores de tiempo de espera para cancelar automáticamente las consultas que tardan demasiado en ejecutarse. Para más información, vea [Establecer valores de tiempo de espera para el procesamiento de informes y conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md). Para obtener más información sobre la detención temporal de un informe, vea [Pause Report and Subscription Processing](disable-or-pause-report-and-subscription-processing.md).  
  
> [!NOTE]  
>  En algunas circunstancias poco frecuentes, quizás resulte necesario reiniciar el servidor para cancelar un proceso. Para el modo de SharePoint, quizás necesite reiniciar el grupo de aplicaciones que hospeda la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Iniciar y detener el servicio del servidor de informes](../report-server/start-and-stop-the-report-server-service.md).  
  
 En este tema:  
  
-   [Ver y cancelar trabajos (modo nativo)](#bkmk_native)  
  
-   [Ver y cancelar trabajos (modo de SharePoint)](#bkmk_sharepoint)  
  
-   [Administrar trabajos mediante programación](#bkmk_programmatically)  
  
##  <a name="bkmk_native"></a> Ver y cancelar trabajos (modo nativo)  
 Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para ver o cancelar un trabajo que se está ejecutando en el servidor de informes. Debe actualizar la página para recuperar una lista de trabajos que se están ejecutando actualmente u obtener el estado de trabajo actualizado de la base de datos del servidor de informes. Al conectarse a un servidor de informes en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], puede abrir una carpeta Trabajos para ver una lista de informes que se están procesando actualmente en el equipo del servidor de informes. La información del estado para cada trabajo se muestra en la página Propiedades del trabajo. Puede ver información del estado para todos los trabajos abriendo el cuadro de diálogo Cancelar trabajos del Servidor de informes.  
  
 Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para ver o cancelar un trabajo que se está ejecutando en el servidor de informes. Debe actualizar la página para recuperar una lista de trabajos que se están ejecutando actualmente u obtener el estado de trabajo actualizado de la base de datos del servidor de informes. Al conectarse a un servidor de informes en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], puede abrir una carpeta Trabajos para ver una lista de informes que se están procesando actualmente en el equipo del servidor de informes. La información del estado para cada trabajo se muestra en la página Propiedades del trabajo. Puede ver información del estado para todos los trabajos abriendo el cuadro de diálogo Cancelar trabajos del Servidor de informes.  
  
 No puede usar [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para enumerar o cancelar la generación de modelos, el procesamiento de modelos o las suscripciones controladas por datos. Al notificar un servicio, no se proporciona una manera de cancelar el procesamiento o la generación de modelos. Sin embargo, puede cancelar las suscripciones controladas por datos usando las instrucciones proporcionadas en este tema.  
  
### <a name="how-to-cancel-report-processing-or-subscription"></a>Cómo cancelar una suscripción o procesamiento de informes  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], conéctese al servidor de informes. Para obtener instrucciones, vea [Conectar con un servidor de informes en Management Studio](../tools/connect-to-a-report-server-in-management-studio.md).  
  
2.  Abra la carpeta **Trabajos** .  
  
3.  Haga clic con el botón derecho en el informe y, después, haga clic en **Cancelar trabajos**.  
  
### <a name="how-to-cancel-a-data-driven-subscription"></a>Cómo cancelar una suscripción controlada por datos  
  
1.  Abra el archivo RSReportServer.config en un editor de texto.  
  
2.  Busque `IsNotificationService`.  
  
3.  Establézcalo en `False`.  
  
4.  Guarde el archivo.  
  
5.  En el Administrador de informes, elimine la suscripción controlada por datos de la pestaña Suscripciones del informe o de **Mis suscripciones**.  
  
6.  Después de eliminar la suscripción, en el archivo RSReportServer.config, busque `IsNotificationService` y establézcalo en `True`.  
  
7.  Guarde el archivo.  
  
### <a name="configuring-frequency-settings-for-retrieving-job-status"></a>Configurar los ajustes de frecuencia para recuperar el estado del trabajo  
 Un trabajo en ejecución se almacena en la base de datos temporal del servidor de informes. Los parámetros de configuración del archivo RSReportServer.config se pueden modificar para controlar la frecuencia con la que el servidor de informes recorre los trabajos en curso y el intervalo después del cual cambia el estado de un trabajo en ejecución de nuevo a en ejecución. El parámetro `RunningRequestsDbCycle` especifica la frecuencia con la que el servidor de informes recorre los procesos en ejecución. De forma predeterminada, la información de estado se registra cada 60 segundos. El parámetro `RunningRequestsAge` especifica el intervalo que transcurre hasta que un trabajo pasa de considerarse "nuevo" a "en ejecución".  
  
##  <a name="bkmk_sharepoint"></a> Ver y cancelar trabajos (modo de SharePoint)  
 La administración de trabajos en una implementación de SharePoint se lleva a cabo con Administración central de SharePoint, para cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
#### <a name="to-manage-jobs-in-sharepoint-mode"></a>Para administrar trabajos en modo de SharePoint  
  
1.  En Administración central de SharePoint, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Busque y haga clic en el nombre de la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para abrir la página de administración de aplicaciones.  
  
3.  Haga clic **Administrar trabajos**  
  
4.  Haga clic en **Id. de trabajo** para ver los detalles del trabajo.  
  
5.  O haga clic en el cuadro correspondiente a su trabajo y en **Eliminar** para cancelar el trabajo. La eliminación del trabajo no elimina la suscripción.  
  
##  <a name="bkmk_programmatically"></a> Administrar trabajos mediante programación  
 Es posible administrar los trabajos mediante programación o con un script. Para más información, vea <xref:ReportService2010.ReportingService2010.ListJobs%2A>, <xref:ReportService2010.ReportingService2010.CancelJob%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Cancelar trabajos del servidor de informes &#40;Management Studio&#41;](../tools/cancel-report-server-jobs-management-studio.md)   
 [Propiedades del trabajo &#40;Management Studio&#41;](../tools/job-properties-management-studio.md)   
 [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Supervisar el rendimiento del servidor de informes](../report-server/monitoring-report-server-performance.md)  
  
  
