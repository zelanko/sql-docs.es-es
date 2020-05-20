---
title: DBO. systargetservers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.systargetservers_TSQL
- dbo.systargetservers
- systargetservers_TSQL
- systargetservers
dev_langs:
- TSQL
helpviewer_keywords:
- systargetservers system table
ms.assetid: 479d1314-be37-4d19-ac9c-419fc9110e53
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 6193bdfaaac12d34ed4993b71fd6b5862046384c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813887"
---
# <a name="dbosystargetservers-transact-sql"></a>dbo.systargetservers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Registra los servidores de destino que están datos de alta actualmente en este dominio de operación multiservidor.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|IDENTIFICADOR del servidor.|  
|**server_name**|**sysname**|Nombre de servidor.|  
|**ubicación**|**nvarchar(200)**|Ubicación del servidor de destino especificado.|  
|**time_zone_adjustment**|**int**|Intervalo de ajuste horario, en horas, desde la hora del meridiano de Greenwich (GMT).|  
|**enlist_date**|**datetime**|Fecha y hora en que se dio de alta el servidor de destino especificado.|  
|**last_poll_date**|**datetime**|Fecha y hora en que el servidor de destino especificado sondeó por última vez la tabla del sistema **sysdownloadlist** del multiservidor para la ejecución de los trabajos.|  
|**status**|**int**|Estado del servidor de destino:<br /><br /> **1** = normal<br /><br /> **2** = resincronización pendiente<br /><br /> **4** = sospechoso sin conexión|  
|**local_time_at_last_poll**|**datetime**|Fecha y hora en que se sondeó por última vez el servidor de destino para detectar operaciones de trabajo.|  
|**enlisted_by_nt_user**|**nvarchar(100**|Nombre de usuario de la persona que ejecuta **sp_msx_enlist** en el servidor de destino.|  
|**poll_internal**|**int**|Número de segundos que transcurren antes de que el servidor de destino sondee el servidor maestro para detectar nuevas instrucciones de descarga.|  
  
  
