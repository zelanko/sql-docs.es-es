---
title: Catalog.worker_agents (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0bd0d827-e2f1-44fe-aa90-6bf922d68d16
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: d56af0ab150255c53746898a638a32112938755c
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="catalogworkeragents-ssisdb-database"></a>Catalog.worker_agents (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Muestra la información de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala Out trabajo.

|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|WorkerAgentId|**uniqueidentifier**|El agente de trabajo Id. de escala Out trabajo.|
|IsEnabled|**bit**|Si está habilitado el trabajador Out de la escala.|
|DisplayName|**nvarchar(256)**|El nombre para mostrar del trabajador Out en escala.|
|Description|**nvarchar(256)**|La descripción de la escala fuera trabajo.|
|MachineName|**nvarchar(256)**|El nombre del equipo para escala Out trabajador.|
|Etiquetas|**nvarchar(max)**|Las etiquetas de escala Out trabajo.|
|UserAccount|**nvarchar(256)**|La cuenta de usuario que se ejecuta el servicio de escala Out trabajo.|
|LastOnlineTime|**DateTimeOffset(7)**|La última vez que el trabajador de salida de escala está en línea.|

## <a name="remarks"></a>Comentarios
Esta vista muestra una fila para cada escala Out trabajador conectarse a la escala fuera Master trabajar con el catálogo de SSISDB.

## <a name="permissions"></a>Permissions
Esta vista exige uno de los siguientes permisos:

- La pertenencia a la **ssis_admin** rol de base de datos

- La pertenencia a la **ssis_cluster_executor** rol de base de datos

- La pertenencia a la **sysadmin** rol de servidor

