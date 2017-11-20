---
title: Catalog.execution_data_taps | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 54226c01-5b8f-4730-8a5f-1da2613f9689
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bc949b9b6111c65d6faa43a118efd03068630fe0
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogexecutiondatataps"></a>catalog.execution_data_taps
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra información de cada derivación de datos definida en una ejecución.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|data_tap_id|**bigint**|Identificador (id.) único de la derivación de datos.|  
|execution_id|**bigint**|Identificador único (id.) de la instancia de ejecución.|  
|package_path|**nvarchar(max)**|Ruta de acceso del paquete de la tarea de flujo de datos en la que se derivan los datos.|  
|dataflow_path_id_string|**nvarchar(4000)**|Cadena de identificación de la ruta de flujo de datos.|  
|dataflow_task_guid|**uniqueidentifier**|Identificador único de la tara de flujos de datos.|  
|max_rows|**int**|Número de filas que se van a capturar. Si este valor no se especifica, se capturan todas las filas.|  
|filename|**nvarchar(4000)**|Nombre del archivo de volcado de datos. Para obtener más información, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).|  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la instancia de ejecución  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
## <a name="see-also"></a>Vea también  
 [Generar archivos de volcado para la ejecución de paquetes](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  

