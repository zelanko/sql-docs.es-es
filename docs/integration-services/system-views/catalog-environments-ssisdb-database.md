---
title: catalog.environments (base de datos de SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 7014c0e3-65dc-4a46-842e-4decf3737748
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9c3660f7314ce9514b4dc03ee2d6fb1490a4eab7
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65715264"
---
# <a name="catalogenvironments-ssisdb-database"></a>catalog.environments (base de datos de SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra los detalles de todos los entornos del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Los entornos contienen variables a las que pueden hacer referencia los proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|environment_id|**bigint**|Identificador único (ID) del entorno.|  
|NAME|**sysname**|El nombre del entorno.|  
|folder_id|**bigint**|Identificador único de la carpeta donde el entorno reside.|  
|description|**nvarchar(1024)**|La descripción del entorno. Este valor es opcional.|  
|created_by_sid|**varbinary(85)**|Identificador de seguridad único (SID) del usuario que creó el entorno.|  
|created_by_name|**nvarchar(128)**|Nombre del usuario que creó el entorno.|  
|created_time|**datetimeoffset**|Fecha y hora en que se creó el entorno.|  
  
## <a name="remarks"></a>Notas  
 En esta vista se muestra una fila por cada entorno del catálogo. Los nombres de entorno solo son únicos con respecto a la carpeta en la que se encuentran. Por ejemplo, un entorno denominado `E1` puede existir en más de una carpeta del catálogo, pero cada carpeta solo puede tener un entorno denominado `E1`.  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso de lectura en el entorno  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
