---
title: Supervisar Analysis Services con SQL Server extendida Events | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- XEvents
- Sql13.ssms.XeASNewEventSession.General.f1
- Sql13.ssms.XeASNewEventSession.Events.f1
- Sql13.ssms.XeASNewEventSession.Targets.f1
- Sql13.ssms.XeASNewEventSession.Advanced.f1
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cec6da660c202dfde5a1169dd34397fca5c51207
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>Supervisar Analysis Services con SQL Server Extended Events
  Eventos extendidos (*xEvents*) es un sistema ligero de supervisión de seguimiento y rendimiento que usa muy pocos recursos del sistema, lo que lo convierte en una herramienta ideal para diagnosticar problemas tanto en los servidores de producción como en los de prueba. También es altamente escalable, configurable y, en SQL Server 2016, más fácil de usar gracias a la nueva compatibilidad de herramienta integrada. En SQL Server Management Studio, en las conexiones con instancias de Analysis Services, puede configurar, ejecutar y supervisar un seguimiento activo, algo parecido al uso de SQL Server Profiler. La adición de mejores herramientas debería convertir a xEvents en un reemplazo más razonable para SQL Server Profiler y crea más simetría en la forma de diagnosticar problemas en el motor de base de datos y las cargas de trabajo de Analysis Services.  
  
 Además de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], también puede configurar sesiones de Eventos extendidos para  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la manera antigua, por medio de scripting XMLA, como se hacía en las versiones anteriores.  
  
 Todos los eventos de Analysis Services se pueden capturar y destinar a usuarios específicos, según se define en [Eventos extendidos](../../relational-databases/extended-events/extended-events.md).  
  
> [!NOTE]  
>  Vea esta [breve presentación de vídeo](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) o lea la [entrada de blog complementaria](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) para obtener más información sobre xEvents para Analysis Services en SQL Server 2016.  
  
##  <a name="bkmk_top"></a> En este tema  
  
-   [Usar Management Studio para configurar Analysis Services](#bkmk_ssas_extended_events_ssms)  
  
-   [Script XMLA para iniciar Extended Events en Analysis Services](#bkmk_script_start)  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> Usar Management Studio para configurar Analysis Services  
 En las instancias tabulares y multidimensionales, Management Studio proporciona una nueva carpeta de administración que contiene sesiones de xEvents iniciadas por el usuario. Puede ejecutar varias sesiones a la vez. Sin embargo, en la implementación actual, la interfaz de usuario de Eventos extendidos para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no admite la actualización ni la reproducción de una sesión existente.  
  
 ![ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "ssas_extended_events_ssms_start")  
  
 **Seleccionar eventos**  
  
 Si ya sabe qué eventos desea capturar, buscarlos es la manera más fácil de agregarlos al seguimiento. De lo contrario, los eventos siguientes se usan habitualmente para supervisar operaciones:  
  
-   **CommandBegin** y **CommandEnd**.  
  
-   **QueryBegin**, **QueryEnd**y **QuerySubcubeVerbose** (muestra la consulta MDX o DAX completa enviada al servidor), además de **ResourceUsage** para estadísticas sobre recursos usados por la consulta y el número de filas devueltas.  
  
-   **ProgressReportBegin** y **ProgressReportEnd** (para operaciones de procesamiento).  
  
-   **AuditLogin** y **AuditLogout** (captura la identidad del usuario con la que una aplicación cliente se conecta a Analysis Services).  
  
 **Seleccionar el almacenamiento de datos**  
  
 Una sesión se puede transmitir en directo a una ventana de Management Studio o guardarse en un archivo para su análisis posterior mediante Power Query o Excel.  
  
-   **event_file** almacena datos de sesión en un archivo .xel.  
  
-   **event_stream** habilita la opción **Observar datos en directo** de Management Studio.  
  
-   **ring_buffer** almacena datos de sesión en memoria mientras el servidor se esté ejecutando. Al reiniciar el servidor, los datos de sesión se descartan.  
  
 **Agregar campos de evento**  
  
 Asegúrese de configurar la sesión de modo que incluya campos de evento para poder ver fácilmente la información interesante.  
  
 **Configurar** es una opción del extremo del cuadro de diálogo.  
  
 ![configurar SSAS-xevents](../../analysis-services/instances/media/ssas-xevents-configure.PNG "ssas-xevents-configurar")  
  
 En Configuración, en la pestaña Campos de evento, seleccione **TextData** para que este campo aparezca junto al evento y muestre los valores devueltos, incluidas las consultas que se están ejecutando en el servidor.  
  
 Después de configurar una sesión para los eventos deseados y el almacenamiento de datos, puede hacer clic en el botón Script para enviar la configuración a uno de los destinos admitidos, que incluye un archivo, una nueva consulta en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y el Portapapeles.  
  
 **Actualizar sesiones**  
  
 Una vez creada la sesión, asegúrese de actualizar la carpeta Sesiones de Management Studio para ver la sesión que acaba de crear. Si configuró un event_stream, puede hacer clic con el botón derecho en el nombre de la sesión y seleccionar **Observar datos en directo** para supervisar la actividad del servidor en tiempo real.  
  
##  <a name="bkmk_script_start"></a> Script XMLA para iniciar Extended Events en Analysis Services  
 El seguimiento de Eventos extendidos se habilita mediante un comando de script de objeto de creación XMLA similar como se muestra a continuación:  
  
```  
<Execute …>  
   <Command>  
      <Batch …>  
         <Create …>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session …>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" …/>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 Donde el usuario definirá los siguientes elementos, según las necesidades del seguimiento:  
  
 *trace_id*  
 Define el identificador único de este seguimiento.  
  
 *trace_name*  
 El nombre proporcionado a este seguimiento; normalmente una definición legible del mismo. Es una práctica común usar el valor de *trace_id* como nombre.  
  
 *AS_event*  
 El evento de Analysis Services que se expondrá. Consulte [Eventos de seguimiento de Analysis Services](../../analysis-services/trace-events/analysis-services-trace-events.md) para ver los nombres de los eventos.  
  
 *data_filename*  
 El nombre del archivo de datos que contiene los datos de los eventos. Este nombre se añade como sufijo con una marca de tiempo para evitar sobrescribir los datos si el seguimiento se envía repetidamente.  
  
 *metadata_filename*  
 El nombre del archivo de datos que contiene los metadatos de los eventos. Este nombre se añade como sufijo con una marca de tiempo para evitar sobrescribir los datos si el seguimiento se envía repetidamente.  
  
||  
|-|  
|![Icono de flecha usado con Back vínculo al principio](../../analysis-services/instances/media/uparrow16x16.gif "icono de flecha usado con Back vínculo al principio") [en este tema](#bkmk_top)|  
  
##  <a name="bkmk_script_stop"></a> Script XMLA para detener Extended Events en Analysis Services  
 Para detener el objeto de seguimiento de Eventos extendidos, debe eliminar el objeto utilizando un comando de script de objeto de eliminación XMLA como se muestra a continuación:  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch …>  
         <Delete …>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 Donde el usuario definirá los siguientes elementos, según las necesidades del seguimiento:  
  
 *trace_id*  
 Define el identificador único para el seguimiento que se va a eliminar.  
  
||  
|-|  
|![Icono de flecha usado con Back vínculo al principio](../../analysis-services/instances/media/uparrow16x16.gif "icono de flecha usado con Back vínculo al principio") [en este tema](#bkmk_top)|  
  
## <a name="see-also"></a>Vea también  
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  

