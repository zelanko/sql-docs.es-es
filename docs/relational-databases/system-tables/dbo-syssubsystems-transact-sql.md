---
title: dbo.syssubsystems (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe7c8fa687a5868bae73b9590ea39a30fc90ee2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33254835"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre todos los subsistemas proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibles. El **syssubsystems** tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|Id. del subsistema.|  
|**subsystem**|**nvarchar(40)**|Nombre del subsistema.|  
|**description_id**|**int**|Mensaje de la fila en la **sys.messages** vista de catálogo que contiene la descripción del subsistema.|  
|**subsystem_dll**|**nvarchar(255)**|Ubicación de la DLL del subsistema.|  
|**agent_exe**|**nvarchar(255)**|Ruta de acceso completa al archivo ejecutable que utiliza el subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Función a la que se llama cuando el subsistema se inicializa.|  
|**event_entry_point**|**nvarchar(30)**|Función a la que se llama cuando se ejecuta un paso del subsistema.|  
|**stop_entry_point**|**nvarchar(30)**|Función a la que se llama cuando un subsistema deja de ejecutarse.|  
|**max_worker_threads**|**int**|Número máximo de pasos simultáneos para un subsistema dado.|  
  
## <a name="remarks"></a>Comentarios  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede tener acceso a esta tabla.  
  
## <a name="see-also"></a>Vea también  
 [dbo.sysproxysubsystem &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxysubsystem-transact-sql.md)   
 [dbo.sysproxies &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysproxies-transact-sql.md)   
 [Sys.Messages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)  
  
  
