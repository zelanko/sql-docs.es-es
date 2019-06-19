---
title: Tarea Monitor de eventos WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.wmieventwatchertask.f1
- sql13.dts.designer.wmieventwatcher.general.f1
- sql13.dts.designer.wmieventwatcher.wmiquery.f1
helpviewer_keywords:
- WQL [Integration Services]
- WMI Event Watcher task [Integration Services]
ms.assetid: b5bb52e9-a77e-41e1-93f9-d4c3bc6b2c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9941fcae545bdf641ff024b3884970b90e23350e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65727322"
---
# <a name="wmi-event-watcher-task"></a>Tarea Monitor de eventos WMI

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Monitor de eventos WMI supervisa un evento de Instrumental de administración de Windows (WMI) mediante una consulta de evento de Lenguaje de consulta de Instrumental de administración (WQL) para especificar los eventos de interés. Puede usar la tarea Monitor de eventos WMI para los siguientes fines:  
  
-   Esperar la notificación de que se han agregado archivos a una carpeta y luego iniciar el procesamiento del archivo.  
  
-   Ejecutar un paquete que elimine archivos cuando la memoria disponible en un servidor alcance un porcentaje inferior al especificado.  
  
-   Controlar la instalación de una aplicación y luego ejecutar un paquete que usa la aplicación.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye una tarea que lee información de WMI.  
  
 Para obtener más información sobre esta tarea, haga clic en el tema siguiente:  
  
-   [Tarea Lector de datos WMI](../../integration-services/control-flow/wmi-data-reader-task.md)  
  
