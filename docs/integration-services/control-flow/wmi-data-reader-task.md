---
title: Tarea lector de datos WMI | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.wmidatareadertask.f1
- sql13.dts.designer.wmidatareadertask.general.f1
- sql13.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Data Reader task [Integration Services]
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8806c102eaec2c2540374bfaddc33b76d8f6e584
ms.openlocfilehash: 75beba806fea6d2e680720ef9c9c72b7809dbe70
ms.contentlocale: es-es
ms.lasthandoff: 08/11/2017

---
# <a name="wmi-data-reader-task"></a>Tarea Lector de datos WMI
  La tarea Lector de datos WMI ejecuta consultas mediante el Lenguaje de consulta del Instrumental de administración de Windows (WMI), que devuelve información de WMI sobre un sistema informático. Puede usar la tarea Lector de datos WMI para los siguientes fines:  
  
-   Realizar consultas de los registros de eventos de Windows en un equipo local o remoto y escribir la información en un archivo o variable.  
  
-   Obtener información sobre la presencia, estado o propiedades de componentes del hardware y usar posteriormente esta información para determinar si se deben ejecutar otras tareas en el flujo de control.  
  
-   Obtener una lista de las aplicaciones y determinar qué versión de cada aplicación está instalada.  
  
 Puede configurar la tarea Lector de datos WMI de las maneras siguientes:  
  
-   Especificar el administrador de conexiones WMI que se debe usar.  
  
-   Especificar el origen de la consulta WQL. La consulta se puede almacenar en una propiedad de tarea, o bien fuera de la tarea, en una variable o archivo.  
  
-   Definir el formato de los resultados de la consulta WQL. La tarea admite una tabla, par de nombre/valor de la propiedad o formato de valor de propiedad.  
  
-   Especificar el destino de la consulta. El destino puede ser una variable o un archivo.  
  
-   Indicar si el destino de la consulta se sobrescribe, se conserva o anexa.  
  
 Si el origen o destino es un archivo, la tarea Lector de datos WMI usa un administrador de conexiones de archivo para conectarse al archivo. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 La tarea Lector de datos WMI usa un administrador de conexiones WMI para conectarse al servidor desde el cual lee la información de WMI. Para más información, consulte [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
## <a name="wql-query"></a>WQL Query  
 WQL es un dialecto de SQL con extensiones para admitir la notificación de eventos de WMI y otras características específicas de WMI. Para obtener más información sobre WQL, vea la documentación sobre Instrumental de administración de Windows en [MSDN Library](http://go.microsoft.com/fwlink/?linkid=7022).  
  
> [!NOTE]  
>  Las clases de WMI varían en las diferentes versiones de Windows.  
  
 La siguiente consulta WQL devuelve entradas en el evento de registro de la aplicación.  
  
```  
SELECT * FROM Win32_NTLogEvent WHERE LogFile = 'Application' AND (SourceName='SQLISService' OR SourceName='SQLISPackage') AND TimeGenerated > '20050117'  
```  
  
 La siguiente consulta WQL devuelve información de disco lógica.  
  
```  
SELECT FreeSpace, DeviceId, Size, SystemName, Description FROM Win32_LlogicalDisk  
```  
  
 La siguiente consulta WQL devuelve una lista de las actualizaciones de Ingeniería de corrección rápida (QFE) al sistema operativo.  
  
```  
Select * FROM Win32_QuickFixEngineering  
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-data-reader-task"></a>Mensajes de registro personalizados disponibles en la tarea Lector de datos WMI  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Lector de datos WMI. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Indica que la tarea inició la lectura de datos WMI.|  
|**WMIDataReaderOperation**|Informa de la consulta WQL que ejecutó la tarea.|  
  
## <a name="configuration-of-the-wmi-data-reader-task"></a>Configuración de la tarea Lector de datos WMI  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="wmi-data-reader-task-editor-general-page"></a>Editor de la tarea Lector de datos WMI (página General)
  Utilice la página **General** del cuadro de diálogo **Editor de la tarea Lector de datos WMI** para asignar un nombre a la tarea Lector de datos WMI y describirla.  
  
  Para más información sobre el lenguaje de consulta de WMI (WQL), vea el tema sobre Instrumental de administración de Windows, [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(Realizar consultas con WQL), en MSDN Library.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la tarea Lector de datos WMI. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Description**  
 Escriba una descripción de la tarea Lector de datos WMI.  
  
## <a name="wmi-data-reader-task-editor-wmi-options-page"></a>Editor de la tarea Lector de datos WMI (página Opciones WMI)
  Use la página **Opciones WMI** del cuadro de diálogo **Editor de la tarea Lector de datos WMI** para especificar el origen de la consulta WQL (Lenguaje de consulta de Instrumental de administración de Windows) y el destino del resultado de la consulta.  
  
 Para más información sobre el lenguaje de consulta de WMI (WQL), vea el tema sobre Instrumental de administración de Windows, [Querying with WQL](http://go.microsoft.com/fwlink/?LinkId=79045)(Realizar consultas con WQL), en MSDN Library.  
  
### <a name="static-options"></a>Opciones estáticas  
 **WMIConnectionName**  
 Seleccione un administrador de conexión de WMI en la lista o haga clic en \< **nueva conexión de WMI...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados**: [Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md).  
  
 **WQLQuerySourceType**  
 Seleccione el tipo de origen de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen en una consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySourceType**.|  
|**Conexión de archivos**|Seleccione el archivo que contiene la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySourceType**.|  
|**Variable**|Establezca el origen en una variable que defina la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySourceType**.|  
  
 **OutputType**  
 Especifique si la salida debe ser una tabla de datos, un valor de propiedad o un valor y nombre de propiedad.  
  
 **OverwriteDestination**  
 Especifica si mantener, sobrescribir o anexar a los datos originales en el archivo de destino o variable.  
  
 **DestinationType**  
 Seleccione el tipo de destino de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Conexión de archivos**|Seleccione un archivo donde guardar los resultados de la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **DestinationType**.|  
|**Variable**|Establezca la variable donde almacenar los resultados de la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **DestinationType**.|  
  
### <a name="wqlquerysourcetype-dynamic-options"></a>Opciones dinámicas WQLQuerySourceType  
  
#### <a name="wqlquerysourcetype--direct-input"></a>WQLQuerySourceType = Entrada directa  
 **WQLQuerySource**  
 Proporcione una consulta o haga clic en los puntos suspensivos (…) y escriba una consulta mediante el cuadro de diálogo **Consulta WQL** .  
  
#### <a name="wqlquerysourcetype--file-connection"></a>WQLQuerySourceType = Conexión de archivos  
 **WQLQuerySource**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysourcetype--variable"></a>WQLQuerySourceType = Variable  
 **WQLQuerySource**  
 Seleccione una variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
### <a name="destinationtype-dynamic-options"></a>Opciones dinámicas DestinationType  
  
#### <a name="destinationtype--file-connection"></a>DestinationType = Conexión de archivos  
 **Destino**  
 Seleccione un administrador de conexión de archivos en la lista o haga clic en \< **nueva conexión...** > para crear una nueva conexión de administrador.  
  
 **Temas relacionados:** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="destinationtype--variable"></a>DestinationType = Variable  
 **Destino**  
 Seleccione una variable en la lista o haga clic en \< **nueva variable...** > para crear una nueva variable.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5).  
  
## <a name="see-also"></a>Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  

