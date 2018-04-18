---
title: sp_enum_sqlagent_subsystems (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad4a380353dddd0bf17a25952b81220f2f2e6a2d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra una lista de los subsistemas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>Argumentos  
 None  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|Nombre del subsistema.|  
|**Descripción**|**nvarchar(512)**|Descripción del subsistema.|  
|**subsystem_dll**|**nvarchar(510)**|Módulo DLL que contiene el subsistema.|  
|**agent_exe**|**nvarchar(510)**|Módulo ejecutable utilizado por el subsistema.|  
|**start_entry_point**|**nvarchar(30)**|Procedimiento al que el Agente SQL Server llama durante la ejecución de pasos de trabajo.|  
|**event_entry_point**|**nvarchar(30)**|Procedimiento al que el Agente SQL Server llama durante la ejecución de pasos de trabajo.|  
|**stop_entry_point**|**nvarchar(30)**|Procedimiento al que el Agente SQL Server llama durante la ejecución de pasos de trabajo.|  
|**max_worker_threads**|**int**|Número máximo de subprocesos que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciará para este subsistema.|  
|**subsystem_id**|**int**|Identificador del subsistema.|  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento enumera los subsistemas disponibles en la instancia.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. A otros usuarios debe concederse el rol fijo de base de datos **SQLAgentOperatorRole** en la base de datos **msdb** .  
  
 Para obtener más información acerca de **SQLAgentOperatorRole**, consulte [Roles fijos de base de datos de SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
## <a name="see-also"></a>Vea también  
 [Implementar la seguridad del Agente SQL Server](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
