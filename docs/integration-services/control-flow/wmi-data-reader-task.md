---
title: "Tarea Lector de datos WMI | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.wmidatareadertask.f1"
helpviewer_keywords: 
  - "XML [Integration Services]"
  - "Lector de datos WMI, tarea [Integration Services]"
ms.assetid: dae57067-0275-4ac3-8f34-1b9d169f1112
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# Tarea Lector de datos WMI
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
  
## WQL Query  
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
  
## Mensajes de registro personalizados disponibles en la tarea Lector de datos WMI  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Lector de datos WMI. Para más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md) y [Mensajes personalizados para registro](../../integration-services/performance/custom-messages-for-logging.md).  
  
|Entrada del registro|Description|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|Indica que la tarea inició la lectura de datos WMI.|  
|**WMIDataReaderOperation**|Informa de la consulta WQL que ejecutó la tarea.|  
  
## Configuración de la tarea Lector de datos WMI  
 Puede establecer propiedades mediante programación o a través del Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obtener información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Lector de datos WMI &#40;página Opciones WMI&#41;](../../integration-services/control-flow/wmi-data-reader-task-editor-wmi-options-page.md)  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiDataReaderTask.WmiDataReaderTask>  
  
## Tareas relacionadas  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## Vea también  
 [Tareas de Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Flujo de control](../../integration-services/control-flow/control-flow.md)  
  
  