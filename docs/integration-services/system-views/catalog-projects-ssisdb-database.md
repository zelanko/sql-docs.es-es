---
title: Catalog.Projects (base de datos SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 668890ae464deb8dfa029eab38b608fee12af0ca
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los detalles de todos los proyectos que aparecen en la **SSISDB** catálogo.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|identificador de proyecto|**bigint**|El identificador único (Id.) del proyecto.|  
|folder_id|**bigint**|El identificador único de la carpeta donde reside el proyecto.|  
|name|**sysname**|Nombre del proyecto.|  
|description|**nvarchar (1024)**|Descripción opcional del proyecto.|  
|project_format_version|**int**|Versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para desarrollar el proyecto.|  
|deployed_by_sid|**varbinary (85)**|Identificador de seguridad (SID) del usuario que instaló el proyecto.|  
|deployed_by_name|**nvarchar (128)**|Nombre del usuario que instaló el proyecto.|  
|last_deployed_time|**DateTimeOffset(7)**|Fecha y hora en que el proyecto se implementó por primera vez o se volvió a implementar.|  
|created_time|**DateTimeOffset(7)**|Fecha y hora en que se creó el proyecto.|  
|object_version_lsn|**bigint**|Versión del proyecto. No se garantiza que este número sea secuencial.|  
|validation_status|**Char (1)**|El estado de la validación|  
|last_validation_time|**DateTimeOffset(7)**|Hora de la última validación.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada proyecto del catálogo.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor.  
  
> [!NOTE]  
>  Si tiene permiso READ en un proyecto, también tendrá permiso READ en todos los paquetes y referencias de entorno asociados a ese proyecto. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
