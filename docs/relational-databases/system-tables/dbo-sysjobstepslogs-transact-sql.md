---
title: dbo.sysjobstepslogs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs: TSQL
helpviewer_keywords: sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 050feecde1f82ca8962552744e2fc2d43d28bd4c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene el registro de los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que están configurados para escribir sus resultados en una tabla. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|Id. del registro de pasos de trabajo.|  
|**registro**|**nvarchar(max)**|Contenido del registro de pasos de trabajo.|  
|**Date_Created**|**datetime**|Fecha y hora en que se creó el registro de pasos de trabajo.|  
|**DATE_MODIFIED**|**datetime**|Fecha y hora en que se modificó por última vez el registro de pasos de trabajo.|  
|**log_size**|**int**|Tamaño del registro de pasos de trabajo, en bytes.|  
|**step_uid**|**uniqueidentifier**|Identificador único del paso de trabajo.|  
  
## <a name="see-also"></a>Vea también  
 [sp_help_jobsteplog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [sp_delete_jobsteplog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
