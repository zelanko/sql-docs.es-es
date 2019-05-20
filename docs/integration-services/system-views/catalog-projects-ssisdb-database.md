---
title: catalog.projects (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a6b595e1-5227-47ce-8ee2-a28c1e1d5645
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b18b2bdd034cf5d6864ddb4e652eda0266758a3
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65714433"
---
# <a name="catalogprojects-ssisdb-database"></a>catalog.projects (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los detalles de todos los proyectos que aparecen en el catálogo de **SSISDB**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|identificador de proyecto|**bigint**|El identificador único (Id.) del proyecto.|  
|folder_id|**bigint**|El identificador único de la carpeta donde reside el proyecto.|  
|NAME|**sysname**|Nombre del proyecto.|  
|description|**nvarchar(1024)**|Descripción opcional del proyecto.|  
|project_format_version|**int**|Versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para desarrollar el proyecto.|  
|deployed_by_sid|**varbinary(85)**|Identificador de seguridad (SID) del usuario que instaló el proyecto.|  
|deployed_by_name|**nvarchar(128)**|Nombre del usuario que instaló el proyecto.|  
|last_deployed_time|**datetimeoffset(7)**|Fecha y hora en que el proyecto se implementó por primera vez o se volvió a implementar.|  
|created_time|**datetimeoffset(7)**|Fecha y hora en que se creó el proyecto.|  
|object_version_lsn|**bigint**|Versión del proyecto. No se garantiza que este número sea secuencial.|  
|validation_status|**char(1)**|El estado de la validación|  
|last_validation_time|**datetimeoffset(7)**|Hora de la última validación.|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra una fila para cada proyecto del catálogo.  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol del servidor de **sysadmin**  
  
> [!NOTE]  
>  Si tiene permiso READ en un proyecto, también tendrá permiso READ en todos los paquetes y referencias de entorno asociados a ese proyecto. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
