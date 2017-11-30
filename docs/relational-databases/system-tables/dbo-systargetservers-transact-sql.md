---
title: dbo.systargetservers (Transact-SQL) | Documentos de Microsoft
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
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs: TSQL
helpviewer_keywords: systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c46f7d8861376b5bc8a25f4befc3c46dad31342
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra los servidores de destino que están datos de alta actualmente en este dominio de operación multiservidor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Identificador de servidor.|  
|**nombre_servidor**|**sysname**|Nombre de servidor.|  
|**ubicación**|**nvarchar (200)**|Ubicación del servidor de destino especificado.|  
|**time_zone_adjustment**|**int**|Intervalo de ajuste horario, en horas, desde la hora del meridiano de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Fecha y hora en que se dio de alta el servidor de destino especificado.|  
|**last_poll_date**|**datetime**|Fecha y hora en que el servidor de destino especificado sondeó por última vez el multiservidor **sysdownloadlist** tabla del sistema para que puedan ejecutar trabajos.|  
|**status**|**int**|Estado del servidor de destino:<br /><br /> **1** = Normal<br /><br /> **2** = resincronización pendiente<br /><br /> **4** = sospecha sin conexión|  
|**local_time_at_last_poll**|**datetime**|Fecha y hora en que se sondeó por última vez el servidor de destino para detectar operaciones de trabajo.|  
|**enlisted_by_nt_user**|**nvarchar (100)**|Nombre de usuario de la persona que ejecuta **sp_msx_enlist** en el servidor de destino.|  
|**poll_internal**|**int**|Número de segundos que transcurren antes de que el servidor de destino sondee el servidor maestro para detectar nuevas instrucciones de descarga.|  
  
  
