---
title: dbo.syssessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syssessions_TSQL
- dbo.syssessions
- syssessions_TSQL
- syssessions
dev_langs:
- TSQL
helpviewer_keywords:
- syssessions system table
ms.assetid: 187819b6-c7f4-4a26-b74c-0a89e96695cf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 35b23525dc9762d012948e6eba0b41156b45ac69
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68056281"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cada vez que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia, crea una nueva sesión. El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza sesiones para mantener el estado de los trabajos cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia o se detiene de manera inesperada. Cada fila de la **syssessions** tabla contiene información sobre una sesión. Use la **sysjobactivity** tabla para ver el estado del trabajo al final de cada sesión.  
  
 Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Id. de una sesión del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**agent_start_date**|**datetime**|Fecha y hora en que se inició el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para esta sesión.|  
  
## <a name="remarks"></a>Comentarios  
 Solo los usuarios que son miembros de la **sysadmin** rol fijo de servidor puede tener acceso a esta tabla.  
  
## <a name="see-also"></a>Vea también  
 [dbo.sysjobactivity &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
