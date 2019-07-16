---
title: dbo.syssubsystems (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3f06182f06e92ff581dd02c072b63fc10962921a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069086"
---
# <a name="dbosyssubsystems-transact-sql"></a>dbo.syssubsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene información sobre todos los subsistemas proxy del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponibles. El **syssubsystems** tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|Id. del subsistema.|  
|**subsystem**|**nvarchar(40)**|Nombre del subsistema.|  
|**description_id**|**int**|Id. de la fila de mensaje la **sys.messages** vista de catálogo que contiene la descripción del subsistema.|  
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
  
  
