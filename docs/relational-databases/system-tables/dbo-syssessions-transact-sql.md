---
title: DBO. syssessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
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
ms.openlocfilehash: 566445a3680dc54382a7e3e66bf77dbcbddca2e8
ms.sourcegitcommit: 4933934fad9f3c3e16406952ed964fbd362ee086
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/31/2019
ms.locfileid: "75548288"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Cada vez que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia, crea una nueva sesión. El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza sesiones para mantener el estado de los trabajos cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia o se detiene de manera inesperada. Cada fila de la tabla **syssessions** contiene información sobre una sesión. Use la tabla **sysjobactivity** para ver el estado del trabajo al final de cada sesión.  
  
 Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**Inter**|Id. de una sesión del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta session_id no es el SPID de la sesión, sino un valor de identidad dentro de esta tabla del sistema.|  
|**agent_start_date**|**DateTime**|Fecha y hora en que se inició el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para esta sesión.|  
  
## <a name="remarks"></a>Observaciones  
 Solo los usuarios que son miembros del rol fijo de servidor **sysadmin** pueden tener acceso a esta tabla.  
  
## <a name="see-also"></a>Véase también  
 [DBO. sysjobactivity &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
