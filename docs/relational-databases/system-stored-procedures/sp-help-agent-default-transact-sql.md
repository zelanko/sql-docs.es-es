---
title: sp_help_agent_default (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_help_agent_default
- sp_help_agent_default_TSQL
helpviewer_keywords:
- sp_help_agent_default
ms.assetid: 7ba55e39-05dd-43c7-b5da-b268ed8426dd
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9819aa01cd440167b23259e150f403574319e0bb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpagentdefault-transact-sql"></a>sp_help_agent_default (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el Id. de la configuración predeterminada del tipo de agente que se pasa como parámetro. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_agent_default [ @profile_id= ] profile_id OUTPUT   
        , [ @agent_type = ] agent_type  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@profile_id=**] *profile_id *** salida**  
 Es el identificador de la configuración predeterminada del tipo de agente. *profile_id* es **int**, no tiene ningún valor predeterminado. *profile_id* también es un parámetro de salida y devuelve el identificador de la configuración predeterminada para el tipo de agente.  
  
 [  **@agent_type=**] **'***agent_type***'**  
 Es el tipo de agente. *agent_type* es **int**, no tiene ningún valor predeterminado y puede ser uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**1**|Agente de instantáneas.|  
|**2**|Agente de lector del registro.|  
|**3**|Agente de distribución.|  
|**4**|Agente de mezcla.|  
|**9**|Agente de lectura de cola|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_agent_default** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **replmonitor** rol fijo de base de datos puede ejecutar **sp_help_agent_default**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
