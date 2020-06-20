---
title: Mensajes personalizados para el registro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], custom
- writing log entries
- SSIS packages, logs
- custom messages for logging [Integration Services]
ms.assetid: 3c74bba9-02b7-4bf5-bad5-19278b680730
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a7fe7d714d93915814b6658409a9f892c28e03b7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917155"
---
# <a name="custom-messages-for-logging"></a>Mensajes personalizados para registro
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona a un amplio conjunto de eventos personalizados para escribir entradas del registro para paquetes y muchas tareas. Puede utilizar estas entradas para guardar información detallada sobre el progreso, resultados y problemas de ejecución al registrar eventos predefinidos o mensajes definidos por el usuario para su análisis posterior. Por ejemplo, puede registrar cuando se inicia y finaliza la inserción masiva para identificar los problemas de rendimiento en la ejecución del paquete.  
  
 Las entradas del registro personalizadas pertenecen a un conjunto de entradas diferente de los eventos estándar de registro que están disponibles para los paquetes y todos los contenedores y tareas. Las entradas del registro personalizadas se han adaptado para capturar información de utilidad sobre una tarea específica de un paquete. Por ejemplo, una de las entradas de registro personalizadas para la tarea Ejecutar SQL registra la instrucción SQL que ejecuta la tarea en el registro.  
  
 Todas las entradas del registro incluyen información de fecha y hora, incluidas las entradas del registro que se escriben automáticamente cuando se inicia o finaliza un paquete. Muchos de los eventos de registro escriben varias entradas en el registro. Esto ocurre generalmente cuando los eventos tienen diferentes fases. Por ejemplo, el evento de registro `ExecuteSQLExecutingQuery` escribe tres entradas: una entrada después de que la tarea adquiere una conexión con la base de datos, otra después de que la tarea comienza a preparar la instrucción SQL y otra más una vez que se completa la ejecución de la instrucción SQL.  
  
 Los siguientes objetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] poseen entradas del registro personalizadas:  
  
 [Paquete](#Package)  
  
 [Tarea Inserción masiva](#BulkInsert)  
  
 [Tarea Flujo de datos](#DataFlow)  
  
 [Tarea Ejecutar DTS 2000](#ExecuteDTS200)  
  
 [Tarea Ejecutar proceso](#ExecuteProcess)  
  
 [Tarea Ejecutar SQL](#ExecuteSQL)  
  
 [Tarea Sistema de archivos](#FileSystem)  
  
 [Tarea FTP](#FTP)  
  
 [Tarea Cola de mensajes](#MessageQueue)  
  
 [Tarea Script](#Script)  
  
 [Tarea Enviar correo](#SendMail)  
  
 [Tarea Transferir bases de datos](#TransferDatabase)  
  
 [Tarea Transferir mensajes de error](#TransferErrorMessages)  
  
 [Tarea Transferir trabajos](#TransferJobs)  
  
 [Tarea Transferir inicios de sesión](#TransferLogins)  
  
 [Tarea Transferir procedimientos almacenados principales](#TransferMasterStoredProcedures)  
  
 [Tarea Transferir objetos de SQL Server](#TransferSQLServerObjects)  
  
 [Tarea Servicios web](#WebServices)  
  
 [Tarea Lector de datos WMI](#WMIDataReader)  
  
 [Tarea Monitor de eventos WMI](#WMIEventWatcher)  
  
 [Tarea XML](#XML)  
  
## <a name="log-entries"></a>Entradas del registro  
  
###  <a name="package"></a><a name="Package"></a>Configura  
 La siguiente tabla contiene las entradas del registro personalizadas para paquetes.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`PackageStart`|Indica que se inició la ejecución del paquete.<br /><br /> Nota: Esta entrada del registro se escribe automáticamente en el registro. No se puede excluir.|  
|`PackageEnd`|Indica que finalizó la ejecución del paquete.<br /><br /> Nota: Esta entrada del registro se escribe automáticamente en el registro. No se puede excluir.|  
|`Diagnostic`|Proporciona información sobre la configuración del sistema que afecta a la ejecución de paquetes, como el número de ejecutables que se pueden ejecutar simultáneamente.<br /><br /> La entrada del registro `Diagnostic` también incluye entradas por delante y por detrás relativas a las llamadas a proveedores de datos externos. Para obtener más información, consulte [Troubleshooting Tools Package Connectivity](troubleshooting/troubleshooting-tools-for-package-connectivity.md).|  
  
###  <a name="bulk-insert-task"></a><a name="BulkInsert"></a>Tarea inserción masiva  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Inserción masiva.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`DTSBulkInsertTaskBegin`|Indica que se inició la inserción masiva.|  
|`DTSBulkInsertTaskEnd`|Indica que finalizó la inserción masiva.|  
|`DTSBulkInsertTaskInfos`|Proporciona información descriptiva sobre la tarea.|  
  
###  <a name="data-flow-task"></a><a name="DataFlow"></a>Tarea flujo de datos  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Flujo de datos.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`BufferSizeTuning`|Indica que la tarea Flujo de datos cambió el tamaño del búfer. En la entrada del registro se describen las razones del cambio de tamaño y se indica el nuevo tamaño temporal del búfer.|  
|`OnPipelinePostEndOfRowset`|Indica que se ha dado la señal de fin del conjunto de filas a un componente, la cual se establece a través de la última llamada del método `ProcessInput`. Se escribe una entrada por cada componente del flujo de datos que procesa la entrada de datos. La entrada incluye el nombre del componente.|  
|`OnPipelinePostPrimeOutput`|Indica que el componente ha completado su última llamada al método `PrimeOutput`. En función del flujo de datos, es posible que se escriban varias entradas. Si el componente es un origen, esto significa que el componente ha terminado de procesar filas.|  
|`OnPipelinePreEndOfRowset`|Indica que un componente está a punto de recibir la señal de fin del conjunto de filas, la cual se establece a través de la última llamada del método `ProcessInput`. Se escribe una entrada por cada componente del flujo de datos que procesa la entrada de datos. La entrada incluye el nombre del componente.|  
|`OnPipelinePrePrimeOutput`|Indica que el componente está a punto de recibir su última llamada del método `PrimeOutput`. En función del flujo de datos, es posible que se escriban varias entradas.|  
|`OnPipelineRowsSent`|Informa del número de filas que se proporciona a una entrada de componentes a través de una llamada al método `ProcessInput`. La entrada del registro incluye el nombre del componente.|  
|`PipelineBufferLeak`|Proporciona información sobre cualquier componente que mantuvo la conexión de los búferes después de que desapareciera el administrador de búferes. Esto significa que no se liberaron los recursos de los búferes y podría ocasionar pérdidas de memoria. La entrada del registro proporciona el nombre del componente y el Id. del búfer.|  
|`PipelineExecutionPlan`|Informa del plan de ejecución del flujo de datos. Proporciona información sobre cómo se van a enviar los búferes a los componentes. Esta información, junto con la entrada PipelineExecutionTrees, explica lo que ocurre en la tarea.|  
|`PipelineExecutionTrees`|Informa sobre los árboles de ejecución del diseño del flujo de datos. El programador del motor de flujo de datos utiliza los árboles para generar el plan de ejecución del flujo de datos.|  
|`PipelineInitialization`|Proporciona información de inicialización sobre la tarea. Esta información incluye los directorios que se utilizan para el almacenamiento temporal de datos BLOB, el tamaño predeterminado del búfer y la cantidad de filas de un búfer. En función de la configuración de la tarea Flujo de datos, es posible que se escriban varias entradas.|  
  
###  <a name="execute-dts-2000-task"></a><a name="ExecuteDTS200"></a>Tarea ejecutar DTS 2000  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Ejecutar DTS 2000.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`ExecuteDTS80PackageTaskBegin`|Indica que la tarea inició la ejecución del paquete DTS 2000.|  
|`ExecuteDTS80PackageTaskEnd`|Indica que finalizó la tarea.<br /><br /> Nota: Es posible que el paquete DTS 2000 continúe ejecutándose una vez finalizada la tarea.|  
|`ExecuteDTS80PackageTaskTaskInfo`|Proporciona información descriptiva sobre la tarea.|  
|`ExecuteDTS80PackageTaskTaskResult`|Informa del resultado de la ejecución del paquete DTS 2000 que ejecutó la tarea.|  
  
###  <a name="execute-process-task"></a><a name="ExecuteProcess"></a>Tarea ejecutar proceso  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Ejecutar proceso.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`ExecuteProcessExecutingProcess`|Proporciona información sobre el proceso de ejecución del ejecutable que se configuró para que ejecute la tarea.<br /><br /> Se escriben dos entradas del registro. Una entrada contiene información sobre el nombre y la ubicación del ejecutable que ejecuta la tarea y la otra entrada registra la salida del ejecutable.|  
|`ExecuteProcessVariableRouting`|Proporciona información acerca de las variables que se enrutan a la entrada y las salidas del ejecutable. Se escriben entradas del registro para stdin (la entrada), stdout (la salida) y stderr (la salida de errores).|  
  
###  <a name="execute-sql-task"></a><a name="ExecuteSQL"></a>Tarea ejecutar SQL  
 La siguiente tabla contiene la entrada del registro personalizada para la tarea Ejecutar SQL.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|Proporciona información sobre las fases de ejecución de la instrucción SQL. Las entradas de registro se escriben cuando la tarea adquiere una conexión con la base de datos, cuando la tarea comienza a preparar la instrucción SQL y una vez que se completa la ejecución de la instrucción SQL. La entrada del registro para la fase de preparación incluye la instrucción SQL que utiliza la tarea.|  
  
###  <a name="file-system-task"></a><a name="FileSystem"></a>Tarea sistema de archivos  
 La siguiente tabla contiene las entradas de registro personalizadas para la tarea Sistema de archivos.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`FileSystemOperation`|Informa sobre la operación que realiza la tarea. La entrada del registro se escribe cuando se inicia la operación del sistema de archivos e incluye información sobre el origen y el destino.|  
  
###  <a name="ftp-task"></a><a name="FTP"></a>Tarea FTP  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea FTP.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`FTPConnectingToServer`|Indica que la tarea inició una conexión con el servidor FTP.|  
|`FTPOperation`|Informa del comienzo y del tipo de operación de FTP que realiza la tarea.|  
  
###  <a name="message-queue-task"></a><a name="MessageQueue"></a>Tarea cola de mensajes  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Cola de mensajes.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`MSMQAfterOpen`|Indica que la tarea finalizó la apertura de la cola de mensajes.|  
|`MSMQBeforeOpen`|Indica que la tarea inició la apertura de la cola de mensajes.|  
|`MSMQBeginReceive`|Indica que la tarea comenzó a recibir un mensaje.|  
|`MSMQBeginSend`|Indica que la tarea comenzó a enviar un mensaje.|  
|`MSMQEndReceive`|Indica que la tarea finalizó la recepción de un mensaje.|  
|`MSMQEndSend`|Indica que la tarea finalizó el envío de un mensaje.|  
|`MSMQTaskInfo`|Proporciona información descriptiva sobre la tarea.|  
|`MSMQTaskTimeOut`|Indica que se superó el tiempo de espera de la tarea.|  
  
###  <a name="script-task"></a><a name="Script"></a>Tarea script  
 La siguiente tabla contiene la entrada personalizada de registro para la tarea Script.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|Informa sobre los resultados de la implementación del registro en el script. Se escribe una entrada de registro para cada llamada al método `Log` del objeto `Dts`. La entrada se escribe cuando se ejecuta el código. Para más información, consulte [Logging in the Script Task](extending-packages-scripting/task/logging-in-the-script-task.md).|  
  
###  <a name="send-mail-task"></a><a name="SendMail"></a>Tarea enviar correo  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Enviar correo.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`SendMailTaskBegin`|Indica que la tarea comenzó a enviar un mensaje de correo electrónico.|  
|`SendMailTaskEnd`|Indica que la tarea finalizó el envío de un mensaje de correo electrónico.|  
|`SendMailTaskInfo`|Proporciona información descriptiva sobre la tarea.|  
  
###  <a name="transfer-database-task"></a><a name="TransferDatabase"></a>Tarea transferir bases de datos  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Transferir bases de datos.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`SourceDB`|Especifica la base de datos que copió la tarea.|  
|`SourceSQLServer`|Especifica el equipo desde el que se copió la base de datos.|  
  
###  <a name="transfer-error-messages-task"></a><a name="TransferErrorMessages"></a>Tarea transferir mensajes de error  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Transferir mensajes de error.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`TransferErrorMessagesTaskFinishedTransferringObjects`|Indica que la tarea finalizó la transferencia de los mensajes de error.|  
|`TransferErrorMessagesTaskStartTransferringObjects`|Indica que la tarea inició la transferencia de los mensajes de error.|  
  
###  <a name="transfer-jobs-task"></a><a name="TransferJobs"></a>Tarea transferir trabajos  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Transferir trabajos.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`TransferJobsTaskFinishedTransferringObjects`|Indica que la tarea finalizó la transferencia de los trabajos del Agente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|`TransferJobsTaskStartTransferringObjects`|Indica que la tarea inició la transferencia de los trabajos del Agente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
  
###  <a name="transfer-logins-task"></a><a name="TransferLogins"></a>Tarea transferir inicios de sesión  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Transferir inicios de sesión.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`TransferLoginsTaskFinishedTransferringObjects`|Indica que la tarea finalizó la transferencia de inicios de sesión.|  
|`TransferLoginsTaskStartTransferringObjects`|Indica que la tarea inició la transferencia de los inicios de sesión.|  
  
###  <a name="transfer-master-stored-procedures-task"></a><a name="TransferMasterStoredProcedures"></a>Tarea transferir procedimientos almacenados principales  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Transferir procedimientos almacenados principales.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`TransferStoredProceduresTaskFinishedTransferringObjects`|Indica que la tarea finalizó la transferencia de los procedimientos almacenados definidos por el usuario que están almacenados en la base de datos **maestra** .|  
|`TransferStoredProceduresTaskStartTransferringObjects`|Indica que la tarea inició la transferencia de los procedimientos almacenados definidos por el usuario que están almacenados en la base de datos **maestra** .|  
  
###  <a name="transfer-sql-server-objects-task"></a><a name="TransferSQLServerObjects"></a>Tarea transferir objetos SQL Server  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Transferir objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`TransferSqlServerObjectsTaskFinishedTransferringObjects`|Indica que la tarea finalizó la transferencia de los objetos de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|`TransferSqlServerObjectsTaskStartTransferringObjects`|Indica que la tarea inició la transferencia de los objetos de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
  
###  <a name="web-services-task"></a><a name="WebServices"></a>Tarea servicios Web  
 La siguiente tabla contiene las entradas del registro personalizadas que puede habilitar para la tarea Servicios web.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`WSTaskBegin`|La tarea inició el acceso a un servicio web.|  
|`WSTaskEnd`|La tarea completó un método de servicio web.|  
|`WSTaskInfo`|Información descriptiva acerca de la tarea.|  
  
###  <a name="wmi-data-reader-task"></a><a name="WMIDataReader"></a>Tarea lector de datos WMI  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Lector de datos WMI.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`WMIDataReaderGettingWMIData`|Indica que la tarea inició la lectura de datos WMI.|  
|`WMIDataReaderOperation`|Informa de la consulta WQL que ejecutó la tarea.|  
  
###  <a name="wmi-event-watcher-task"></a><a name="WMIEventWatcher"></a>Tarea monitor de eventos WMI  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea Monitor de eventos WMI.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`WMIEventWatcherEventOccurred`|Indica que ocurrió el evento que supervisaba la tarea.|  
|`WMIEventWatcherTimedout`|Indica que se superó el tiempo de espera de la tarea.|  
|`WMIEventWatcherWatchingForWMIEvents`|Indica que la tarea inició la ejecución de la consulta WQL. La entrada incluye la consulta.|  
  
###  <a name="xml-task"></a><a name="XML"></a>Tarea XML  
 La siguiente tabla contiene las entradas del registro personalizadas para la tarea XML.  
  
|Entrada del registro|Descripción|  
|---------------|-----------------|  
|`XMLOperation`|Proporciona información sobre la operación que la tarea realiza.|   
  
## <a name="see-also"></a>Consulte también  
 [Registro de Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
