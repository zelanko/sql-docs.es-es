---
title: dbo.sysjobs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
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
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs: TSQL
helpviewer_keywords: sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1fd6e90a9e823e38a83f5b218027e15183ab76ae
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena la información de cada trabajo programado que debe ejecutar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Id. único del trabajo.|  
|**originating_server_id**|**int**|Id. del servidor del que proviene el trabajo.|  
|**Nombre**|**sysname**|Nombre del trabajo.|  
|**habilitado**|**tinyint**|Indica si el trabajo está habilitado para su ejecución.|  
|**Descripción**|**nvarchar(512)**|Descripción del trabajo.|  
|**start_step_id**|**int**|Id. del paso del trabajo en el que debe comenzar la ejecución.|  
|**category_id**|**int**|Id. de la categoría del trabajo.|  
|**owner_sid**|**varbinary (85)**|Número identificador de seguridad (SID) del propietario del trabajo.|  
|**notify_level_eventlog**|**int**|**Máscara de bits** que indica en qué circunstancias se debe registrar un evento de notificación en el registro de aplicación de Microsoft Windows:<br /><br /> **0** no = nunca<br /><br /> **1** = cuando el trabajo tiene éxito<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cuando el trabajo se completa (independientemente del resultado del trabajo)|  
|**notify_level_email**|**int**|Máscara de bits que indica en qué circunstancias se debe enviar una notificación por correo electrónico cuando se completa un trabajo:<br /><br /> **0** no = nunca<br /><br /> **1** = cuando el trabajo tiene éxito<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cuando el trabajo se completa (independientemente del resultado del trabajo)|  
|**notify_level_netsend**|**int**|Máscara de bits que indica en qué circunstancias se debe enviar un mensaje de red cuando se completa un trabajo:<br /><br /> **0** no = nunca<br /><br /> **1** = cuando el trabajo tiene éxito<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cuando el trabajo se completa (independientemente del resultado del trabajo)|  
|**notify_level_page**|**int**|Máscara de bits que indica en qué circunstancias se debe enviar un mensaje a un localizador cuando se completa un trabajo:<br /><br /> **0** no = nunca<br /><br /> **1** = cuando el trabajo tiene éxito<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cuando el trabajo se completa (independientemente del resultado del trabajo)|  
|**notify_email_operator_id**|**int**|Nombre de correo electrónico del operador que recibe la notificación.|  
|**notify_netsend_operator_id**|**int**|Id. del equipo o del usuario utilizado para enviar mensajes de red.|  
|**notify_page_operator_id**|**int**|Id. del equipo o del usuario utilizado para enviar un mensaje de localizador.|  
|**delete_level**|**int**|**Máscara de bits** que indica en qué circunstancias se debe eliminar el trabajo cuando se completa un trabajo:<br /><br /> **0** no = nunca<br /><br /> **1** = cuando el trabajo tiene éxito<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cuando el trabajo se completa (independientemente del resultado del trabajo)|  
|**Date_Created**|**datetime**|Fecha en que se creó el trabajo.|  
|**DATE_MODIFIED**|**datetime**|Fecha en que se modificó el trabajo por última vez.|  
|**version_number**|**int**|Versión del trabajo.|  
  
  
