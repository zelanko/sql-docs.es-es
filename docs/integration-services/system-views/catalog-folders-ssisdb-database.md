---
title: Catalog.Folders (base de datos SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 21a37c16-60aa-4b3f-8bca-ac90ad1697ac
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9622bd1a5f1415c9f506a00a63441081154b53ff
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las carpetas del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|id|**bigint**|Identificador único de la carpeta.|  
|name|**sysname(nvarchar(128)**|Nombre de la carpeta, que es único dentro del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|description|**nvarchar (1024)**|Descripción de la carpeta.|  
|created_by_sid|**varbinary (85)**|Identificador de seguridad único (SID) del usuario que creó la carpeta.|  
|created_by_name|**nvarchar (128)**|Nombre del usuario que creó la carpeta.|  
|created_time|**DateTimeOffset(7)**|Fecha y hora en que se creó la carpeta.|  
  
## <a name="remarks"></a>Comentarios  
 Esta vista muestra una fila para cada carpeta en el catálogo.  
  
## <a name="permissions"></a>Permissions  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la carpeta  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  

