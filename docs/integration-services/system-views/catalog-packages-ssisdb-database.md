---
title: Catalog.Packages (base de datos SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
helpviewer_keywords:
- packages view [Integration Services]
- catalog.packages view [Integration Services]
ms.assetid: a634e94d-f492-4dfd-9611-a35f545106a1
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f836c2b1bdf59f157f10abb708ed55f99dfc9f0f
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogpackages-ssisdb-database"></a>catalog.packages (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los detalles de todos los paquetes que aparecen en la **SSISDB** catálogo.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|package_id|**bigint**|El identificador único (Id.) del paquete.|  
|name|**nvarchar(256)**|El nombre único del paquete.|  
|package_guid|**uniqueidentifier**|El identificador único global (GUID) que identifica el paquete.|  
|description|**nvarchar (1024)**|Una descripción opcional del paquete.|  
|package_format_version|**int**|La versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para desarrollar el paquete.|  
|version_major|**int**|Versión principal del paquete.|  
|version_minor|**int**|Versión secundaria del paquete.|  
|version_build|**int**|La versión de la compilación del paquete.|  
|version_comments|**nvarchar (1024)**|Comentarios opcionales acerca de la versión del paquete.|  
|version_guid|**uniqueidentifier**|El GUID que identifica de forma exclusiva la versión del paquete.|  
|identificador de proyecto|**bigint**|Identificador único del proyecto.|  
|entry_point|**bit**|El valor de `1` significa que el paquete se puede iniciar directamente. El valor de `0` significa que el paquete debe ser iniciado por otro paquete mediante la tarea Ejecutar paquete. El valor predeterminado es `1`.|  
|validation_status|**Char (1)**|El estado de la validación.|  
|last_validation_time|**DateTimeOffset(7)**|Hora de la última validación.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada paquete del catálogo.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto correspondiente  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor.  
  
> [!NOTE]  
>  Si tiene permiso READ en un proyecto, también tendrá permiso READ en todos los paquetes y referencias de entorno asociados a ese proyecto. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  

