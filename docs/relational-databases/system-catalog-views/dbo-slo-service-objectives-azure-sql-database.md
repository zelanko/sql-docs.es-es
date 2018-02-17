---
title: dbo.slo_service_objectives (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database
ms.service: sql-database
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
f1_keywords:
- dbo.slo_service_objectives
- dbo.slo_service_objectives_TSQL
- slo_service_objectives
- slo_service_objectives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dbo.slo_service_objectives
- slo_service_objectives
ms.assetid: d5dd7ed9-440a-4432-ad45-644e4e72318f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a5d3a911aa1ffa5088f2a817c2434c98eb7cbe3
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/16/2018
---
# <a name="dbosloserviceobjectives-azure-sql-database"></a>dbo.slo_service_objectives (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  Esta característica está en estado de vista previa y está en desuso en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12. No dependa de la implementación específica de esta característica, ya que podría modificarse o quitarse en una versión futura.  
  
 Devuelve información sobre el Objetivo de nivel de servicio (SLO) del servidor actual.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V11.|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|objective_id|**uniqueidentifier**|Identificador del objetivo de nivel de servicio.|  
|name|**sysname**|Nombre del objetivo de nivel de servicio.|  
|description|**nvarchar**|Descripción del objetivo de nivel de servicio.|  
|create_date|**datetimeoffset(7)**|fecha de creación del objeto de nivel de servicio en el servidor.|  
|is_system|**bit**|1 = objetivo de nivel de servicio del sistema|  
|is_default|**bit**|1 = el objetivo de nivel de servicio es el SLO predeterminado.|  
|state|**tinyint**|1 = el objetivo de nivel de servicio está habilitado.<br /><br /> 2 = el objetivo de nivel de servicio está deshabilitado.|  
|state_desc|**nvarchar**|Descripción del objetivo de nivel de servicio.|  
|metadata_version|**decimal**|Versión del objetivo de nivel de servicio.|  
  
## <a name="permissions"></a>Permissions  
 Esta vista está disponible para todos los roles de usuario con permisos para conectarse a virtual **maestro** base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Administración de bases de datos Premium](http://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
