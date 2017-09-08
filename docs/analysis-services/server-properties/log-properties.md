---
title: Propiedades de registro | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- QueryLogFileSize property
- QueryLogTableName property
- TraceBackgroundDistributionPeriod property
- TraceMaxRowsetSize property
- NullKeyConvertedToUnknown property
- CrashReportsFolder property
- TraceDefinitionFile property
- SQLDumperFlagsOn property
- KeyErrorLimit property
- SnapshotDefinitionFile property
- MinidumpErrorList property
- ErrorLogFileName property
- KeyDuplicate property
- IgnoreDataTruncation property
- logs [Analysis Services]
- Enabled property
- FileSizeMB property
- TraceFileWriteTrailerPeriod property
- TraceQueryResponseTextChunkSize property
- File property
- FileBufferSize property
- TraceRowsetBackgroundFlushPeriod property
- ErrorLogFileSize property
- TraceRequestParameters property
- KeyErrorLimitAction property
- CreateQueryLogTable property
- LogDir property
- TraceBackgroundFlushPeriod property
- TraceFileBufferSize property
- SQLDumperFlagsOff property
- QueryLogConnectionString property
- KeyNotFound property
- KeyErrorLogFile property
- TraceReportFQDN property
- KeyErrorAction property
- QueryLogFileName property
- MessageLogs property
- MiniDumpFlagsOn property
- SnapshotFrequencySec property
- QueryLogSampling property
- CreateAndSendCrashReports property
- LogDurationSec property
ms.assetid: 33fd90ee-cead-48f0-8ff9-9b458994c766
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 72e9b5094c12d014c361875016b8208264ad2860
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="log-properties"></a>Propiedades de registro
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor de registro descritas en las siguientes tablas. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
## <a name="general"></a>General  
 **Archivo**  
 Una propiedad de cadena que identifica el nombre del archivo de registro del servidor. Esta propiedad solo se aplica cuando se utiliza un archivo de disco para realizar el registro, a diferencia de cuando se utiliza una tabla de base de datos (comportamiento predeterminado).  
  
 El valor predeterminado de esta propiedad es msmdsrv.log.  
  
 **FileBufferSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MessageLogs**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="error-log"></a>Registro de errores  
 Puede establecer estas propiedades en la instancia de servidor level para modificar los valores predeterminados de Configuración de errores que aparecen en otras herramientas y diseñadores. Vea [configuración de errores de cubo, partición y procesamiento de dimensiones &#40; SSAS - Multidimensional &#41; ](../../analysis-services/multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md) y <xref:Microsoft.AnalysisServices.MiningStructure.ErrorConfiguration%2A> para obtener más información.  
  
 **ErrorLog\ErrorLogFileName**  
 Una propiedad utilizada como valor predeterminado durante la operación de procesamiento realizada por el servidor.  
  
 **ErrorLog\ErrorLogFileSize**  
 Una propiedad utilizada como valor predeterminado durante la operación de procesamiento realizada por el servidor.  
  
 **ErrorLog\KeyErrorAction**  
 Especifica la acción que realiza el servidor cuando se produce un error de **KeyNotFound** . Entre las respuestas válidas a este error se incluyen:  
  
-   **ConvertToUnknown** indica al servidor que asigne el valor de clave de error al miembro desconocido.  
  
-   **DiscardRecord** indica al servidor que excluya el registro.  
  
 **ErrorLog\KeyErrorLogFile**  
 Es un nombre de archivo definido por el usuario que debe tener una extensión de archivo .log, situado en una carpeta para la que la cuenta de servicio tiene permisos de lectura y escritura. Este archivo de registro solo contendrá errores generados durante el procesamiento. Use la Caja negra si necesita información más detallada.  
  
 **ErrorLog\KeyErrorLimit**  
 Es el número máximo de errores de integridad de datos que el servidor permitirá antes de que se produzca un error de procesamiento. Un valor de -1 indica que no hay ningún límite. El valor predeterminado es 0, lo que significa que el procesamiento se detiene después de producirse el primer error. También puede establecerlo en un número entero.  
  
 **ErrorLog\KeyErrorLimitAction**  
 Especifica la acción que realiza el servidor cuando el número de errores de clave alcanza el límite superior. Entre las respuestas válidas a esta acción se incluyen:  
  
-   **StopProcessing** indica al servidor que detenga el procesamiento cuando se alcance el límite de errores.  
  
-   **StopLogging** indica al servidor que detenga el registro de errores cuando se alcance el límite de errores, pero que permita que el procesamiento continúe.  
  
 **ErrorLog\ LogErrorTypes\KeyNotFound**  
 Especifica la acción que realiza el servidor cuando se produce un error de **KeyNotFound** . Entre las respuestas válidas a este error se incluyen:  
  
-   **IgnoreError** indica al servidor que continúe con el procesamiento sin registrar el error o contarlo de cara al límite de errores de clave. Si se omite el error, se permite que el procesamiento continúe sin agregarlo al recuento de errores o registrarlo en la pantalla o en el archivo de registro. El registro en cuestión tiene un problema de integridad de datos y no se puede agregar a la base de datos. El registro se descartará o se agregará al Miembro desconocido, según determine la propiedad **KeyErrorAction** .  
  
-   **ReportAndContinue** indica al servidor que registre el error, lo cuente de cara al límite de errores de clave y continúe con el procesamiento. El registro que desencadena el error se descarta o se convierte en Miembro desconocido.  
  
-   **ReportAndStop** indica al servidor que registre el error y detenga el procesamiento inmediatamente, cualquiera que sea el límite de errores de clave. El registro que desencadena el error se descarta o se convierte en Miembro desconocido.  
  
 **ErrorLog\ LogErrorTypes\KeyDuplicate**  
 Especifica la acción que realiza el servidor cuando se encuentra una clave duplicada. Entre los valores válidos se incluyen **IgnoreError** para continuar con el procesamiento como si el error no se hubiera producido, **ReportAndContinue** para registrar el error y continuar con el procesamiento, y **ReportAndStop** para registrar el error y detener el procesamiento inmediatamente, aunque el recuento de errores esté por debajo del límite de errores.  
  
 **ErrorLog\ LogErrorTypes\NullKeyConvertedToUnknown**  
 Especifica la acción que realiza el servidor cuando una clave NULL se ha convertido en Miembro desconocido. Entre los valores válidos se incluyen **IgnoreError** para continuar con el procesamiento como si el error no se hubiera producido, **ReportAndContinue** para registrar el error y continuar con el procesamiento, y **ReportAndStop** para registrar el error y detener el procesamiento inmediatamente, aunque el recuento de errores esté por debajo del límite de errores.  
  
 **ErrorLog\ LogErrorTypes\NullKeyNotAllowed**  
 Especifica la acción que realiza el servidor cuando **NullProcessing** se establece en **Error** para un atributo de dimensión. Se genera un error cuando no se permite un valor NULL en un atributo determinado. Esta propiedad de configuración de errores informa al paso siguiente, que es notificar el error y continuar con el procesamiento hasta que se alcance el límite de errores. Entre los valores válidos se incluyen **IgnoreError** para continuar con el procesamiento como si el error no se hubiera producido, **ReportAndContinue** para registrar el error y continuar con el procesamiento, y **ReportAndStop** para registrar el error y detener el procesamiento inmediatamente, aunque el recuento de errores esté por debajo del límite de errores.  
  
 **ErrorLog\ LogErrorTypes\CalculationError**  
 Una propiedad utilizada como valor predeterminado durante la operación de procesamiento realizada por el servidor.  
  
 **ErrorLog\IgnoreDataTruncation**  
 Una propiedad utilizada como valor predeterminado durante la operación de procesamiento realizada por el servidor.  
  
## <a name="exception"></a>Excepción  
 **Exception\CreateAndSendCrashReports**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\CrashReportsFolder**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\SQLDumperFlagsOn**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\SQLDumperFlagsOff**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\MiniDumpFlagsOn**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Exception\MinidumpErrorList**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="flight-recorder"></a>Caja negra SQL  
 **FlightRecorder\Enabled**  
 Una propiedad booleana que indica si la característica Caja negra SQL está habilitada.  
  
 **FlightRecorder\FileSizeMB**  
 Una propiedad de entero de 32 bits con signo que define el tamaño del archivo de disco de la caja negra SQL, en megabytes.  
  
 **FlightRecorder\LogDurationSec**  
 Una propiedad de entero de 32 bits con signo que define la frecuencia con la que se activa la caja negra SQL, en segundos.  
  
 **FlightRecorder\SnapshotDefinitionFile**  
 Una propiedad de cadena que define el nombre del archivo de definición de instantáneas, que contiene comandos de descubrimiento que se emiten al servidor cuando se toma una instantánea.  
  
 El valor predeterminado para esta propiedad está en blanco, que a su vez establece el valor predeterminado en el nombre de archivo FlightRecorderSnapshotDef.xml.  
  
 **FlightRecorder\SnapshotFrequencySec**  
 Una propiedad de entero de 32 bits con signo que define la frecuencia de instantáneas, en segundos.  
  
 **FlightRecorder\TraceDefinitionFile**  
 Una propiedad de cadena que especifica el nombre del archivo de definición de seguimiento de la Caja negra SQL.  
  
 El valor predeterminado para esta propiedad está en blanco, que a su vez establece el valor predeterminado en FlightRecorderTraceDef.xml.  
  
## <a name="query-log"></a>Registro de consultas  
 **Se aplica a:** modo de servidor multidimensional únicamente  
  
 **QueryLog\QueryLogFileName**  
 Una propiedad de cadena que especifica el nombre del archivo de registro de consultas. Esta propiedad solo se aplica cuando se utiliza un archivo de disco para realizar el registro, a diferencia de cuando se utiliza una tabla de base de datos (comportamiento predeterminado).  
  
 **QueryLog\QueryLogSampling**  
 Una propiedad de entero de 32 bits que especifica la velocidad de muestreo del registro de consultas.  
  
 El valor predeterminado para esta propiedad es 10, lo que significa que se ha registrado 1 de cada 10 consultas del servidor.  
  
 **QueryLog\QueryLogFileSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **QueryLog\QueryLogConnectionString**  
 Una propiedad de cadena que especifica la conexión con la base de datos del registro de consultas.  
  
 **QueryLog\QueryLogTableName**  
 Una propiedad de cadena que especifica el nombre de la tabla del registro de consultas.  
  
 El valor predeterminado de esta propiedad es OlapQueryLog.  
  
 **QueryLog\CreateQueryLogTable**  
 Una propiedad booleana que especifica si se crea la tabla del registro de consultas.  
  
 El valor predeterminado para esta propiedad es False, que indica que el servidor no creará automáticamente la tabla del registro y no registrará eventos de consulta.  
  
> [!NOTE]  
>  Para obtener más información sobre cómo configurar el registro de consultas, vea el tema sobre la [configuración del registro de consultas de Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81890).  
  
## <a name="trace"></a>Seguimiento  
 **Trace\TraceBackgroundDistributionPeriod**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceBackgroundFlushPeriod**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceFileBufferSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceFileWriteTrailerPeriod**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceMaxRowsetSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceProtocolTraffic**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceQueryResponseTextChunkSize**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceReportFQDN**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceRequestParameters**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **Trace\TraceRowsetBackgroundFlushPeriod**  
 Una propiedad avanzada que no debería cambiar, salvo a petición de expertos en soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
