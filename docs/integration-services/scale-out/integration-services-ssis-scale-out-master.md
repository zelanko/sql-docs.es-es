---
title: SQL Server Integration Services (SSIS) escalada Master | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 1672c015186998065b5d6dc95897147aa11d14ec
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out-master"></a>Patrón de escalado horizontal de Integration Services (SSIS)
El patrón de escalado horizontal administra el sistema de escalado horizontal mediante el catálogo SSISDB y el servicio de patrón de escalado horizontal. 

El catálogo SSISDB almacena toda la información de los trabajadores de escalado horizontal, los paquetes y las ejecuciones. Proporciona la interfaz para habilitar un trabajador de escalado horizontal y ejecutar paquetes en el escalado horizontal. Para obtener más información, consulte [Tutorial: configuración del escalado horizontal de Integration Services](walkthrough-set-up-integration-services-scale-out.md) o [Ejecutar paquetes en Integration Services](run-packages-in-integration-services-ssis-scale-out.md).

El patrón de escalado horizontal es un servicio de Windows que se encarga de la comunicación con los trabajadores de escalado horizontal. Intercambia el estado de las ejecuciones de paquetes con los trabajadores de escalado horizontal a través de HTTPS y opera en los datos en SSISDB. 

## <a name="scale-out-related-sql-views-and-stored-procedures-in-ssisdb"></a>Escala relacionadas con vistas SQL y procedimientos almacenados de SSISDB

#### <a name="views"></a>Views:
[[catalog].[master_properties]](../../integration-services/system-views/catalog-master-properties-ssisdb-database.md), [[catalog].[worker_agents]](../../integration-services/system-views/catalog-worker-agents-ssisdb-database.md).

#### <a name="stored-procedures"></a>Procedimientos almacenados:

- Para la administración del trabajador de escalado horizontal:  
 [[catalog].[disable_worker_agent]](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md), [[catalog].[enable_worker_agent]](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md).
- Para ejecutar paquetes en el escalado horizontal:   
[[catalog].[create_execution]](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [[catalog].[add_execution_worker]](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md), [[catalog].[start_execution]](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).   

## <a name="configure-sql-server-integration-services-scale-out-master-service"></a>Configurar el servicio de patrón de escalado horizontal de SQL Server Integration Services
El servicio de patrón de escalado horizontal puede configurarse mediante el archivo \<controlador\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config. El servicio debe reiniciarse después de actualizar el archivo de configuración.


Configuración  |Description  |Valor predeterminado  
---------|---------|---------
PortNumber|Número de puerto de red usado para comunicarse con un trabajador de escalado horizontal.|8391         
SSLCertThumbprint|Huella digital del certificado SSL usado para proteger la comunicación con un trabajador de escalado horizontal.|Huella digital del certificado SSL especificado durante la instalación del patrón de escalado horizontal         
SqlServerName|El nombre de la [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] que contiene el catálogo de SSISDB. Por ejemplo: ServerName\\\\InstanceName.|El nombre de SQL Server que se instala con el maestro de salida de escala.         
CleanupCompletedJobsIntervalInMs|Intervalo de limpieza de los trabajos de ejecución terminados en milisegundos.|43200000         
DealWithExpiredTasksIntervalInMs|Intervalo para tratar con los trabajos de ejecución terminados en milisegundos.|300000
MasterHeartbeatIntervalInMs|Intervalo de latido del patrón de escalado horizontal en milisegundos. Especifica el intervalo según el que el patrón de escalado horizontal actualiza su estado de conexión en el catálogo SSISDB.|30000
SqlConnectionTimeoutInSecs|El tiempo de espera de conexión de SQL en segundos al conectarse a SSISDB.|15        

## <a name="view-scale-out-master-service-log"></a>Ver registro del servicio de patrón de escalado horizontal
El archivo de registro del servicio de escala Out maestra se encuentra en la \<controlador\>: \Users\\*[account]*\AppData\Local\SSIS\ScaleOut\Master ruta de acceso. 

El *[account]* hace referencia a la cuenta que ejecuta el servicio de escala Out Master. De forma predeterminada, esta cuenta es SSISScaleOutMaster140.

