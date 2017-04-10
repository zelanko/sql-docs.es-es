---
title: "Trabajador de escalado horizontal de Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 480a3f3d-9a79-4a02-81e5-7d27afd756c4
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Trabajador de escalado horizontal de Integration Services (SSIS)
El trabajador de escalado horizontal ejecuta un servicio de trabajador de escalado horizontal de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion_md](../includes/ssisnoversion-md.md)] para extraer tareas de ejecución del patrón de escalado horizontal y ejecuta los paquetes localmente con ISServerExec.exe.

## <a name="configure-sql-server-integration-services-scale-out-worker-service"></a>Configurar servicio de trabajador de escalado horizontal de SQL Server Integration Services
El servicio de trabajador de escalado horizontal puede configurarse mediante el archivo \<controlador\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config. El servicio debe reiniciarse después de actualizar el archivo de configuración.
    


Configuración  |Description  |Valor predeterminado  
---------|---------|---------
DisplayName|Nombre para mostrar del trabajador de escalado horizontal. **NO está en uso en [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|Nombre de equipo         
Description|Descripción del trabajador de escalado horizontal. **NO está en uso en [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|Vacía         
MasterEndpoint|Punto de conexión para conectarse al patrón de escalado horizontal.|Punto de conexión establecido durante la instalación del trabajador de escalado horizontal         
MasterHttpsCertThumbprint|Huella digital del certificado SSL de cliente usado para autenticar el patrón de escalado horizontal|Huella digital del certificado de cliente especificado durante la instalación del trabajador de escalado horizontal.          
WorkerHttpsCertThumbprint|Huella digital del certificado del patrón de escalado horizontal usado para autenticar el trabajador de escalado horizontal.|Huella digital de un certificado creado e instalado automáticamente durante la instalación del trabajador de escalado horizontal          
StoreLocation|Ubicación del almacén del certificado del trabajador.|LocalMachine       
StoreName|Nombre del almacén en el que está el certificado de ese trabajador.|My         
AgentHeartbeatInterval|Intervalo del latido del trabajador de escalado horizontal.|00:01:00         
TaskHeartbeatInterval|Intervalo del estado de la tarea de generación de informes del trabajador de escalado horizontal.|00:00:10         
HeartbeatErrorTollerance|Una vez transcurrido este período desde el último latido correcto, la tarea finaliza si se recibe una respuesta de error del latido.|00:10:00      
TaskRequestMaxCPU|Límite superior de CPU del trabajador de escalado horizontal para solicitar tareas. **NO está en uso en [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|70.0         
TaskRequestMinMemory|Límite inferior de memoria en MB del trabajador de escalado horizontal para solicitar tareas. **NO está en uso en [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] vNext CTP1.**|100.0         
MaxTaskCount|Número máximo de tareas que puede contener el trabajador de escalado horizontal.|10         
LeaseInterval|Intervalo de concesión de una tarea por parte del trabajador de escalado horizontal.|00:01:00         
TasksRootFolder|Carpeta de registros de tareas. Si el valor está vacío, se usa la ruta de acceso de la carpeta \<controlador\>: \Users\\*[cuenta]*\AppData\Local\SSIS\Cluster\Tasks. [cuenta] es la cuenta que ejecuta el servicio de trabajador de escalado horizontal. De forma predeterminada, la cuenta es SSISScaleOutWorker140.|Vacía         
TaskLogLevel|Nivel de registro de tarea del trabajador de escalado horizontal. (Verbose 0x01, Information 0x02, Warning 0x04, Error 0x08, Progress 0x10, CriticalError 0x20, Audit 0x40)|126 (Information,Warning,Error,Progress,CriticalError,Audit)     
TaskLogSegment|Intervalo de tiempo de un archivo de registro de tarea.|00:00:00         
TaskLogEnabled|Especifica si el registro de tarea está habilitado.|true         
ExecutionLogCacheFolder|Carpeta que se usa para almacenar en caché el registro de ejecución del paquete. Si el valor está vacío, se usa la ruta de acceso de la carpeta \<controlador\>: \Users\\*[cuenta]*\AppData\Local\SSIS\Cluster\Agent\ELogCache. [cuenta] es la cuenta que ejecuta el servicio de trabajador de escalado horizontal. De forma predeterminada, la cuenta es SSISScaleOutWorker140.|Vacía         
ExecutionLogMaxBufferLogCount|Número máximo de registros de ejecución en caché en un búfer de registro de ejecución en memoria.|10000        
ExecutionLogMaxInMemoryBufferCount|Número máximo de búferes de registro de ejecución en memoria para los registros de ejecución.|10         
ExecutionLogRetryCount|Número de reintentos si se produce un error en el registro de ejecución.|3         
AgentId|Id. de agente de trabajador del trabajador de escalado horizontal|Se genera automáticamente        



## <a name="view-scale-out-worker-log"></a>Ver el registro del trabajador de escalado horizontal
El archivo de registro del servicio de trabajador de escalado horizontal está en la ruta de acceso de la carpeta \<controlador\>: \Users\\*[cuenta]*\AppData\Local\SSIS\Cluster\Agent.

TasksRootFolder configura la ubicación del registro de cada tarea individual en el archivo WorkerSettings.config. Si no se especifica, el registro está en la ruta de acceso de la carpeta \<controlador\>: \Users\\*[cuenta]*\AppData\Local\SSIS\Cluster\Tasks. 

La carpeta *[cuenta]* es la cuenta que ejecuta el servicio de trabajador de escalado horizontal. De forma predeterminada, la cuenta es SSISScaleOutWorker140.
    