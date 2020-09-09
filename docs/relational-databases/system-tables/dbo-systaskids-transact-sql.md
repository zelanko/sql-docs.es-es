---
description: dbo.systaskids (Transact-SQL)
title: dbo.systaskids (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- systaskids_TSQL
- dbo.systaskids
- systaskids
- dbo.systaskids_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systaskids system table
ms.assetid: 45c56d89-4160-4d84-80bf-a7a05488792d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3a3e639fcc99f3b78d499e76062cd7f6d32f516c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551088"
---
# <a name="dbosystaskids-transact-sql"></a>dbo.systaskids (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una asignación de las tareas creadas en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a trabajos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] de la versión actual. Esta tabla se almacena en la base de datos **msdb** .  
  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**task_id**|**int**|Id. de la tarea|  
|**job_id**|**uniqueidentifier**|Id. del trabajo al que está asignada la tarea|  
  
  
