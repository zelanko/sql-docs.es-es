---
description: dbo.syssessions (Transact-SQL)
title: Sesiones de dbo.sys(Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 72fa9a3d55b3ed783fcbfc7c230676e7fe653eea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473303"
---
# <a name="dbosyssessions-transact-sql"></a>dbo.syssessions (Transact-SQL)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Cada vez que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicia, crea una nueva sesión. El Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza sesiones para mantener el estado de los trabajos cuando el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia o se detiene de manera inesperada. Cada fila de la tabla **syssessions** contiene información sobre una sesión. Use la tabla **sysjobactivity** para ver el estado del trabajo al final de cada sesión.  
  
 Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|Id. de una sesión del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta session_id no es el SPID de la sesión, sino un valor de identidad dentro de esta tabla del sistema.|  
|**agent_start_date**|**datetime**|Fecha y hora en que se inició el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para esta sesión.|  
  
## <a name="remarks"></a>Observaciones  
 Solo los usuarios que son miembros del rol fijo de servidor **sysadmin** pueden tener acceso a esta tabla.  
  
## <a name="see-also"></a>Consulte también  
 [dbo.sysjobactivity &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-sysjobactivity-transact-sql.md)  
  
  
