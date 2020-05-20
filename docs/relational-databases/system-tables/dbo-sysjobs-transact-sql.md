---
title: DBO. sysjobs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8fe374a81fc88b6591da8fb0303d5ea490cccac0
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807067"
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysjobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Almacena la información de cada trabajo programado que debe ejecutar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Id. único del trabajo.|  
|**originating_server_id**|**int**|Id. del servidor del que proviene el trabajo.|  
|**name**|**sysname**|Nombre del trabajo.|  
|**activó**|**tinyint**|Indica si el trabajo está habilitado para su ejecución.|  
|**denominación**|**nvarchar(512)**|Descripción del trabajo.|  
|**start_step_id**|**int**|Id. del paso del trabajo en el que debe comenzar la ejecución.|  
|**category_id**|**int**|Id. de la categoría del trabajo.|  
|**owner_sid**|**varbinary(85)**|Número identificador de seguridad (SID) del propietario del trabajo.|  
|**notify_level_eventlog**|**int**|**Máscara** de archivo que indica en qué circunstancias se debe registrar un evento de notificación en el registro de aplicación de Microsoft Windows:<br /><br /> **0** = nunca<br /><br /> **1** = cuando el trabajo se realiza correctamente<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cada vez que se completa el trabajo (independientemente del resultado del trabajo)|  
|**notify_level_email**|**int**|Máscara de bits que indica en qué circunstancias se debe enviar una notificación por correo electrónico cuando se completa un trabajo:<br /><br /> **0** = nunca<br /><br /> **1** = cuando el trabajo se realiza correctamente<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cada vez que se completa el trabajo (independientemente del resultado del trabajo)|  
|**notify_level_netsend**|**int**|Máscara de bits que indica en qué circunstancias se debe enviar un mensaje de red cuando se completa un trabajo:<br /><br /> **0** = nunca<br /><br /> **1** = cuando el trabajo se realiza correctamente<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cada vez que se completa el trabajo (independientemente del resultado del trabajo)|  
|**notify_level_page**|**int**|Máscara de bits que indica en qué circunstancias se debe enviar un mensaje a un localizador cuando se completa un trabajo:<br /><br /> **0** = nunca<br /><br /> **1** = cuando el trabajo se realiza correctamente<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cada vez que se completa el trabajo (independientemente del resultado del trabajo)|  
|**notify_email_operator_id**|**int**|Nombre de correo electrónico del operador que recibe la notificación.|  
|**notify_netsend_operator_id**|**int**|Id. del equipo o del usuario utilizado para enviar mensajes de red.|  
|**notify_page_operator_id**|**int**|Id. del equipo o del usuario utilizado para enviar un mensaje de localizador.|  
|**delete_level**|**int**|**Máscara de máscara** que indica en qué circunstancias se debe eliminar el trabajo cuando se completa un trabajo:<br /><br /> **0** = nunca<br /><br /> **1** = cuando el trabajo se realiza correctamente<br /><br /> **2** = cuando se produce un error en el trabajo<br /><br /> **3** = cada vez que se completa el trabajo (independientemente del resultado del trabajo)|  
|**date_created**|**datetime**|Fecha en que se creó el trabajo.|  
|**date_modified**|**datetime**|Fecha en que se modificó el trabajo por última vez.|  
|**version_number**|**int**|Versión del trabajo.|  
  
  
