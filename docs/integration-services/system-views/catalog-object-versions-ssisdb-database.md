---
title: Catalog.object_versions (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2fd8c020-1c77-4702-8e6b-efa6a348daab
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3ea7c5ae054a002b9bb4f150e60f323ae03d702a
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogobjectversions-ssisdb-database"></a>catalog.object_versions (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las versiones de objetos en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. En esta versión, solo las versiones de proyectos se admiten en esta vista.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|object_version_lsn|**bigint**|Identificador único (ID) de la versión del objeto. No se garantiza que este número sea secuencial.|  
|object_id|**bigint**|Identificador único del objeto.|  
|object_type|**smallint**|Tipo de objeto. Se mostrará un valor `20` para los proyectos.|  
|object_name|**sysname(nvarchar(128))**|Nombre del objeto.|  
|description|**nvarchar (1024)**|Descripción del proyecto.|  
|created_by|**nvarchar (128)**|Nombre del usuario que agregó el objeto al catálogo.|  
|created_time|**datetimeoffset**|Fecha y hora en que el objeto se agregó al catálogo.|  
|restored_by|**nvarchar (128)**|Nombre del usuario que restauró el objeto.|  
|last_restored_time|**datetimeoffset**|Fecha y hora en que el objeto se restauró por última vez.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada versión de un objeto en el catálogo.  
  
## <a name="permissions"></a>Permissions  
 Para ver las filas en esta vista, debe tener uno de los siguientes permisos:  
  
-   Permiso READ en el objeto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   Pertenencia en el **sysadmin** rol de servidor.  
  
> [!NOTE]  
>  Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
