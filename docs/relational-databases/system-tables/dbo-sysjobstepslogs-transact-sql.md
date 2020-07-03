---
title: dbo.sysjobstepslogs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysjobstepslogs_TSQL
- sysjobstepslogs_TSQL
- sysjobstepslogs
- dbo.sysjobstepslogs
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobstepslogs system table
ms.assetid: 128c25db-0b71-449d-bfb2-38b8abcf24a0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1807760e10c6a158ab2ef05162e391290e073ab4
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890428"
---
# <a name="dbosysjobstepslogs-transact-sql"></a>dbo.sysjobstepslogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene el registro de los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que están configurados para escribir sus resultados en una tabla. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**log_id**|**int**|Id. del registro de pasos de trabajo.|  
|**inicia**|**nvarchar(max)**|Contenido del registro de pasos de trabajo.|  
|**date_created**|**datetime**|Fecha y hora en que se creó el registro de pasos de trabajo.|  
|**date_modified**|**datetime**|Fecha y hora en que se modificó por última vez el registro de pasos de trabajo.|  
|**log_size**|**int**|Tamaño del registro de pasos de trabajo, en bytes.|  
|**step_uid**|**uniqueidentifier**|Identificador único del paso de trabajo.|  
  
## <a name="see-also"></a>Consulte también  
 [sp_help_jobsteplog &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-jobsteplog-transact-sql.md)   
 [sp_delete_jobsteplog &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-jobsteplog-transact-sql.md)  
  
  
