---
title: Catalog.extended_operation_info (base de datos de SSISDB) | Documentos de Microsoft
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
ms.assetid: db299b45-557d-4c62-8e14-355cdb051f63
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4d89a9adbf89dcc89715832664dcca176cd7f2ff
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogextendedoperationinfo-ssisdb-database"></a>catalog.extended_operation_info (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra la información extendida sobre todas las operaciones del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|info_id|**bigint**|El identificador único (id.) de la información extendida.|  
|operation_id|**bigint**|El Identificador único de la operación que corresponde a la información extendida.|  
|object_name|**nvarchar (260)**|Nombre del objeto.|  
|object_type|**smallint**|Tipo de objeto afectado por la operación. El objeto puede ser una carpeta (`10`), proyecto (`20`), paquete (`30`), entorno (`40`) o instancia de ejecución (`50`).|  
|reference_id|**bigint**|El Identificador único de la referencia que se utiliza en la operación.|  
|status|**int**|Estado de la operación. Los valores posibles son creado (`1`), en ejecución (`2`), cancelado (`3`), con errores (`4`), pendiente (`5`), finalizado inesperadamente (`6`), correcto (`7`), deteniendo (`8`) y completado (`9`).|  
|start_time|**DateTimeOffset(7)**|Fecha y hora en que empezó la operación.|  
|end_time|**DateTimeOffset(7)**|La fecha y hora en la que finalizó la operación.|  
  
## <a name="remarks"></a>Comentarios  
 Una operación única puede tener varias filas de información extendida.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en la operación  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  

