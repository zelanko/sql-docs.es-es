---
title: catalog.folders (base de datos de SSISDB) | Microsoft Docs
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6ac40d88cd99c30f8cb5d80037d7e8ae4195bdd
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="catalogfolders-ssisdb-database"></a>catalog.folders (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Muestra las carpetas del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|id|**bigint**|Identificador único de la carpeta.|  
|NAME|**sysname(nvarchar(128)**|Nombre de la carpeta, que es único dentro del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|description|**nvarchar(1024)**|Descripción de la carpeta.|  
|created_by_sid|**varbinary(85)**|Identificador de seguridad único (SID) del usuario que creó la carpeta.|  
|created_by_name|**nvarchar(128)**|Nombre del usuario que creó la carpeta.|  
|created_time|**datetimeoffset(7)**|Fecha y hora en que se creó la carpeta.|  
  
## <a name="remarks"></a>Notas  
 Esta vista muestra una fila para cada carpeta en el catálogo.  
  
## <a name="permissions"></a>Permisos  
 Esta vista exige uno de los siguientes permisos:  
  
-   Permiso READ en la carpeta  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
> [!NOTE]  
>  Cuando se dispone de permiso para realizar una operación en el servidor, también se dispone de permiso para ver información sobre la operación. Se aplica la seguridad en el nivel de fila; solo se muestran las filas para las que disponga de permiso para ver.  
  
  
