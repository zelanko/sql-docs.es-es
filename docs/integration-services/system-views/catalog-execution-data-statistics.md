---
title: Catalog.execution_data_statistics | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 6f51407e-0e4e-4b44-af33-db14c9d40ded
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: fa1d87489ff6d0a10d95bf160ded3d038ca39d81
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutiondatastatistics"></a>catalog.execution_data_statistics
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta vista muestra una fila cada vez que un componente de flujo de datos envía datos a un componente de nivel inferior para una ejecución del paquete determinada. La información de esta vista se puede usar para calcular el rendimiento de datos de un componente.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|data_stats_id|**bigint**|Identificador (id.) único de los datos.|  
|execution_id|**bigint**|Identificador único para la instancia de ejecución.|  
|package_name|**nvarchar (260)**|Nombre del primer paquete que se inició durante la ejecución.|  
|task_name|**nvarchar(4000)**|Nombre de la tarea Flujo de datos.|  
|dataflow_path_id_string|**nvarchar(4000)**|Cadena de identificación de la ruta de flujo de datos.|  
|dataflow_path_name|**nvarchar(4000)**|Nombre de la ruta de flujo de datos.|  
|source_component_name|**nvarchar(4000)**|Nombre del componente de flujo de datos que envió los datos.|  
|destination_component_name|**nvarchar(4000)**|Nombre del componente de flujo de datos que recibió los datos.|  
|rows_sent|**bigint**|Número de filas enviadas desde el componente de origen.|  
|created_time|**datatimeoffset(7)**|Hora en que se obtuvieron los valores.|  
|execution_path|**nvarchar(max)**|Ruta de acceso de ejecución del componente.|  
  
## <a name="remarks"></a>Comentarios  
  
-   Cuando hay varios resultados del componente, se agrega una fila para cada uno de ellos.  
  
-   De forma predeterminada, cuando se inicia una ejecución, la información sobre el número de filas que se envían no se registra.  
  
-   Para ver estos datos para la ejecución de un paquete determinado, establezca el nivel de registro en **detallado**. Para más información, vea [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
