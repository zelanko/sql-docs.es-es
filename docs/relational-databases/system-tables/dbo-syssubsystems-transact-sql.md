---
title: Subsistemas de dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssubsystems
- syssubsystems
- syssubsystems_TSQL
- dbo.syssubsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syssubsystems system table
ms.assetid: 114b3d55-1ad6-4777-b868-8ef0c86ba596
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7de71454c59ede4bfea182ea605a0e9d59da2c00
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890358"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene información sobre todos los subsistemas proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibles. La tabla **syssubsystems** se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|Id. del subsistema.|  
|**subsistema**|**nvarchar(40)**|Nombre del subsistema.|  
|**description_id**|**int**|ID. de mensaje de la fila de la vista de catálogo **Sys. Messages** que contiene la descripción del subsistema.|  
|**subsystem_dll**|**nvarchar(255)**|Ubicación de la DLL del subsistema.|  
|**agent_exe**|**nvarchar(255)**|Ruta de acceso completa al archivo ejecutable que utiliza el subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Función a la que se llama cuando el subsistema se inicializa.|  
|**event_entry_point**|**nvarchar(30)**|Función a la que se llama cuando se ejecuta un paso del subsistema.|  
|**stop_entry_point**|**nvarchar(30)**|Función a la que se llama cuando un subsistema deja de ejecutarse.|  
|**max_worker_threads**|**int**|Número máximo de pasos simultáneos para un subsistema dado.|  
  
## <a name="remarks"></a>Comentarios  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden tener acceso a esta tabla.  
  
## <a name="see-also"></a>Consulte también  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
