---
title: Catalog.execution_component_phases | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 07a9a163-4787-40f7-b371-ac5c6cb4b095
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: b3459ce6d7e9eb0b9580ffa54e3b87e16f3e8fb0
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="catalogexecutioncomponentphases"></a>catalog.execution_component_phases
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra el tiempo dedicado por un componente de flujo de datos a cada fase de ejecución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|phase_stats_id|**bigint**|Identificador (id.) único de la fase.|  
|execution_id|**bigint**|Identificador único para la instancia de ejecución.|  
|package_name|**nvarchar (260)**|Nombre del primer paquete que se inició durante la ejecución.|  
|task_name|**nvarchar(4000)**|Nombre de la tarea Flujo de datos.|  
|subcomponent_name|**nvarchar(4000)**|Nombre del componente de flujo de datos.|  
|phase|**nvarchar (128)**|Nombre de la fase de ejecución.|  
|start_time|**DateTimeOffset(7)**|Hora a la que se inició la fase.|  
|end_time|**DateTimeOffset(7)**|Hora a la que finalizó la fase.|  
|execution_path|**nvarchar(max)**|Ruta de ejecución de la tarea Flujo de datos.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada fase de ejecución de un componente de flujo de datos, como Validate, Pre-Execute, Post-Execute, PrimeOutput y ProcessInput. Cada fila muestra la hora de inicio y de finalización de una fase de ejecución concreta.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa la vista catalog.execution_component_phases para averiguar la cantidad total de tiempo que un paquete específico para su ejecución en todas las fases (**active_time**) y el tiempo total transcurrido para el paquete (**total_time**).  
  
> [!WARNING]  
>  La vista catalog.execution_component_phases proporciona esta información cuando el nivel de registro de la ejecución del paquete se establece en Performance (Rendimiento) o Verbose (Detallado). Para más información, vea [Enable Logging for Package Execution on the SSIS Server](../../integration-services/performance/integration-services-ssis-logging.md#server_logging).  
  
```sql
use SSISDB  
select package_name, task_name, subcomponent_name, execution_path,  
    SUM(DATEDIFF(ms,start_time,end_time)) as active_time,  
    DATEDIFF(ms,min(start_time), max(end_time)) as total_time  
from catalog.execution_component_phases  
where execution_id = 1841  
group by package_name, task_name, subcomponent_name, execution_path  
order by package_name, task_name, subcomponent_name, execution_path  
```  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
