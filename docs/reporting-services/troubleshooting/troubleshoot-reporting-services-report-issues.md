---
title: "Solución de problemas de informes de servicios de Reporting | Documentos de Microsoft"
ms.custom: 
ms.date: 02/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a705d103-85b1-49b5-b27f-332b1040d029
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9a8c5f76c0d2cd35f0ef52b77b79b13cc8b5efbe
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot--reporting-services-report-issues"></a>Solución de problemas de informes de Reporting Services
Este tema contiene información útil para solucionar problemas con el diseño de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] , la vista previa de un informe, la publicación de un informe en un servidor de informes en modo nativo o en modo de SharePoint, la visualización de un informe en el servidor de informes o la exportación de un informe en un formato de archivo diferente.  
## <a name="monitor-report-servers"></a>Supervisión de servidores de informes  
Puede utilizar las herramientas del sistema y de base de datos para supervisar la actividad del servidor de informes. También puede ver los archivos del registro de seguimiento del servidor de informes o consultar en el registro de ejecución del servidor de informes información detallada acerca de informes concretos. Si está utilizando el Monitor de rendimiento, puede agregar contadores de rendimiento para el servicio web del servidor de informes y el servicio de Windows con el fin de identificar los cuellos de botella de identidad en el procesamiento a petición o programado.  
Para más información, consulte [Supervisar el rendimiento del servidor de informes](../../reporting-services/report-server/monitoring-report-server-performance.md).  
  
  
## <a name="view-the-report-server-logs"></a>Visualización de los registros del servidor de informes  
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] registra muchos eventos internos y externos en archivos de registro que graban datos sobre informes concretos, información de depuración, solicitudes y respuestas HTTP y eventos del servidor de informes. También puede crear registros de rendimiento y seleccionar contadores de rendimiento que especifiquen los datos que se recopilarán. El directorio predeterminado para los archivos de registro de una instalación predeterminada es `<drive>\Program Files\Microsoft SQL Server\MSRS130.MSSQLSERVER\Reporting Services\LogFiles`.   
  
Para más información, consulte [Archivos de registro y orígenes de Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
Para determinar específicamente si las esperas del informe se deben a la recuperación de datos o al procesamiento o la representación del informe, utilice el registro de ejecución. Para más información, consulte [Registro de ejecución del servidor de informes y la vista ExecutionLog3].   
  
## <a name="view-the-call-stack-for-report-processing-error-messages-on-the-report-server"></a>Ver la pila de llamadas de los mensajes de error de procesamiento de informes en el servidor de informes  
Al ver un informe publicado en el Administrador de informes, podría ver un mensaje de error que represente un error de representación o procesamiento general. Para obtener más información, puede ver la pila de llamadas.   
  
Para ver la pila de llamadas, inicie sesión en el servidor de informes con las credenciales de administrador local, haga clic con el botón derecho en la página del Administrador de informes y haga clic en **Ver código fuente**. La pila de llamadas proporciona el contexto detallado del mensaje de error.  
  
## <a name="use-includessmanstudiofullincludesssmanstudiofullmd-to-verify-queries-and-credentials"></a>Uso de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] para comprobar las consultas y credenciales  
Puede utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull.md)] para validar las consultas complejas antes de incluirlas en un informe.   
  
Para más información, consulte [Editor de consultas del motor de base de datos](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md) y [Administrar objetos mediante el Explorador de objetos](~/ssms/object/manage-objects-by-using-object-explorer.md).  
  
## <a name="analyze-problem-reports-with-report-data-cached-on-the-client"></a>Análisis de informes del problema con los datos de informes almacenados en la memoria caché del cliente  
Cuando el autor de un informe lo crea en Business Intelligence Development Studio, el cliente de creación almacena en memoria caché los datos en forma de archivo .rdl.data, que se utiliza al obtener la vista previa de un informe. Cada vez que la consulta cambia, la memoria caché se actualiza. Para depurar los problemas del informe, a veces resulta útil evitar la actualización de los datos del informe para que no cambien mientras lleva a cabo la depuración.   
  
Para controlar si [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull.md)] solamente puede utilizar los datos de la memoria caché, agregue la sección siguiente al archivo devenv.exe.config en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio.md)]. La ubicación del directorio predeterminado es: `<drive>:Program Files\Microsoft Visual Studio 10.0\Common7\IDE`.   
  
```  
<system.diagnostics>  
      <switches>  
         <add name="Microsoft.ReportDesigner.ReportPreviewStore.ForceCache" value="1" />  
      </switches>  
   </system.diagnostics>  
```  
Siempre que el valor esté establecido en 1, solo se utilizan los datos del informe almacenado en memoria caché. Asegúrese de quitar esta sección cuando termine de depurar el informe.  
  
## <a name="see-also"></a>Vea también  
[Errores y eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]



