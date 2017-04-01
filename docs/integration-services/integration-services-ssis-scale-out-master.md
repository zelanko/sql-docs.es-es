---
title: "Patr&#243;n de escalado horizontal de Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e89803f-0471-40ba-b5e4-ddd2c815eecd
caps.latest.revision: 7
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 7
---
# Patr&#243;n de escalado horizontal de Integration Services (SSIS)
El patrón de escalado horizontal administra el sistema de escalado horizontal mediante el catálogo SSISDB y el servicio de patrón de escalado horizontal. 

El catálogo SSISDB almacena toda la información de los trabajadores de escalado horizontal, los paquetes y las ejecuciones. Proporciona la interfaz para habilitar un trabajador de escalado horizontal y ejecutar paquetes en el escalado horizontal. Para obtener más información, consulte [Tutorial: configuración del escalado horizontal de Integration Services](../integration-services/walkthrough-set-up-integration-services-scale-out.md) o [Ejecutar paquetes en Integration Services](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).

El patrón de escalado horizontal es un servicio de Windows que se encarga de la comunicación con los trabajadores de escalado horizontal. Intercambia el estado de las ejecuciones de paquetes con los trabajadores de escalado horizontal a través de HTTPS y opera en los datos en SSISDB. 

## <a name="scale-out-related-sql-views-and-stored-procdures-in-ssisdb"></a>Vistas y procedimientos almacenados de SQL relacionados con el escalado horizontal en SSISDB

### <a name="views"></a>Views:
[[catalog].[master_properties]](../integration-services/system-views/catalog-master-properties-ssisdb-database.md), [[catalog].[worker_agents]](../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).
### <a name="stored-procedures"></a>Procedimientos almacenados:

- Para la administración del trabajador de escalado horizontal:  
 [[catalog].[disable_worker_agent]](../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md), [[catalog].[enable_worker_agent]](../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md).
- Para ejecutar paquetes en el escalado horizontal:   
[[catalog].[create_execution]](../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [[catalog].[add_execution_worker]](../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md), [[catalog].[start_execution]](../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>Configurar el servicio de patrón de escalado horizontal de SQL Server Integration Services
El servicio de patrón de escalado horizontal puede configurarse mediante el archivo \<controlador\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config. El servicio debe reiniciarse después de actualizar el archivo de configuración.


Configuración  |Description  |Valor predeterminado  
---------|---------|---------
PortNumber|Número de puerto de red usado para comunicarse con un trabajador de escalado horizontal.|8391         
SSLCertThumbprint|Huella digital del certificado SSL usado para proteger la comunicación con un trabajador de escalado horizontal.|Huella digital del certificado SSL especificado durante la instalación del patrón de escalado horizontal         
InstanceName|Nombre de la instancia de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] que incluye el catálogo SSISDB. MSSQLSERVER es el nombre de la instancia predeterminada de [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]. |Nombre de la instancia de SQL Server que se instala con el patrón de escalado horizontal         
CleanupCompletedJobsIntervalInMs|Intervalo de limpieza de los trabajos de ejecución terminados en milisegundos.|43200000         
DealWithExpiredTasksIntervalInMs|Intervalo para tratar con los trabajos de ejecución terminados en milisegundos.|300000
MasterHeartbeatIntervalInMs|Intervalo de latido del patrón de escalado horizontal en milisegundos. Especifica el intervalo según el que el patrón de escalado horizontal actualiza su estado de conexión en el catálogo SSISDB.|30000        

## <a name="view-scale-out-master-service-log"></a>Ver registro del servicio de patrón de escalado horizontal
El archivo de registro del servicio de patrón de escalado horizontal se encuentra en la ruta de acceso de la carpeta \<controlador\>: \Users\\*[cuenta]*\AppData\Local\SSIS\Cluster\Master. 

La carpeta *[cuenta]* se refiere a la cuenta que ejecuta el servicio de patrón de escalado horizontal. De forma predeterminada, esta cuenta es SSISScaleOutMaster140.