---
title: Catalog.environment_references (base de datos de SSISDB) | Documentos de Microsoft
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
ms.assetid: efec53ef-3e5a-4b76-b71d-a0cf9e11ac00
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ee6f15af7a5384fea850aa67c7b5a95483530740
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogenvironmentreferences-ssisdb-database"></a>catalog.environment_references (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las referencias de entorno para todos los proyectos en el **SSISDB** catálogo.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|reference_id|**bigint**|Identificador (id.) único de la referencia.|  
|identificador de proyecto|**bigint**|Identificador único del proyecto.|  
|reference_type|**Char (1)**|Indica si el entorno se puede encontrar en la misma carpeta que el proyecto (referencia relativa) o en una carpeta diferente (referencia absoluta). Cuando el valor es `R`, el entorno se encuentra utilizando una referencia relativa. Cuando el valor es `A`, el entorno se encuentra utilizando una referencia absoluta.|  
|environment_folder_name|**sysname**|Nombre de la carpeta si el entorno se encuentra utilizando una referencia absoluta.|  
|environment_name|**sysname**|Nombre del entorno al que hace referencia el proyecto.|  
|validation_status|**Char (1)**|El estado de la validación.|  
|last_validation_time|**datatimeoffset(7)**|Hora de la última validación.|  
  
## <a name="remarks"></a>Comentarios  
 En esta vista se muestra una fila por cada referencia al entorno del catálogo.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en el proyecto correspondiente  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor.  
  
> [!NOTE]  
>  Si tiene permiso READ en un proyecto, también tendrá permiso READ en todos los paquetes y referencias de entorno asociados a ese proyecto. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
## <a name="remarks"></a>Comentarios  
 Un proyecto puede tener referencias de entorno absolutas o relativas. Las referencias relativas se refieren al entorno por nombre y requieren que resida en la misma carpeta que el proyecto. Las referencias absolutas hacen referencia al entorno por nombre y carpeta, y pueden hacer referencia a los entornos que residen en una carpeta diferente que el proyecto. Un proyecto puede hacer referencia a varios entornos.  
  
  