## <a name="wql-queries"></a>Consultas WQL  
 WQL es un dialecto de SQL con extensiones para admitir la notificación de eventos de WMI y otras características específicas de WMI. Para obtener más información sobre WQL, vea la documentación sobre Instrumental de administración de Windows en [MSDN Library](https://go.microsoft.com/fwlink/?linkid=62553).  
  
> [!NOTE]  
>  Las clases de WMI varían en las diferentes versiones de Windows.  
  
 La siguiente consulta supervisa la notificación de que el uso de la CPU supera el 40 por ciento.  
  
```  
SELECT * from __InstanceModificationEvent WITHIN 2 WHERE TargetInstance ISA 'Win32_Processor' and TargetInstance.LoadPercentage > 40  
```  
  
 La siguiente consulta detecta la notificación de que se ha agregado un archivo a una carpeta.  
  
```  
SELECT * FROM __InstanceCreationEvent WITHIN 10 WHERE TargetInstance ISA "CIM_DirectoryContainsFile" and TargetInstance.GroupComponent= "Win32_Directory.Name=\"c:\\\\WMIFileWatcher\""   
```  
  
## <a name="custom-logging-messages-available-on-the-wmi-event-watcher-task"></a>Mensajes de registro personalizados disponibles en la tarea Monitor de eventos WMI  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Monitor de eventos WMI. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|Indica que ocurrió un evento que supervisaba la tarea.|  
|**WMIEventWatcherTimedout**|Indica que se superó el tiempo de espera de la tarea.|  
|**WMIEventWatcherWatchingForWMIEvents**|Indica que la tarea inició la ejecución de la consulta WQL. La entrada incluye la consulta.|  
  
## <a name="configuration-of-the-wmi-event-watcher-task"></a>Configuración de la tarea Monitor de eventos WMI  
 Puede configurar la tarea Lector de datos WMI de las maneras siguientes:  
  
-   Especificar el administrador de conexiones WMI que se debe usar.  
  
-   Especificar el origen de la consulta WQL. El origen puede ser externo con respecto a la tarea, una variable o un archivo, o la consulta se puede almacenar en una propiedad de tarea.  
  
-   Especificar la acción realizada por la tarea cuando se produce el evento WMI. Puede registrar la notificación de eventos y el estado después del evento, o activar eventos personalizados de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que proporcionen información asociada con el evento WMI, la notificación y el estado después del evento.  
  
-   Definir de qué manera la tarea responde ante el evento. La tarea se puede configurar para realizarse correctamente o generar un error, según el evento, o la tarea puede supervisar el evento nuevamente.  
  
-   Especificar la acción realizada por la tarea cuando se agota el tiempo de espera de la consulta WMI. Puede registrar el tiempo de espera y el estado después del tiempo de espera, o activar un evento personalizado de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que indique que se agotó el tiempo de espera del evento WMI y que registre el tiempo de espera y el estado del tiempo de espera.  
  
-   Definir de qué manera la tarea responde ante el tiempo de espera. La tarea se puede configurar para realizarse correctamente o presentar un error, o la tarea puede detectar el evento nuevamente.  
  
-   Especificar la cantidad de veces que la tarea supervisa el evento.  
  
-   Especificar el tiempo de espera.  
  
 Si el origen es un archivo, la tarea Monitor de eventos WMI usa un administrador de conexiones de archivos para conectarse al archivo. Para más información, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 La tarea Monitor de eventos WMI usa un administrador de conexiones WMI para conectarse al servidor desde el cual lee la información de WMI. Para más información, consulte [WMI Connection Manager](../../integration-services/connection-manager/wmi-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-wmi-event-watcher-task"></a>Configuración mediante programación de la tarea Monitor de eventos WMI  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WmiEventWatcherTask.WmiEventWatcherTask>  
  
## <a name="wmi-event-watcher-task-editor-general-page"></a>Editor de la tarea Monitor de eventos WMI (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Monitor de eventos WMI** para asignar un nombre a la tarea Monitor de eventos WMI y describirla.  
  
 Para más información sobre el lenguaje de consulta de WMI (WQL), vea el tema sobre Instrumental de administración de Windows, [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)(Realizar consultas con WQL), en MSDN Library.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la tarea Monitor de eventos WMI. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Monitor de eventos WMI.  
  
## <a name="wmi-event-watcher-task-editor-wmi-options-page"></a>Editor de la tarea Monitor de eventos WMI (página Opciones WMI)
  Use la página **Opciones WMI** del cuadro de diálogo **Editor de la tarea Monitor de eventos WMI** para especificar el origen de la consulta WQL (Lenguaje de consulta de Instrumental de administración de Windows) y la manera en que la tarea Monitor de eventos WMI responde a los eventos WMI (Instrumentación de Microsoft Windows).  
  
 Para más información sobre el lenguaje de consulta de WMI (WQL), vea el tema sobre Instrumental de administración de Windows, [Querying with WQL](https://go.microsoft.com/fwlink/?LinkId=79045)(Realizar consultas con WQL), en MSDN Library.  
  
### <a name="static-options"></a>Opciones estáticas  
 **WMIConnectionName**  
 Seleccione un administrador de conexiones WMI de la lista, o bien haga clic en \<**Nueva conexión WMI…** > para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager.md), [Editor del administrador de conexiones WMI](../../integration-services/connection-manager/wmi-connection-manager-editor.md)  
  
 **WQLQuerySourceType**  
 Seleccione el tipo de origen de la consulta WQL que ejecuta la tarea. Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen en una consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
|**Conexión de archivos**|Seleccione el archivo que contiene la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
|**Variable**|Establezca el origen en una variable que defina la consulta WQL. Al seleccionar este valor se muestra la opción dinámica **WQLQuerySource**.|  
  
 **ActionAtEvent**  
 Especifique si el evento WMI registra el evento e inicia una acción de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o si solamente registra el evento.  
  
 **AfterEvent**  
 Especifique si la tarea se realiza correctamente o se produce un error después de recibir el evento WMI, o si la tarea continúa inspeccionando si el evento se vuelve a producir.  
  
 **ActionAtTimeout**  
 Especifique si la tarea registra un tiempo de espera de consulta WMI e inicia un evento de [!INCLUDE[ssIS](../../includes/ssis-md.md)] como respuesta o si solamente registra el tiempo de espera.  
  
 **AfterTimeout**  
 Especifique si la tarea se realiza correctamente o se produce un error en respuesta a un tiempo de espera, o si la tarea continúa inspeccionando si se vuelve a producir otro tiempo de espera.  
  
 **NumberOfEvents**  
 Especifique el número de eventos a inspeccionar.  
  
 **Timeout**  
 Especifique el número de segundos que se debe esperar a que el evento ocurra. Un valor de 0 significa que no rige ningún tiempo de espera.  
  
### <a name="wqlquerysource-dynamic-options"></a>Opciones dinámicas de WQLQuerySource  
  
#### <a name="wqlquerysource--direct-input"></a>WQLQuerySource = Entrada directa  
 **WQLQuerySource**  
 Proporcione una consulta, o bien haga clic en el botón de puntos suspensivos (…) y escriba una consulta con el cuadro de diálogo **Consulta WQL**.  
  
#### <a name="wqlquerysource--file-connection"></a>WQLQuerySource = Conexión de archivos  
 **WQLQuerySource**  
 Seleccione un administrador de conexiones de archivos de la lista, o bien haga clic en \<**Nueva conexión…** > para crear un administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="wqlquerysource--variable"></a>WQLQuerySource = Variable  
 **WQLQuerySource**  
 Seleccione una variable de la lista o haga clic en \<**Nueva variable…** > para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Agregar variable](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
